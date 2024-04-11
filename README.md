# README V1.1 #

This README would normally document whatever steps are necessary to get your application up and running.

### What is this repository for? ###
This is a repository to showcase major DevOps functionality with Atlassian products, the major goal is utilize CI/CD pipelines from Bitbucket to show our customers,
how easy it is to configure and maintain CI/CD with Bitbucket, but also show daily activities of a Developer, Engineer, Eeam Lead and/or Release Manager working 
with Atlassian Eco-System.

* Understand and Configuring CI/CD with Bitbucket
* Integrating Bitbucket with JSW and Slack 
* Executing Branch and Code Commit
* This Pipeline is integrated with JSW and Slack, in this section you will learn how to configure these steps.

For more information please visit [_JSW + Bitbucket_](https://www.atlassian.com/software/jira/bitbucket-integration).

### How do I get set up? ###

#### Step 1: Fork this repository:

Pls do not use this repository, fork before you use it.
More details in the [_How to fork a repository guide_](https://confluence.atlassian.com/bitbucket/forking-a-repository-221449527.html).

Make sure to change the first part of the repository name to match your Workspace ID. This is important for later steps in the demo, where you will publish a static website on Bitbucket Cloud, and this is done by combining your workspace ID with the bitbucket.io domain suffix as your repository name.

For example, if your workspace name is “my-demo-workspace”, the new repository name should be “my-demo-workspace.bitbucket.io”. 

#### Step 2: Enable your Pipeline:

* Go to Repository Settings "left panel"
* Scroll-down, Pipelines section and click in Settings
* Turn-on the toggle "Enable Pipeline"
* Go back to your Repository, select Pipelines "left pane" and click "Run initial pipeline" (most likely, it will fail, however, this is expected, you can continue with the next steps)

#### Step 3: Integrate your repository with JSW:

Please follow the steps in this document to integrate JSW with Bitbucket

* Click in “Jira Issues” in the left panel
* In the “Connect to Jira Cloud” screen, click on “Open settings”
* Select the cloud site that you want to connect to and click “Grant access” on both sides (Bitbucket Cloud and Jira Software)
* When clicking again “Jira Issues” in Bitbucket Cloud, issues of your project will appear in Bitbucket Jira Issues.

#### Step 4: Preparing your Pipeline

In order to run your CI/CD Demo, you will need to configure some variables in your Pipeline, this will contain informations about your JSW and Slack channel of your choice to run the demo.

* Go back to Repository Settings / Pipelines and open Settings.
* Click in the section "View bitbucket-pipeline.yml"
* What you see is the yml file of your pipeline, click in Edit. 

This Pipeline has 2 Steps that require your attention and configuration;

 * atlassian/jira-transition:0.2.4
 * atlassian/slack-notify:2.0.0

### atlassian/jira-transition:0.2.4 Jira Ticket Transition:

 This step will set the Jira ticket status to In-Progress, this is something you can change if you want to use a different status, just remember that, this status must be availible in your JSW Project.

 Under "atlassian/jira-transition:0.2.4" you will see 3 Variables that need be configured before you run your pipeline.

* Your Jira Cloud URL, such as “https://acme.atlassian.net/jira”
* Email of your Atlassian Account
* Your personal API token (https://id.atlassian.com/manage-profile/security/api-tokens)

 **These Variables need to be created under each one of the environments and also at the repository level.

 In the right-side you will see the Pipeline Configuration Panel, you will need to add these variables and values.

### atlassian/slack-notify:2.0.0 Slack Notification:

 This step will notify Slack Channel that your build is now in Staging Environment, Slack msgs are often used during development phases, there is also an interactive trigger that can be used by Bots in Slack, for now we will only use this as notification.

 PRETEXT and MESSAGE can be changes to whatever you want, just remember to add the msg in between ""

 This section also need be configured, the difference here is that we are not using variables, instead we are adding the value directly into the pipeline, this is just to show that you can do that, but in the normal use and daily tasks we always recommend to use variables.

 You will need to change the WEBHOOK_URL: adding the URL Hook of your Slack channel, here is the steps you need execute to create your slack channel and get your [_URL Hook_](https://api.slack.com/messaging/webhooks). 


### Running your Pipeline ###

 After finish your pipeline configuration you will need to Commit the file that you just changed, please click in Commit, “…in the pop-up window, add a message that reference one of the Jira Issue Keys and explains the changes you just did, for example: "MOBL-8: CI/CD Pipeline pre-configuration"

