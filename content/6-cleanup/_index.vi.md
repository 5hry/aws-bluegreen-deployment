+++
title = "Kết quả, dọn dẹp tài nguyên"
date = 2021
weight = 6
chapter = false
pre = "<b>6. </b>"
+++

Kết quả, chúng ta có thể truy cập trang web thông qua DNS name của ALB. 
![Result](/images/6.clean/result.png)

Ở trên là chi tiết các bước deploy ECS service sử dụng chiến lược Blue/Green Deployment. Và có thể truy cập được qua [DNS của ALB](http://ws1-bluegreen-alb-1574488828.ap-southeast-1.elb.amazonaws.com/). Tiếp tục mình sẽ củng cố, phát triển, sử dụng Route53 để triển khai route traffic để tối ưu hóa việc route traffic.

Ở phần clean resource, ta có thể để lại một vài thứ như bộ CodeBuild CodeDeploy và CodePipeline vì những service này tính tiền theo mình xài nhiêu trả nhiêu nên có thể để lại nếu như cần phục vụ mục đích sau này. ECS thì ta có thể cho desired task = 0 gần như là không mất phí, nếu như tạm thời ngừng bài workshop và cần làm tiếp thì đây là cách hiệu quả nhất. 
Ngoài ra ta sẽ xóa ALB, TG, ... 
Chọn ALB, confirm xóa.
![ALB 1](/images/6.clean/01-alb.png)
![ALB 2](/images/6.clean/02-alb.png)
![ALB 3](/images/6.clean/03-alb.png)
Nếu có tạo EC2 để chạy database thì xóa luôn EC2. Chọn EC2 và **Stop** nếu cần để phục vụ sau này, không thì ta **Terminate** luôn.
![EC2 1 ](/images/6.clean/01-ec2.png)

Cuối cùng, nếu tạo quá nhiều image trong ECR thì nên xóa, có thể để lại image mới nhất để phục vụ sau này.
![ECR 1](/images/6.clean/01-ECR.png)

Xóa các Task Definition cũ nếu không cần dùng đến, deregister các Task cũ.
![Task def 1](/images/6.clean/01-task.png)

Vậy là mình đã hoàn thành việc clean resource. Cảm ơn các bạn đã đọc, nếu có góp ý về nội dung các bạn có thể liên hệ qua [facebook này](https://wwww.facebook.com/stn.akai).