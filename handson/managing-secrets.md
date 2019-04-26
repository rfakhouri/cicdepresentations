# Managing Secrets Hands On Lab

In this lab you will see how easy it is to find secrets in a project in GitHub

## Scanning for secrets in GitHub

0. Download GitRob from the GitRob GitHub site
0. Create a GitHub Personal Access Token instructions are here: https://help.github.com/en/articles/creating-a-personal-access-token-for-the-command-line
0. Add that Personal Access Token to your environment variables
   - Linux/MacOS users can follow the instructions on the GitRob GitHub site. 
   - Windows user can follow the instructions here: https://superuser.com/questions/949560/how-do-i-set-system-environment-variables-in-windows-10
0. Run GitRob against the following organization `cds-snc`
0. Play around with the results that are found

## Protecting from secrets

0. Add a new Job to your `azure-pipelines.yml` file. You can use the following yml fragment.  
   _Note: This doesn't require a built container so can run parallel with the build job_  
0. Add either dxa4481/truffleHog or yelp/detect-secrets to your `azure-pipelines.yml` file, or both.
    - `pip install truffleHog`
    - `pip install detect-secrets`
0. Scan the project during the build pipeline.
0. Review the results on your Pull Request and tune the scan to ignore any false-positives.
0. Try to commit a file with a secret to your repo and perform a Pull Request


_You can use the following fragment for your new job_
```yml

  - job: Scan Secrets
    pool:
      vmImage: 'Ubuntu-16.04'
    steps:
    #Install and scan steps go here
```  