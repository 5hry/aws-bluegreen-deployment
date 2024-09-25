---
title : "Tạo CodePipeline"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 5.3 </b> "
---
Sau khi đã hoàn thành tạo Build project và Deployment group ở phần trước, thì ta sẽ tạo CodeDeploy để kết nối 2 service này lại để khi trigger từ source code sẽ chạy 2 service này liên tục và output của Build project là các file artifact sẽ làm input cho Deployment để triển khai các task lên ECS service.

- Chọn mode Superseded để có thể thực hiện đè được luồng pipeline cũ. 
- Ta có thể tạo mới role và gán thêm các policy mới cho role đó, ví dụ như S3, các quyền liên quan được gán trong 2 service CodeBuild và CodeDeploy.

![CodePipeline 1](/images/5.Codepipeline/01-CP.png)

Source stage: Ta có thể kết nối với source code từ github thông qua connection kết nối với Github và chỉ ra repo cũng như branch của repo cho pipeline.
![CodePipeline 2](/images/5.Codepipeline/02-CP.png)
Ở đây có thể chọn các thông tin về trigger từ Github: no filter (trigger pipeline với bất kì push hoặc clone repo), specify filter (chỉ ra các commit nào mới trigger pipeline), hoặc không không tự động trigger pipeline.
![CodePipeline 3](/images/5.Codepipeline/03-CP.png)
Build stage: Chỉ ra build project đã tọa hoặc tạo project mới.
![CodePipeline 4](/images/5.Codepipeline/04-CP.png)
Deploy stage: stage này sẽ chỉ ra cần deploy application nào, trong deploy group nào, cũng như các artifacts được lưu ở đâu. Ta sẽ chọn deploy application và group vừa tạo. Chọn BuildArtifact từ S3.  
![CodePipeline 5](/images/5.Codepipeline/05-CP.png)
Các file artifacts: **appspec.yaml**, **taskdef.json** để chỉ ra task, container chạy image vừa được build ra.
![CodePipeline appspec.yaml](/images/5.Codepipeline/appspec-CP.png)
![CodePipeline taskdef.json](/images/5.Codepipeline/taskdef-CP.png)

Sau khi hoàn tất quá trình tạo CodePipeline thì có thể chọn Release change để chạy Pipeline, khi chạy từng stage, ta có thể xem chi tiết quá trình bằng cách chọn View detail. 
![CodePipeline 5](/images/5.Codepipeline/05-CP.png)
Sau khi chạy thì giờ đã có thêm một task mới chạy new revision của taskdef. 
![CodePipeline 6](/images/5.Codepipeline/06-CP.png)

**Add Notifications**: Ngoài ra, ta có thể  thêm stage vào pipeline, ví dụ sau khi thay đổi source code, sau khi build xong thì sẽ cần người review lại xem có thực hiện bước tiếp theo không. Mình sẽ tạo thêm SNS để thông báo tới những người này xem có confirm chạy bước tiếp theo không.
![CodePipeline 7](/images/5.Codepipeline/07-CP.png)

Tạo một subscription để thông báo qua mail,…
![CodePipeline 8](/images/5.Codepipeline/0-CP.png)

Add stage để thêm bước Manual Approval 
![CodePipeline 9](/images/5.Codepipeline/09-CP.png)
Thêm action là Manual Approval và sau khi chạy tới stage này thì pipe sẽ dừng và chờ confirm thì mới được chạy tiếp tục.
![CodePipeline 10](/images/5.Codepipeline/10-CP.png)
Khi build xong thì tới stage này sẽ chờ để Approval hoặc Reject thì sẽ tiếp tục hoặc dừng pipeline để chờ confirm từ người kiểm tra.
![CodePipeline 11](/images/5.Codepipeline/11-CP.png)
![CodePipeline 12](/images/5.Codepipeline/12-CP.png)
Sau khi chạy tới bước Deployment thì ta có thể xem quá trình deploy ở deployment trong detail. Ở đây, ta có thể xem được thông tin quá trình deploy, các task được tạo mới và có thể reroute trước traffic thay vì hết thời gian đã chỉ định. Hoặc cũng có thể rollback ngay khi phát hiện lỗi mà không có downtime.
![CodePipeline 13](/images/5.Codepipeline/13-CP.png)
![CodePipeline 14](/images/5.Codepipeline/14-CP.png)
