---
title : "Tạo hai target groups blue và green"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 3.1. </b> "
---
Tạo 2 Target Groups Blue và Green để chứa  các tasks chạy ứng dụng web trong ECS Cluster. Ở đây chọn target type là **IP Address** vì các task ta sẽ chạy mode Fargate thay vì EC2 instance.

![Target Groups 1](/images/3.ALB-TG/01-TG.png)

Mở port 80 trên cả 2 target group.

![Target Groups 2](/images/3.ALB-TG/02-TG.png)

Có thể cấu hình health check để kiểm tra xem các task được register trong TG có healthy không. Health check ở trang gốc.

![Target Groups 3](/images/3.ALB-TG/03-TG.png)

Các thông số nâng cao cho health check.

![Target Groups 4](/images/3.ALB-TG/04-TG.png)

Bây giờ đã có 2 target groups blue và green. Tuy nhiên 2 Target groups blue và green này vẫn chưa được associate cho Load Balancer nào. Vì vậy cần tạo ALB để load traffic vào 2 TG này.
![Target Groups 5](/images/3.ALB-TG/05-TG.png)

