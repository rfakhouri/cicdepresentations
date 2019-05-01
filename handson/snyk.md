# Snyk Vulnerability Scanning Hands On

In this hands on activity we are going to integrate Snyk vulnerability scanning into our build pipeline.

0. Use your GitHub account to create an account on Snyk.io
0. Install Snyk.io globally on your local machine `npm install -g snyk`
0. Navigate to the Vue-Client folder and run `snyk auth` to login and then `snyk test` to scan your repo. 
0. Add a job into your build pipeline to scan for vulnerabilities, this job does not need the app to be built to run.
0. Add a secret variable to your build pipeline to store your Snyk Authentication token
    - https://snyk.io/docs/cli-authentication/
0. Install snyk on the pipeline.
0. Run `snyk test` in `vue-client` and `express-api`. 
0. Run the test.
0. Ignore the issue that are found by adding them to your build script
    - https://snyk.io/docs/cli-ignore/
    - _please note at the moment there is a bit of a bug in this hands on so we'll just remove the test for now. :(_
0. Run your test again

```
  - job: scan_secrets
    pool:
      vmImage: 'Ubuntu-16.04'
    steps:
    - script: echo "I do nothing"


```