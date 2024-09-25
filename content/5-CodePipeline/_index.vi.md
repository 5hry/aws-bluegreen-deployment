---
title : "Tạo luồng CodePipeline"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---
![CodePipeline 1](/images/5.Codepipeline/arc.png)
Hình trên mô tả quá trình CI/CD với các dịch vụ của AWS. Mối quan hệ giữa các dịch vụ trong sơ đồ như sau:

1. **CodePipeline**: Là dịch vụ quản lý luồng công việc CI/CD, điều khiển việc tự động hóa triển khai ứng dụng thông qua các bước.

{{% notice info %}}
Hiện tại **CodeCommit** đã không còn hỗ trợ users mới nên mình chuyển qua dùng Github để tiện cho tất cả mọi người.
{{% /notice %}}

2. **CodeCommit Repo**: Lưu trữ mã nguồn của dự án, trong đó bao gồm các file `taskdef.json` và `appspec.yaml`. 
    - `taskdef.json`: Định nghĩa task cho **Amazon ECS**.
    - `appspec.yaml`: Định nghĩa các thông tin cần thiết cho việc triển khai trong **CodeDeploy**.

3. **Image Repo (Amazon ECR)**: Lưu trữ các Docker images được build từ dự án. Đây là nơi lưu giữ phiên bản container của ứng dụng.

4. **Amazon ECR action**: Lấy Docker image từ **Image Repo (Amazon ECR)** để đưa vào quy trình triển khai.

5. **Amazon ECS**: Dịch vụ chạy các container ứng dụng. **Amazon ECS** nhận Docker image từ **Amazon ECR** và thực thi ứng dụng.

6. **CodeDeploy ECS Blue/Green action**: Triển khai ứng dụng theo chiến lược **Blue/Green**, tức là có thể chạy hai phiên bản ứng dụng song song (một phiên bản hiện tại và một phiên bản mới), để đảm bảo rằng nếu phiên bản mới có lỗi, ta có thể quay lại phiên bản cũ một cách nhanh chóng.

7. **Amazon S3 artifact bucket**: Lưu trữ các artifacts (chẳng hạn như `imageDetail.json`) chứa các thông tin về quá trình triển khai, bao gồm thông tin về Docker image, **ECS task**, và quá trình **CodeDeploy**.

Quá trình tổng quan:
- **CodePipeline** bắt đầu quá trình CI/CD và điều hướng các hành động tiếp theo.
- **CodeCommit** quản lý mã nguồn, và sau khi mã được đẩy lên, nó kích hoạt hành động **Amazon ECR** để lấy Docker image. Tuy nhiên ở trong workshop này, mình sẽ thay thế **CodeCommit** bằng Github để phục vụ cho tất cả mọi người.
- Docker image sau đó được triển khai trên **Amazon ECS**.
- **CodeDeploy** quản lý việc triển khai ứng dụng với chiến lược **Blue/Green**, đồng thời lưu trữ thông tin chi tiết của quá trình triển khai vào **Amazon S3**.
