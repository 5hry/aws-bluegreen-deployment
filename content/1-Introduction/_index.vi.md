---
title : "Giới thiệu"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---
In this section, we will explore what **Blue/Green Deployment** is and the problem it solves.

First, in the traditional model, when updating an application, there is a downtime period during the deployment process because the same hardware (where the application is running) is used. To avoid disrupting the user experience, updates are often performed late at night, and the application is temporarily suspended. While this reduces the impact, it still causes some disruption for certain users.

To solve this issue, **Blue/Green Deployment** was introduced. This deployment strategy minimizes downtime to nearly zero. The idea behind this strategy is to create two identical hardware environments to run two production environments. The workflow can be summarized as follows:
- We have two identical hardware setups. One is running the current version of the application that users are interacting with, called **Blue**, while the other environment runs the new version of the application (not yet released to users), called **Green**.
- Once the new version is deployed and there are no issues, user traffic is routed to the **Green** environment.
- The **Blue** environment then becomes the environment for the next deployment version.
![Architecture](/images/bluegreen.png)
Thus, with this strategy, the downtime issue has been resolved.