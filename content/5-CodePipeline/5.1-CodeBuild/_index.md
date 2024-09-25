---
title : "Create CodeBuild"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 5.1 </b> "
---

According to the model, we now have a Github repository containing the source code of the application, as mentioned in the **Introduction** section. Next, we need to create a build project using CodeBuild to build an image from the source code on Github.

We create a connection using OAuth.
![CodeBuild 1](/images/5.Codepipeline/01-CB.png)

For the Environment, select On Demand (pay based on build time). For the Image, choose an image managed by CodeBuild. For Compute, select EC2 to avoid timeouts, as Lambda has a time limit.
![CodeBuild 2](/images/5.Codepipeline/02-CB.png)

We assign this Build Project the permissions to interact with ECR, CloudWatch, and Secret Manager to read secret variables stored there, such as the username and password of the DockerHub account, in order to log in to DockerHub and push the image.
![CodeBuild 3](/images/5.Codepipeline/03-CB.png)

Next, we need to specify what the project should do during the build process using the buildspec.yaml file. There are 3 phases: pre_build (actions before the build), build (the build actions), and post_build (actions after the build is completed).

- **Pre_build**: Log in to ECR to get the URI of the repo and the commit hash of the repo, assigning these to two variables for use in the build process.
- **Build**: Build the image and tag the image.
- **Post_build**: Push the image to the ECR repo, then write the image information to the imageDetail.json file for CodeDeploy to use for deployment to ECS.

Below is the buildspec.yaml file to tell CodeBuild what to do.

![CodeBuild buildspec](/images/5.Codepipeline/buildspec-CB.png)

Specifically, in this file:
- In the **Pre_build** step, the Build Project will log in to DockerHub using the username and password stored in Secret Manager, log in to ECR, and retrieve the commit hash of the Github repo when triggering CodeBuild. 
- In the **Build** step, the Build Project will build the image from the source code on Github when triggered, then tag the image.
- Finally, in the **Post_build** step, the image will be pushed with two tags, `latest` and the commit hash, to ECR, and then the image information (Image URI and Repo) will be written to the **imageDetails.json** file.

The artifact files include:
- **appspec.yaml**: Defines the task, container, and container port for deployment to ECS.
- **imageDetail.json**: Contains information about the image that was built.
- **taskdef.json**: Contains the task definition for running in ECS.

Select the S3 bucket to store the artifacts:

![CodeBuild 4](/images/5.Codepipeline/04-CB.png)

Store build logs using CloudWatch.
![CodeBuild 5](/images/5.Codepipeline/05-CB.png)

Then select **Create build project** to complete the creation process.
{{% notice info %}}
Each time a Build Project is created, it will automatically run once without needing to be triggered by Github.
{{% /notice %}}

