# CI-CD-with-Azure-DevOps
Creating this repo to show how to create a Continuous Integration and Continuous Deployment pipeline using Azure DevOps to automate the delivery process of a Java Maven Application

The steps to accomplish this will involve moving our application code from the local dev environment ( such as VS Code or IntelliJ) to Azure Repos. Next, we will create a CI pipeline and generate artifacts to be used for the CD pipeline. Subsequently, we will publish the artifact in different environments such as Azure App Service with approval conditions implemented for illustration.

Below is how the target architecture will look like

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/9e9080b0-d9d8-4060-a174-33735c427b39)


## Step 1: 
Go to Azure DevOps organization and create a new project

![Image](https://github.com/users/kenchuks44/projects/4/assets/88329191/0a4129bd-4ccc-42cd-9cbd-86ab3d364f67)

![Image](https://github.com/users/kenchuks44/projects/4/assets/88329191/d0499add-96ed-434a-9a6e-f8debf1ca81c)

## Step 2: 
Next, we push existing project code on the local machine to Azure Repos by firstly, right clicking on the project folder on the local machine and selecting Git Bash and then running the following git commands below

```
```git init```
```git add .```
```git commit -m "file added"```
```git push <azure_repo_url>```
```
![Image](https://github.com/users/kenchuks44/projects/4/assets/88329191/6b7240d9-6003-404e-a19d-b83a9eb9e1da)

![Image](https://github.com/users/kenchuks44/projects/4/assets/88329191/637acedf-8943-45ef-9d0a-f3654f228ca6)

The application code will now be see in Azure Repos

![Image](https://github.com/users/kenchuks44/projects/4/assets/88329191/a1e8f1f2-8822-4b70-96ad-3cdb500a8bfb)

## Step 3: 
We create a new pipeline for the continuous integration

![Image](https://github.com/users/kenchuks44/projects/4/assets/88329191/aea863ed-9f1a-4477-9c64-0503e1aedbed)

## Step 4: 
Next, we select the source where our project code resides (here Azure Repos), the project and the repository

![Image](https://github.com/users/kenchuks44/projects/4/assets/88329191/16df0d68-5923-4b71-ae77-613dfc48a4d3)

## Step 5: 
As our test project is Java based, we need to install the build automation tool primarily for Java projects which is Maven

![Image](https://github.com/users/kenchuks44/projects/4/assets/88329191/50c9004e-193b-4a6c-bbcb-743ebed17826)

## Step 6: 
On the pipeline section, we choose the pipeline agent. The agent is the machine where the build is performed. It is the agent that runs the tasks and jobs defined in the pipeline. They can be WIndows-based or Linux-based machines. We have Microsoft hosted agents and self hosted agents. In this project, we will use Microsoft hosted agent which comes pre-configured and they are maintained and updated by Microsoft. Leave other settings as default, then click Save and Run

![Image](https://github.com/users/kenchuks44/projects/4/assets/88329191/547ad7dd-2d76-4853-b10d-0a5c3ab7fc8d)

![Image](https://github.com/users/kenchuks44/projects/4/assets/88329191/c6503df8-e6b4-40e8-bb9b-9ef4c76b541a)

## Step 7: 
The build process will start, at completion, an artifact will be generated to be used for Continuous Deployment pipeline

![Image](https://github.com/users/kenchuks44/projects/4/assets/88329191/fcebf581-9bbc-49bc-9567-f10e78b6829f)

![Image](https://github.com/users/kenchuks44/projects/4/assets/88329191/dc820b1b-b0c3-4071-be31-0fd38495b7c3)

![Image](https://github.com/users/kenchuks44/projects/4/assets/88329191/254ccedf-7b58-428b-a010-0b819938ed99)

## Step 8: 
We go to the pipeline section, click on the edit button, then on the Triggers tab, we select Enable Continuous Integration. This will ensure that whenever we make changes to the application code locally and push the code to the repository, a build will be triggered.

![Image](https://github.com/users/kenchuks44/projects/4/assets/88329191/982b344d-45dc-438a-af17-f4a8026b428c)

![Image](https://github.com/users/kenchuks44/projects/4/assets/88329191/e3d5a90c-a5c2-4062-9679-803e61a3e581)

![Image](https://github.com/users/kenchuks44/projects/4/assets/88329191/52afc7e7-d332-4c43-8112-d69a75f20f4d)

![Image](https://github.com/users/kenchuks44/projects/4/assets/88329191/395deb7b-ba04-4ecf-8edf-e8ffd19a1f76)

## Step 9: 
We can observe the job running till completion and an artifact is then generated.

![Image](https://github.com/users/kenchuks44/projects/4/assets/88329191/a6181bae-a496-4e6b-b6c6-2ae71cfdce8a)

![Image](https://github.com/users/kenchuks44/projects/4/assets/88329191/f937ce25-89b3-44aa-bd8e-3bc439430516)

## Step 10: For the Continuous Delivery pipeline:
Here, we are deploying to Azure App Service Web App. To do this, we will first create a service connection to authenticate to the Azure subscription on Azure DevOps. For the service connection authentication, a service principal was used. 

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/c743f6a1-8412-4638-8311-0b479cd38cf5)

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/24bfd32f-8dd3-4cbb-9347-e32dfae99712)

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/dc71ffe3-9602-4ff4-8407-9f441b922f38)

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/f4bab06c-0c85-40f5-bd23-ff7bee1def0a)

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/d3921f62-0be6-4f10-ba1d-edb16c0153df)

Then, on the Azure portal, through the Microsoft Entra ID, we registered the application (take note of the app ID). Next, we created a client secret (copied and kept in a safe location). Next, we grant permissions to the service principal to read information on the Azure subscription. To achieve this, we create a reader role assignment and assign it to the service principal.

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/5ba9daae-dd8b-4fd7-9851-42063792c25d)

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/9b2a676c-11e5-4ac1-8dad-3bfc1b70bcee)

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/be934b46-d315-41d7-94b8-18e28bd93399)

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/a5aa97a9-8b45-449f-aed7-3ad413072587)

Then, finally setup the service connection

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/a64651d2-fcdb-4594-869b-01583ae2ce02)

## Step 11: 
Creating a release pipeline: A release pipeline enables us to automate the deployment and delivery of the java maven app to various stages and environments such as Development, QA and Production environments.

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/070fbada-4b1e-4aea-8d22-a4d16d144b06)

On creating the release pipeline, we select Azure App Service deployment as we are deploying the app to Azure Web App. Next, we select build and the source of our build is the artifact previously generated.

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/993d22d5-a92c-40ea-a188-d75ae9b394ae)

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/94ff6d79-5f3c-4c9a-a384-b6cfde0bdbbf)

Next, we add a stage to the pipeline, define the build job to be executed and then manually trigger the pipeline using Microsoft hosted agent.

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/73c6cc2f-428f-471b-a6b2-c883c479b68c)

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/ecd42ad8-68f5-40bd-802a-135a2a2e1845)

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/e1bbe9a9-5e8f-4707-8bcb-23f2b602999f)

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/43a5fd8a-3449-4736-a318-cb429b9fc5b6)

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/dc2e1925-d77a-4f07-af5f-0d7fe17ecd0f)

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/73bc8f70-3bf9-475a-8ea9-f3871ab7fa51)

Once completed, go to the Azure Web App on the Azure portal and click on the domain URL and the website will be displayed in the browser.

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/cc3c5f4a-45bd-494c-a4ce-43addbc426e5)

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/5fe7357f-53f5-4c01-94c4-e23f47ec670a)

## Step 12: 
Continuous deployment/delivery: To standardize and streamline our release pipeline, we will enable continuous deployment to increase efficiency and minimize the possibilities of human error. Also, for stages like production, it is often recommended to enable a manual trigger with a pre-deployment condition to ensure the right individuals deploys to that environment.

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/493f66dd-ea64-4f08-b851-7ba7cb428e82)

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/358ad467-58ae-4311-a642-df7f5a529ef0)

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/1d0113ea-369f-44eb-8a21-11b6bda8d20f)

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/4bbaafc3-8b34-4af4-9c4c-f06f83e4e1b1)

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/0e490bec-278e-4619-ae86-c690d4255e82)

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/3bf5becd-51d7-4882-8384-93b4c8133a8a)

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/ff7de415-7f20-4af4-8421-24541c079415)

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/586aad1a-535c-407d-9417-25350c727534)


































