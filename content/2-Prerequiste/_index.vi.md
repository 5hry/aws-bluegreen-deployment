---
title : "Các bước chuẩn bị"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2. </b> "
---
{{% notice warning %}}
Bạn cần có sẵn một ứng dụng web, nếu như không có thì không thể làm tiếp được. Có thể tham khảo và sử dụng ứng dụng web [ở đây](https://github.com/5hry/e-commerce-web-bluegreen-deploy)
{{% /notice %}}

Workshop này yêu cầu cần source code cho ứng dụng web và Dockerfile để build ứng dụng.
Trong workshop này mình sẽ sử dụng ứng dụng web bán hàng, cụ thể là những thiết bị điện tử. Có truy cập database được chạy trên một EC2 Instance.

Vì workshop này tập trung vào BlueGreenDeployment nên mình tạo một EC2 Instance để chạy database để tiết kiệm.

Mình có chuẩn bị một Dockerfile để chạy database ở mã nguồn ở trên. Các bạn có thể tải về để chạy hoặc có thể copy DNS của EC2 Instance mình đã tạo ở đây (**ec2-54-169-49-30.ap-southeast-1.compute.amazonaws.com**) cho vào file connectDB.php
![Image](/images/2.prerequisite/001-connectDB.png)
EC2 đang chạy một image database của ứng dụng.
![Docker Database](/images/2.prerequisite/002-docker.png)

Bây giờ ta có thể follow theo các bước trong Workshop mà không cần lo lắng thiếu gì nữa.