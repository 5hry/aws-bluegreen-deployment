---
title : "Create CodePipeline"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 5.3 </b> "
---

After completing the creation of the Build project and Deployment group in the previous section, we will now create CodeDeploy to connect these two services. When triggered by the source code, these services will run continuously, with the output of the Build project (artifacts) serving as the input for the Deployment to deploy tasks to the ECS service.

- Select the Superseded mode to overwrite the old pipeline flow.
- You can create a new role and assign additional policies, such as S3 permissions, and related permissions for both CodeBuild and CodeDeploy services.

![CodePipeline 1](/images/5.Codepipeline/01-CP.png)

Source stage: You can connect the source code from Github via a connection to Github, specifying the repo and branch for the pipeline.
![CodePipeline 2](/images/5.Codepipeline/02-CP.png)

You can choose the trigger settings for Github: no filter (trigger pipeline with any push or clone of the repo), specify filter (specify which commits trigger the pipeline), or disable automatic triggers.
![CodePipeline 3](/images/5.Codepipeline/03-CP.png)

Build stage: Specify the previously created Build project or create a new one.
![CodePipeline 4](/images/5.Codepipeline/04-CP.png)

Deploy stage: This stage specifies which application to deploy, in which deployment group, and where the artifacts are stored. Select the application and deployment group you just created. Choose BuildArtifact from S3.
![CodePipeline 5](/images/5.Codepipeline/05-CP.png)

Artifact files: **appspec.yaml** and **taskdef.json** specify the task and container to run the image that was just built.
![CodePipeline appspec.yaml](/images/5.Codepipeline/appspec-CP.png)
![CodePipeline taskdef.json](/images/5.Codepipeline/taskdef-CP.png)

After completing the CodePipeline setup, you can choose **Release change** to run the Pipeline. As each stage runs, you can view the details of the process by selecting **View detail**.
![CodePipeline 5](/images/5.Codepipeline/05-CP.png)

Once executed, a new task running the new revision of the task definition is created.
![CodePipeline 6](/images/5.Codepipeline/06-CP.png)

**Add Notifications**: You can add additional stages to the pipeline, for example, after source code changes or after the build, a manual review might be required to proceed. To achieve this, you can create an SNS to notify reviewers, asking them to confirm whether to continue to the next stage.
![CodePipeline 7](/images/5.Codepipeline/07-CP.png)

Create a subscription to send notifications via email, etc.
![CodePipeline 8](/images/5.Codepipeline/0-CP.png)

Add a stage for **Manual Approval**.
![CodePipeline 9](/images/5.Codepipeline/09-CP.png)

Add a **Manual Approval** action. Once the pipeline reaches this stage, it will pause and wait for confirmation before proceeding.
![CodePipeline 10](/images/5.Codepipeline/10-CP.png)

After the build is completed, it will wait for **Approval** or **Reject**, continuing or pausing the pipeline for confirmation from the reviewer.
![CodePipeline 11](/images/5.Codepipeline/11-CP.png)
![CodePipeline 12](/images/5.Codepipeline/12-CP.png)

Once the pipeline reaches the **Deployment** step, you can view the deployment details. Here, you can monitor the deployment process, see newly created tasks, and even manually reroute traffic before the specified time elapses. You can also rollback if an error is detected without causing downtime.
![CodePipeline 13](/images/5.Codepipeline/13-CP.png)
![CodePipeline 14](/images/5.Codepipeline/14-CP.png)

