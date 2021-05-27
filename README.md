# CONTORL.AWS

## A command is worth a thousand API calls. 

Control your AWS cloud with a simple API that does all the undifferentiated heavy lifting for you. 

Instead of having to learn the arcane details of each of the hundreds of AWS services, Control helps you think in terms of Apps, Services, Tasks and Resources, conceptually similar to Heroku or other PaaS offerings. 

Run `control setup` to prepare your AWS account to host your apps & services. Internally, Control will configure a VPC, make private and public subnets in every availability zone, and set up the internet gateways, route tables and ACLs.

Run `control create app` to start a collection of Services and Tasks that make up a single App. You can think of each App as a combination of a container and a [Procfile](https://devcenter.heroku.com/articles/procfile) — a codebase, Sevices that work over HTTP, and Tasks that either run periodically on cron or 24/7. Internally, Control will set up an ECR repository, and configure your one or more of ECS, Fargate, App Runner, Cloud Map, HTTP Gateway, Lambda and ALB based on sensible defaults that you can override. All configurations are enabled for autoscaling, logging and metrics, with locked-down security groups. 

Run `control create database` to set up a database of your choice on RDS, with sensible defaults for backups, IOPS and locked-down security groups. 

Run `control attach databaseID ––to appID` to set up permissions for the app security group to reach the database security group, and add the `DATABASE_URL` environment variable to your application configuration. 

Run `control create topic` to create a messaging topic, which gives you a fully integrated SNS + SQS combo that allows you to process any volume of messages easily. Internally, You can then do `control attach topic --publisher publishingAppID` or `control attach topic --subscriber subscribingAppID` to add the SNS topic URL or SQS queue URL to the application, with the correct IAM permissions set to send or receive & delete messages. 

### Running

`control` works with great with AWS CloudShell, helping you control your apps and services from anywhere without having to manage credentials. It also runs fine on your local machine, using the AWS credentials configured according to the default conventions. 

### Scripting

All `control` commands support JSON output for easy scripting. 
