# Intro to Azure DevOps Pipeline Hands On Lab.
 In this lab you will create a project in GitHub connect it to an Azure Pipeline this pipeline and repo will be used in subsequent labs.


## Part 1 Creating a Pipeline 

0. Fork the following repo to your personal GitHub account: https://github.com/csps-efpc-daan-students-etudiants/intro-to-azure-devops-handson 
0. Create an account with Azure DevOps, you should be able to use the account you created for the 2 day Azure course. 
   - https://devops.azure.com 
0. Create a new organization give it whatever name you want _Note: must be globally unique_
0. Create a new Public Project, again give it whatever name you want.
0. Create a new build pipeline, and select GitHub.
0. Authorize Azure DevOps on your GitHub account, follow the instructions for following a GitHub App
    - https://docs.microsoft.com/en-us/azure/devops/pipelines/repos/github?view=azure-devops#authorize-access-to-your-repositories
   Instructions can be found here: https://help.github.com/en/articles/fork-a-repo 
0. Select an empty yaml, then save and run it.
   This will automatically save the file and commit it to your master branch, so make sure you `pull` down that file.
   
   
## Part 2 Building and publishing artifacts on the Pipeline

0. Modify the yaml file so that it runs `docker-compose build` 
0. Save the following docker images built from the previous command in the `publish` folder (_Hint you'll have to create that folder first_).
    - `express-api:latest` 
    - `vue-client:latest`   
Instructions can be found here: https://docs.docker.com/engine/reference/commandline/save/
0. Publish the tar file you just created to the pipeline using the **artifactName** `images`, and the **targetPath** `./publish`
   Instructions can be found here: https://docs.microsoft.com/en-us/azure/devops/pipelines/tasks/utility/publish-pipeline-artifact?view=azure-devops
0. Move the steps you just created into a job.
    - https://docs.microsoft.com/en-us/azure/devops/pipelines/process/phases?view=azure-devops&tabs=yaml  
  *You can copy the following template*

```yml

trigger:
- master

jobs: 
  - job: build_containers
    pool:
      vmImage: 'Ubuntu-16.04'
    steps:
    - script: echo "I do nothing!"
    #Build and publish steps go here
  - job: integration_tests
    pool:
      vmImage: 'Ubuntu-16.04'
    dependsOn: 
      - build_containers
    steps:
    - script: echo "Well okay I don't do nothing but whatever!"
    # Download steps go here
```

## Part 3 Downloading Artifacts and loading them on the pipelien

0. Download the artifact you published in the last part from the pipeline using the artifactName 
    - Instructions can be found here: https://docs.microsoft.com/en-us/azure/devops/pipelines/tasks/utility/download-pipeline-artifact?view=azure-devops
0. Load the file you just downloaded from the pipeline.
    - Instructions can be found here: https://docs.docker.com/engine/reference/commandline/load/ 
0. Start your application in detached mode `docker-compose up -d` to ensure everything worked.