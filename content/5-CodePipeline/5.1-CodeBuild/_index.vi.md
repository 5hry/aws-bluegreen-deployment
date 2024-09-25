---
title : "Tạo CodeBuild"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 5.1 </b> "
---
Theo như mô hình, hiện tại ta đã có repo Github chứa source code của ứng dụng được trình bày ở phần **Introduction**. Tiếp theo chúng ta cần tạo một build project bằng CodeBuild để build ra image từ source code trên Github. 

Ta tạo connection đến bằng OAuth.
![CodeBuild 1](/images/5.Codepipeline/01-CB.png)

Environment ta chọn On Demand (tính tiền dựa trên thời gian Build), Image chọn image được quản lý bởi CodeBuild, Compute ta chọn EC2 để tránh việc có thể bị ngắt nếu như build quá lâu vì Lambda có giới hạn thời gian.
![CodeBuild 2](/images/5.Codepipeline/02-CB.png)
Chúng ta gán cho Build Project này các quyền tương tác với ECR, CloudWatch và Secret Manager để đọc các biến secret được lưu ở đây ví dụ như username, password của account DockerHub để đăng nhập vào DockerHub để push image lên. 
![CodeBuild 3](/images/5.Codepipeline/03-CB.png)

Tiếp theo ta cần chỉ ra cho project biết được cần làm gì trong quá trình build thông qua file buildspec.yaml. Có 3 phase là pre_build (thực hiện các hành động trước khi build), build (hành động build) và post_build (sau khi build xong thực hiện các hành động này). 

- **Pre_build**: log in vào ECR để lấy URI của repo và commit hash của repo gán vào 2 biến để phục vụ quá trình build.
- **Build**: Thực hiện build ra image và đánh tag cho image đó.
- **Post_build**: push image lên lại ECR repo, ghi thông tin về image ra file imageDetail.json để phục vụ cho CodeDeploy đọc thông tin triển khai cho ECS.

Dưới đây là file buildspec.yaml để chỉ ra cho CodeBuild biết cần làm gì.

![CodeBuild buildspec](/images/5.Codepipeline/buildspec-CB.png)

Cụ thể thì trong file này, ở bước **Pre_build** thì Build Project này sẽ đăng nhập vào DockerHub với username và password lưu trong Secret Manager, đăng nhập vào ECR, và lấy commit hash của Github repo khi trigger CodeBuild. Bước **Build**, Build Project sẽ thực hiện build ra image từ source code trên github khi trigger, sau đó đánh tag cho image. Cuối cùng, ở bước **Post_build** thì sẽ push image với 2 tag latest và commit hash lên ECR, sau đó ghi thông tin image (Image URI và Repo) vào file **imageDetails.json**.

Các file artifacts như: 
- **appspec.yaml**: để chỉ ra task def và container cũng như port của container để triển khai lên ECS.
- **imageDetail.json**: chứa thông tin và image vừa được build ra.
- **taskdef.json**: chứa thông tin định nghĩa task chạy trong ECS.

Chọn S3 bucket để lưu các artifacts:


![CodeBuild 4](/images/5.Codepipeline/04-CB.png)

Lưu logs của quá trình Build bằng CloudWatch.
![CodeBuild 5](/images/5.Codepipeline/05-CB.png)

Sau đó chọn **Create build project** để hoàn thành quá trình tạo.
{{% notice info %}}
Mỗi khi tạo một Build Project, sau khi tạo xong nó sẽ tự động chạy 1 lần mà chưa cần trigger từ Github.
{{% /notice %}}