# CI-CD-with-Azure-DevOps
Creating this project to show how to setup a Continuous Integration and Continuous Deployment pipeline using Azure DevOps to automate the delivery process of a Java Maven Application

The steps to accomplish this will involve moving our application code from the local dev environment ( such as VS Code or IntelliJ) to Azure Repos. Next, we will create a CI pipeline and generate artifacts to be used for the CD pipeline. Subsequently, we will publish the artifact in different environments such as Azure App Service with approval conditions implemented for illustration.

Below is how the target architecture will look like

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/9e9080b0-d9d8-4060-a174-33735c427b39)


## Step 1: 
Go to Azure DevOps organization and create a new project

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/7dcdc08a-b857-40b6-9219-51747c87e441)


![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/8e714bcb-e482-4b9e-a5db-b0b45811dd81)


## Step 2: 
Next, we push existing project code on the local machine to Azure Repos by firstly, right clicking on the project folder on the local machine and selecting Git Bash and then running the following git commands below

```
git init
git add .
git commit -m "file added"
git push <azure_repo_url>
```

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/724e3a2b-b4f5-489c-adb3-659c068b8e8f)


The application code will now be see in Azure Repos

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/c77bde30-38cd-43db-9def-3d14a92ee541)


## Step 3: 
We create a new pipeline for the continuous integration

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/28f1b2c6-04d4-4af7-ae74-d65cbef5859a)


## Step 4: 
Next, we select the source where our project code resides (here Azure Repos), the project and the repository

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/ead0b523-ca35-4207-a719-b1d2687081ea)


## Step 5: 
As our test project is Java based, we need to install the build automation tool primarily for Java projects which is Maven

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/93148353-15bf-499f-b319-337e52028f22)


## Step 6: 
On the pipeline section, we choose the pipeline agent. The agent is the machine where the build is performed. It is the agent that runs the tasks and jobs defined in the pipeline. They can be WIndows-based or Linux-based machines. We have Microsoft hosted agents and self hosted agents. In this project, we will use Microsoft hosted agent which comes pre-configured and they are maintained and updated by Microsoft. Leave other settings as default, then click Save and Run

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/0abcb958-cd16-4a94-997b-74be9c84d6f4)


![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/b0a76656-994e-48f4-88fb-41ac5c6ea49f)


## Step 7: 
The build process will start, at completion, an artifact will be generated to be used for Continuous Deployment pipeline

![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/43cd396f-266e-413c-af74-cf3f7a83daea)


![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/666f50d6-4428-4079-93b9-aac81983bc2f)


![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/8c8a2616-c30a-493c-ad48-f17b5bbe6f63)


## Step 8: 
We go to the pipeline section, click on the edit button, then on the Triggers tab, we select Enable Continuous Integration. This will ensure that whenever we make changes to the application code locally and push the code to the repository, a build will be triggered.

![Screenshot (54)](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/a1e30df3-8f89-43ca-80e6-34faa9a5c874)



![Screenshot (55)](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/708b3dc0-ff58-406b-8f89-7eae1ffb0a01)



![image](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/aced5202-96a6-42e9-80c4-d25e2ac04c1c)


![Screenshot (59)](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/3299caa0-ad07-41b8-b41e-07b40fd6d33b)



## Step 9: 
We can observe the job running till completion and an artifact is then generated.

![Screenshot (60)](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/f9d33c5e-0639-47cc-9dc1-34441cb874d1)



![Screenshot (61)](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/e16ecba8-015f-4529-a906-60c396f251e4)



## Step 10: For the Continuous Delivery pipeline:
Here, we are deploying to Azure App Service Web App. To do this, we will first create a service connection to authenticate to the Azure subscription on Azure DevOps. For the service connection authentication, a service principal was used. 

![Screenshot (67)](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/757ed17f-59a4-4d56-9acc-4e10e63e5e45)

![Screenshot (69)](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/c1ce0be5-bfaf-47a9-9f52-063f9d650f98)

![Screenshot (63)](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/b167bfa5-3bda-422f-a72f-97be61668be6)


Then, on the Azure portal, through the Microsoft Entra ID, we registered the application (take note of the app ID). Next, we created a client secret (copied and kept in a safe location). Next, we grant permissions to the service principal to read information on the Azure subscription. To achieve this, we create a reader role assignment and assign it to the service principal.

![Screenshot (70)](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/5f573b4e-b9fe-4d19-9388-74ecb6c72f8a)


![Screenshot (72)](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/2c1c0142-c307-4db3-9324-6e92bb2b85d6)


![Screenshot (73)](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/3c83fed8-774e-4cab-9f97-78822fcc582b)


Then, finally setup the service connection

![Screenshot (74)](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/23a6b99c-945b-48c1-9f87-6ade67f04fee)


## Step 11: 
Creating a release pipeline: A release pipeline enables us to automate the deployment and delivery of the java maven app to various stages and environments such as Development, QA and Production environments.

![Screenshot (75)](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/ccb3e36b-4d31-4838-bb8e-e815ddd691fc)


On creating the release pipeline, we select Azure App Service deployment as we are deploying the app to Azure Web App. Next, we select build and the source of our build is the artifact previously generated.

![Screenshot (76)](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/58d6ac58-3bad-4699-ae88-186a8f39927e)


![Screenshot (77)](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/db11bcaf-cb3c-43b0-aead-e8993957dc4d)


Next, we add a stage to the pipeline, define the build job to be executed and then manually trigger the pipeline using Microsoft hosted agent.

![Screenshot (78)](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/d3387dac-a00e-40f0-a9dd-d82eb1de0d48)


![Screenshot (79)](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/23adf639-6d0f-4ecb-a711-5b4a06888c8c)


![Screenshot (82)](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/b5ef6762-690f-43f9-b107-eef578baa940)


![Screenshot (80)](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/387adee3-f5db-4043-8950-6d6214b26e3b)


![Screenshot (81)](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/37de18b8-c0bc-4833-be79-53ab79811f3f)


![Screenshot (88)](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/6e2cc244-e3c9-4da8-bd80-5ac71d5a3d14)


Once completed, go to the Azure Web App on the Azure portal and click on the domain URL and the website will be displayed in the browser.

![Screenshot (92)](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/36beaa4d-b6e0-42ba-9eb3-1534a3784338)


## Step 12: 
Continuous deployment/delivery: To standardize and streamline our release pipeline, we will enable continuous deployment to increase efficiency and minimize the possibilities of human error. Also, for stages like production, it is often recommended to enable a manual trigger with a pre-deployment condition to ensure the right individuals deploys to that environment.

![Screenshot (90)](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/2b40003d-9d39-4788-a4fa-6e8ad5a930c7)


![Screenshot (89)](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/b89f673f-ad2d-498f-a14f-d6bbcad47994)


![Screenshot (94)](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/3985d6c6-c4ef-4121-a627-7239d211ae1e)


![Screenshot (95)](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/907cc1c7-813a-46a2-a145-879610cea34f)


![Screenshot (93)](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/16dba4e7-bec8-4245-b0c1-92f6bc13bb73)


![Screenshot (91)](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/0ad4f5a5-970f-4df5-a218-82c244699f46)


![Screenshot (134)](https://github.com/kenchuks44/CI-CD-with-Azure-DevOps/assets/88329191/691fb8f4-f961-4dc3-87dd-c4251a8aca9e)





































