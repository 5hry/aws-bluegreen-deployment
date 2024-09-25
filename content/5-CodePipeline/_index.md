---
title : "Create CI/CD pipeline"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---

![CodePipeline 1](/images/5.Codepipeline/arc.png)
The image above illustrates the CI/CD process with AWS services. The relationship between the services in the diagram is as follows:

1. **CodePipeline**: This service manages the CI/CD workflow, automating the application deployment process through various steps.

{{% notice info %}}
Currently, **CodeCommit** no longer supports new users, so I have switched to using Github to make it more convenient for everyone.
{{% /notice %}}

2. **CodeCommit Repo**: Stores the project's source code, including the `taskdef.json` and `appspec.yaml` files. 
    - `taskdef.json`: Defines the task for **Amazon ECS**.
    - `appspec.yaml`: Specifies the necessary information for deployment in **CodeDeploy**.

3. **Image Repo (Amazon ECR)**: Stores the Docker images built from the project. This is where the container version of the application is kept.

4. **Amazon ECR action**: Retrieves the Docker image from **Image Repo (Amazon ECR)** to enter the deployment process.

5. **Amazon ECS**: This service runs containerized applications. **Amazon ECS** retrieves the Docker image from **Amazon ECR** and runs the application.

6. **CodeDeploy ECS Blue/Green action**: Deploys the application using the **Blue/Green** strategy, allowing two application versions to run in parallel (one current version and one new version). This ensures that if the new version has issues, you can quickly revert to the old version.

7. **Amazon S3 artifact bucket**: Stores artifacts (such as `imageDetail.json`), which contain information about the deployment process, including details on the Docker image, **ECS task**, and the **CodeDeploy** process.

Overview of the process:
- **CodePipeline** starts the CI/CD process and directs the subsequent actions.
- **CodeCommit** manages the source code, and once the code is pushed, it triggers the **Amazon ECR** action to retrieve the Docker image. However, in this workshop, we will replace **CodeCommit** with Github for everyone's convenience.
- The Docker image is then deployed on **Amazon ECS**.
- **CodeDeploy** manages the application deployment using the **Blue/Green** strategy, while detailed deployment information is stored in **Amazon S3**.
