# ORMAE-DevOps-Test

Objective - 

Chalk out a Git repository structure in terms of helping in reaching maximum efficiency in terms of ease of development and collaborating. 

Lay down a plan for CI/CD. As there will be tests pertaining to each microservice, how do you plan to run them in tandem in the deployment pipeline. 

Prepare a deployment strategy that can be adapted for Staging, UAT and Production. Note that staging setup needs to be less in terms of operating cost. 

Prepare a plan to see logs in all the above three environments. 

Prepare a plan to add alerts and monitoring across all of the mentioned components.

Explanation:

I am going with Hybrid Cloud platform Architecture because it is cost aptimized and Flexible to upgrade the infrastructure and software installations.

First of all let me give you an overview of what we were trying to achieve:

We are working on an ECommerce application using by microservices.

We created DevOps pipeline for those services independently.
         
 In order to achieve these one of the most important requirement was Git repository's for our code
         
 But the main problem was whether to keep all the services in the same repository in separate folders Mono repository or to keep separate repositories for each of the services Multiple repositories.
 
Both had their pros and cons. But at first I went for the 2nd option i.e separate repository for each service but I will show you the Mono repository setup as well which is actually a good choice for the development environment.

So what made me go in that direction?

One of the main reason behind micro-service architecture was to release software faster, and to create small teams to develop and deliver a single service. i.e managing the whole life cycle of the micro service was a team’s responsibility from development to delivery and maintenance. Thus creating separate repository for different service made sense because a team can then concentrate on a particular repository and we can maintain separate development and release for them.

Using multiple repository setup help in different ways:

Clear ownership: Having separate repository for a particular service is a definite microservice way of doing things because the team that owns that service is clearly responsible for independently develop and deploy the full stack of that microservice.

Smaller code base: Separate repositories for a service leads to smaller code base and lesser complexity during code merge.

Narrow clones: While doing DevOps and automated build and releases, smaller code base leads to considerably lesser code download/clone time, that leads to faster build and deployments.


CI/CD process for a microservices architecture:

The code repository is a multi repository, with folders organized by microservice.

The team's branching strategy is based on trunk-based development.

The team uses release branches to manage releases. Separate releases are created for each microservice.

The CI/CD process uses Jenkins Pipelines to build, test, and deploy the microservices to EKS.

The container images for each microservice are stored in Elastic Container Registry.

The team uses Helm charts to package each microservice.

Checks that no other deployments are happening in parallel for the same service

Installs the previously prepared Helm package (created in CI pipeline)

Commits back to the git repo the dependencies list of the app

Creates a mark in New Relic for monitoring purposes

Sends a message to our teams to show the status of the deployment

CI/CD pipeline for deploying microservices to Kubernetes Service:

Automating application deployment, scaling, and management. Kubernetes provides a platform for automating deployment, scaling, and operations of containerized applications across clusters of hosts. Building efficient and scalable applications in the cloud.

You can deploy and manage containerized applications more easily with a fully managed Kubernetes service. Elastic Kubernetes Service (EKS) offers serverless Kubernetes, a CI/CD experience, and enterprise-grade security and governance.

Kubernetes works with containerized applications. Containers are readily versioned and managed through development and deployment. By including the infrastructure configuration manifests in this management structure, it becomes easier to deploy to the correct infrastructure and have alternate infrastructure definitions available for different purposes. This process is the essence of how implements Infrastructure as Code (IaC) using Terraform templates. IaC is the process of managing and provisioning the technology stack for an application through version-controlled software, rather than using a manual process to configure discrete hardware devices and operating systems.

              Based on the selected configuration files, Terraform generates an execution plan describing what it will do to reach the desired deployment state and then executes the plan to build the described infrastructure. As the configuration changes, Terraform determines what changed and creates an incremental execution plan for applying changes. This ability makes Terraform highly suitable for supporting Kubernetes in a CI/CD process environment.
              
See logs in all the above three environments.

AWS Elastic Beanstalk provides two ways to regularly view logs from the Amazon EC2 instances that run your application:

Configure your Elastic Beanstalk environment to upload rotated instance logs to the environment's Amazon S3 bucket.

Configure the environment to stream instance logs to Amazon CloudWatch Logs.

When you configure instance log streaming to CloudWatch Logs, Elastic Beanstalk creates CloudWatch Logs log groups for proxy and deployment logs on the Amazon EC2 instances, and transfers these log files to CloudWatch Logs in real time. For more information about instance logs, see Viewing logs from Amazon EC2 instances in your Elastic Beanstalk environment.

If you enable enhanced health for your environment, you can configure the environment to stream health information to CloudWatch Logs. When the environment's health status changes, Elastic Beanstalk adds a record to a health log group, with the new status and a description of the cause of the change. For information about environment health streaming, see Streaming Elastic Beanstalk environment health information to Amazon CloudWatch Logs.

Plan to add alerts and monitoring:

You can create a CloudWatch alarm that monitors CloudWatch metrics for one of your instances. CloudWatch will automatically send you a notification when the metric reaches a threshold you specify. You can create a CloudWatch alarm using the Amazon EC2 console, or using the more advanced options provided by the CloudWatch console.

In the navigation pane, choose Instances.

Select the instance and choose Actions, Monitoring, Manage CloudWatch alarms.

On the Manage CloudWatch alarms detail page, under Add or edit alarm, select Create a new alarm.

For Alarm notification, choose whether to turn the toggle on or off to configure Amazon Simple Notification Service (Amazon SNS) notifications. Enter an existing Amazon SNS topic or enter a name to create a new topic.

For Alarm action, choose whether to turn the toggle on or off to specify an action to take when the alarm is triggered. Select an action from the dropdown.

