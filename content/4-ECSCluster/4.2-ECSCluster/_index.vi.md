---
title : "Tạo ECS Cluster"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 4.2 </b> "
---

Tiếp đến sau khi đã tạo ECR - nơi chứa các image được build ra thì ta cần tạo một ECS Cluster để chứa service chạy các task chạy ứng dụng của chúng ta.

Giờ mình sẽ tạo một cluster để chứa service chạy các tasks. Chọn mode Fargate. 

![ECS 1](/images/4.ECS/01-ECS.png)

Sau khi tạo Cluster với những thông số cơ bản, tạo một service để deploy các tasks với launch type là fargate trong ECS Cluster vừa tạo.
![ECS 2](/images/4.ECS/02-ECS.png)

Deployment configure thì mình sẽ chọn service để launch một task group thay vì chỉ một task ⇒ hỗ trợ blue/green deployment. Ở đây ta cần tạo một task definition định nghĩa phần cứng ảo cũng như là container cho task chạy. Ta có thể vào ECS để tạo hoặc tạo bằng json. Nó có định nghĩa container trong task sẽ chạy image nào, container port, host port, …



![ECS 3](/images/4.ECS/03-ECS.png)

Để mà có thể thao tác với ECR, ECS, S3, ELB, … ta cần tạo một role để gán cho CodeDeploy có những quyền đó để lấy image từ ECR, deploy các tasks trong ECS và đọc source từ S3, ... 

![ECS 4](/images/4.ECS/04-ECS.png)

Ở phần networking ta sẽ chọn security group như đã trình bày lúc nãy. Vì ta Fargate này cần pull image từ ECR nên cần để public IP để có thể ra ngoài Internet, có thể tắt nếu cấu hình lại route table và NAT gateway.

![ECS 5](/images/4.ECS/05-ECS.png)

Cấu hình thêm Load Balancing chọn Production listener đã được thêm từ lúc đầu là port 80 và Test listener là port 81 forward đến 2 Target group blue và green. 
Chúng ta sẽ chọn ALB đã được tạo từ phần trước để forward traffic đến 2 TG blue và green.

![ECS 6](/images/4.ECS/06-ECS.png)
![ECS 7](/images/4.ECS/07-ECS.png)

Sau khi chọn **Create** thì ta đã có service với các tasks đang ở trạng thái pending.
![ECS 8](/images/4.ECS/08-ECS.png)