# Introduction to Pipelines in Azure DevOps

---

## Why Azure Devops?

ESDC has bought Azure Space and it's what I have access to

------

Here's a secret

Note: CI Pipelines are Commodified. They all do the same thing. Run Commands on a computer somewhere.

------

Use a CI Tool that you have access to.
For instance most major CSPs we can procure have them.

- **Azure** Azure DevOps Pipelines
- **AWS** CodePipeline
- **GCP** Cloud Build

Note: CSP = Cloud Service Provider


------

There are also lots of other good options. 

- drone.io
- Circle CI
- Travis
- Concourse
- Spinnaker
- Gitlab CI

Note: Some of these are SaaS, some self-hosted, some both. Most of these provide free build time for Open Source Projects

------

Just don't use Jenkins unless you have to. 

Note: It's better then nothing. Jenkensteins make for brittle configuration management.

---

Yaml Files

Note: This is the recommended way to 

---

Pipelines


------

If you have a single stage, you can omit stages and directly specify jobs:

------

If you have a single stage and a single job, you can omit those keywords and directly specify steps:

---

Stages  

A stage is a collection of related jobs. By default, stages run sequentially, starting only after the stage ahead of them has completed.

---

Jobs  

A job is a collection of steps to be run by an agent or, in some cases, on the server. Jobs can be run conditionally, and they may depend on earlier jobs.


------

Container Reference  

Docker hub

```yaml
container: string # Docker Hub image reference or resource alias
```

Other Container Registries

```yaml
container:
  image: string  # container image name
  options: string  # arguments to pass to container at startup
  endpoint: string  # endpoint for a private container registry
  env: { string: string }  # list of environment variables to add
```


------

Strategies

`matrix` and `parallel` are mutually-exclusive strategies for duplicating a job.


------

Matrix  
Matrixing generates copies of a job with different inputs. This is useful for testing against different configurations or platform versions.

------

Parallel  
This specifies how many duplicates of the job should run. This is useful for slicing up a large test matrix. The VS Test task understands how to divide the test load across the number of jobs scheduled.


------

Maximum Parallelism  
Regardless of which strategy is chosen and how many jobs are generated, this value specifies the maximum number of agents which will run at a time for this family of jobs.

If not specified or set to 0, no limit will be applied.

---

Steps

Steps are a linear sequence of operations that make up a job. Each step runs in its own process on an agent and has access to the pipeline workspace on disk. This means environment variables are not preserved between steps but filesystem changes are.

------

Schema 

```yaml
steps: [ script | bash | pwsh | powershell | checkout | task | templateReference ]
```

---

Variables

Hardcoded values can be added directly, or variable groups can be referenced. Variables may be specified at the pipeline, stage, or job level.

------

Secret Variables

These should never be added to your azure-pipelines.yml file and should be either pulled in from a secret management tool at build time or entered into the web portal.

---

Templates

You can export reusable sections of your pipeline to a separate file. These separate files are known as templates. Azure Pipelines supports four kinds of templates:

- Stage
- Job
- Step
- Variable

------

Templates may themselves include other templates. Azure Pipelines supports a maximum of 50 unique template files in a single pipeline.

---

Resources

------

Container resource  
Container jobs let you isolate your tools and dependencies inside a container. The agent will launch an instance of your specified container, then run steps inside it. The container resource lets you specify your container images.

Service containers run alongside a job to provide various dependencies such as databases.

------


Repository resource  
If your pipeline has templates in another repository, you must let the system know about that repository. The repository resource lets you specify an external repository.

------

Type  
Pipelines support two types of repositories, git and github. git refers to Azure Repos Git repos. If you choose git as your type, then name refers to another repository in the same project. For example, otherRepo. To refer to a repo in another project within the same organization, prefix the name with that project's name. For example, OtherProject/otherRepo.

If you choose github as your type, then name is the full name of the GitHub repo including the user or organization. For example, Microsoft/vscode. Also, GitHub repos require a service connection for authorization.

---

Triggers

Push Trigger   
PR Trigger

---

Tasks

------

Pre-defined actions created by Microsoft

*This makes your pipeline less portable*

------

*But also can make your life much easier*

Note: Realistically how often are you going to migrate to another CSP?

---

References
- https://docs.microsoft.com/en-us/azure/devops/pipelines/?view=azure-devops
