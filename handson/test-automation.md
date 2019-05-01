# Test Automation Hands On Lab

Use this lab time to create two types of test for the Demo Application 
## Part 1 Setup

1. Checkout the Lesson-1 Tag of the CICDDemoApp
0. Checkout a branch with the name "<<YourName>>-Unit-Test"


## Part 1 End to End test using Cypress

*N.B.  Use the following commands to setup your environment for writing cypress tests:*

```bash
docker-compose up -d express-api
vue-client/npm run test:e2e
```
*This will start up the back end server in detached mode and will start the cypress tests*

---

0. Add the Cypress Vue Cli dev dependency to the project using `npm i --save-dev @vue/cli-plugin-e2e-cypress`
0. Add the Cypress-Axe Dev dependency to the project  
   Use the instructions found here: https://www.npmjs.com/package/cypress-axe  
  *You will have to restart your cypress instance after this step*
0. Write a test that adds a task and validates that it gets added
0. Write a test that toggles the task you added in the previous step and validates that it gets toggled.
0. Add the following to the `scripts` section of the `vue-client/package.json` file.  
    `"test:e2e-cli": "vue-cli-service test:e2e --headless --url http://localhost:8080 --config video=false,chromeWebSecurity=false",`  
This will run the cypress tests in headless mode, it disables video, and disables the Cross-Origin-Resource-Sharing Check.  
0. Add the following Job to you azure-pipelines.yml file
  
```yaml 
  - job: integration_tests
    pool:
      vmImage: 'Ubuntu-16.04'
    dependsOn: 
      - build_containers
    steps:
      - task: DownloadPipelineArtifact@0
        inputs: 
          targetPath: .
          artifactName: images
      - script: docker load < docker-images.tar
        displayName: 'Loading Docker Images'
      - script: docker-compose up -d  express-api postgres-database vue-client
        displayName: 'Start Backend'
      - script: | 
          cd vue-client
          npm ci 
          npm run test:e2e-cli
        displayName: 'Run Test'
```

## Part 2 Unit Tests

0. Add Nock to your project as a dev tool 
    - `npm i --save-dev nock` 
0. Use nock and jest to write an automated unit test for the mounted method in the `home.vue` file. The test should do the following: 
   1. Setup the nock mock
   2. run the mounted method
   3. verify that the mocked tasks get added to the tasks property
0. Add unit test to vue-client docker build by adding the following line in the build stage after `npm ci` is run:
  `RUN npm run test:unit`

## Part 3 Finish up

0. Commit your changes
0. Push your branch up to GitHub
0. Open a Pull Request to kick off the build