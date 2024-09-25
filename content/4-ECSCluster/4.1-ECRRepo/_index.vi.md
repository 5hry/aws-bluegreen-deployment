---
title : "Tạo ECR Repo"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 4.1 </b> "
---

Đầu tiên vì chúng ta chạy ứng dụng container nên cần tạo ra image, vì vậy ta cũng cần nơi bảo mật để chứa các image đó và cũng tiện để truy cập từ ECS. Do đó, ta có thể chọn ECR để lưu trữ các image được build ra. Ta thực hiện tạo một ECR repo có tên là **ws1-bluegreen-repo** như hình dưới. 

{{% notice warning %}}
Nếu như những image trong này không phục vụ bất cứ tác vụ nào ở ngoài dịch vụ AWS thì nên để ở private để đảm bảo bảo mật, tránh bị đánh cắp image.
{{% /notice %}}


![ECR 1](/images/4.ECS/01-ECR.png)