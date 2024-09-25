---
title : "Create ECR Repo"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 4.1 </b> "
---

First, since we are running a containerized application, we need to create an image. Therefore, we also need a secure place to store these images that is easily accessible from ECS. We can choose ECR to store the built images. We create an ECR repo named **ws1-bluegreen-repo** as shown below.

{{% notice warning %}}
If the images in this repo are not serving any tasks outside of AWS services, it is recommended to keep them private to ensure security and prevent image theft.
{{% /notice %}}

![ECR 1](/images/4.ECS/01-ECR.png)
