# Intro to Azure DevOps Pipeline Hands On Lab.
 In this lab you will create a project in GitHub connect it to an Azure Pipeline this pipeline and repo will be used in subsequent labs.
 
1. Create an account with Azure DevOps, you should be able to use the account you created for the 2 day Azure course. 
   - https://devops.azure.com 
2. Fork the following repo to your personal GitHub account: <<TODO: Add initial repo here>>  
   Instructions can be found here: https://help.github.com/en/articles/fork-a-repo 
3. Create a azure-pipeline.yml file that runs `docker-compose build` 
4. Save the following docker images built from the previous command in the `publish` folder (_Hint you'll have to create that folder first_).
    - `express-api:latest` 
    - `vue-client:latest`   
Instructions can be found here: https://docs.docker.com/engine/reference/commandline/save/
0. Publish the tar file you just created to the pipeline using the **artifactName** `images`, and the **targetPath** `./publish`
   Instructions can be found here: https://docs.microsoft.com/en-us/azure/devops/pipelines/tasks/utility/publish-pipeline-artifact?view=azure-devops
0. 