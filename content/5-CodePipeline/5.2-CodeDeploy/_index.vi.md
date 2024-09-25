---
title : "Tạo CodeDeploy"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 5.2 </b> "
---
Sau khi đã tạo xong Build Project, ta sẽ tạo CodeDeploy để lấy image được build ra từ Build Project để triển khai chạy các task trong 2 target **Blue** và **Green**.

Vào CodeDeploy, tạo một application với platform là **Amazon ECS**.
![CodeDeploy 1](/images/5.Codepipeline/01-CD.png)

Từ applications vừa tạo, tạo thêm một deployment group để chứa các deployments.
![CodeDeploy 2](/images/5.Codepipeline/02-CD.png)

Trong đó cần role có những quyền đọc ECR, deploy ECS, đọc S3, và ALB để điều chỉnh traffic. 
![CodeDeploy role](/images/5.Codepipeline/role-CD.png)

Tiếp đó ta sẽ cấu hình các thông tin về cluster, service, ALB,… Chọn lại thông tin Cluster và Service đã tạo phần trước và ALB, Target Group đã tạo ở phần 2.
![CodeDeploy 3](/images/5.Codepipeline/03-CD.png)

Ở đây ta có thể cấu hình deployment theo nhiều cách như có thể reroute traffic ngay lập tức khi tạo xong các task mới hoặc có thể cấu hình thời gian để reroute traffic, chiến lược reroute,… và terminate các task đang chạy phiên bản cũ. 
![CodeDeploy 4](/images/5.Codepipeline/05-CD.png)

Chọn **Create Deployment group** để tạo.

Khi chạy deploy thì sẽ khởi tạo CloudFormation để tạo các resource trên ECS.