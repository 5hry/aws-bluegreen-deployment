---
title : "Tạo Application Load Balancer trỏ đến 2 TG"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 3.2. </b> "
---
ALB để nhận traffic trực tiếp từ users nên cần chọn scheme Internet Facing, hiện tại chỉ cần IPv4.
![ALB 1](/images/3.ALB-TG/01-ALB.png)

Ở đây chọn hết 3 zones của region Singapore.

{{% notice tip %}}
Ở đây, ta cần chọn ít nhất 2 zones, tuy nhiên càng nhiều càng tốt. Ở mỗi zone chúng ta chọn thì ALB sẽ đặt một ...(cái này mình quên, mình sẽ tìm hiểu và update lại) ở public subnet của zone đó. Sau đó, khi traffic vào hoặc ra subnet của zone đó thì sẽ đi thông qua cái đó.
{{% /notice %}}
![ALB 2](/images/3.ALB-TG/02-ALB.png)

Tạo 2 listeners, ở đây mỗi listener sẽ lắng nghe một port trên ALB sau đó sẽ forward traffic đến cho từng TG tương ứng, ở đây port 80 sẽ forward đến Blue group, và port 81 sẽ forward đến Green group.

![ALB 3](/images/3.ALB-TG/03-ALB.png)

{{% notice warning %}}
Trong Security group phải mở cả 2 port 80 cho users và port 81 cho phục vụ người nào đảm nhiệm testing. Nếu không mở port 81  thì sẽ không thể truy cập vào testing environment được.
{{% /notice %}}

![ALB 4](/images/3.ALB-TG/04-ALB.png)

Ta có thể xem tổng quan về ALB chúng ta sắp tạo ở dưới đây, nếu có gì sai sót có thể sửa lại trước khi nhấn **Create**.
![ALB 5](/images/3.ALB-TG/05-ALB.png)

Sau khi **Create**, ta đã có được DNS name, chúng ta có thể truy cập thông qua DNS name này.

![ALB 6](/images/3.ALB-TG/06-ALB.png)