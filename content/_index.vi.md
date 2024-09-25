---
title : "ECS Service Blue/Green Deployment"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
---
# Triển khai Amazon ECS Service sử dụng chiến lược Blue/Green Deployment

### Tổng quan
Trong phần này, chúng ta sẽ triển khai chiến lược này trên AWS Cloud với kiến trúc được minh họa dưới đây.

![Architecture](/images/main-arc.png)

Tóm tắt ngắn gọn về hệ thống: khi người dùng truy cập Internet, họ sẽ đi qua một Application Load Balancer mở hai cổng, 80 và 81, trỏ đến hai Target Groups đã đăng ký các tasks trong ECS Service. Cổng 80 sẽ chuyển hướng lưu lượng truy cập đến các tasks đang chạy trong môi trường sản xuất, trong khi cổng 81 chuyển hướng lưu lượng đến các tasks chạy để kiểm tra. Các tasks này trỏ đến một cơ sở dữ liệu chạy trên một EC2 instance.

Về phần Deployment, khi mã nguồn được đẩy lên Github, nó sẽ kích hoạt **CodeBuild** để xây dựng lại image mới từ mã nguồn, sau đó đẩy các artifacts lên S3 để **CodeDeploy** có thể kéo về và triển khai lên ECS Cluster. (Ở đây, chúng ta không sử dụng **CodeCommit** vì dịch vụ này không còn hỗ trợ tài khoản mới, nên chúng ta sử dụng Github thay thế.)
