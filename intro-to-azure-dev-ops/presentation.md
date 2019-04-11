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

## Schema

```yaml
name: string  # build numbering format
resources:
  containers: [ containerResource ]
  repositories: [ repositoryResource ]
variables: { string: string } | [ variable | templateReference ]
trigger: trigger
pr: pr
stages: [ stage | templateReference ]
```

------

If you have a single stage, you can omit stages and directly specify jobs:

```yaml
# ... other pipeline-level keywords
jobs: [ job | templateReference ]
```

------

If you have a single stage and a single job, you can omit those keywords and directly specify steps:


```yaml
# ... other pipeline-level keywords
steps: [ script | bash | pwsh | powershell | checkout | task | templateReference ]
```

---

Stages  

A stage is a collection of related jobs. By default, stages run sequentially, starting only after the stage ahead of them has completed.

------

Schema

```yaml
stages:
- stage: string  # name of the stage, A-Z, a-z, 0-9, and underscore
  displayName: string  # friendly name to display in the UI
  dependsOn: string | [ string ]
  condition: string
  variables: { string: string } | [ variable | variableReference ] 
  jobs: [ job | templateReference]
```

---

Jobs  

A job is a collection of steps to be run by an agent or, in some cases, on the server. Jobs can be run conditionally, and they may depend on earlier jobs.

------

Schema

```yaml
jobs:
- job: string  # name of the job, A-Z, a-z, 0-9, and underscore
  displayName: string  # friendly name to display in the UI
  dependsOn: string | [ string ]
  condition: string
  strategy:
    matrix: # matrix strategy, see below
    parallel: # parallel strategy, see below
    maxParallel: number # maximum number of agents to simultaneously run copies of this job on
  continueOnError: boolean  # 'true' if future jobs should run even if this job fails; defaults to 'false'
  pool: pool # see pool schema
  workspace:
    clean: outputs | resources | all # what to clean up before the job runs
  container: containerReference # container to run this job inside
  timeoutInMinutes: number # how long to run the job before automatically cancelling
  cancelTimeoutInMinutes: number # how much time to give 'run always even if cancelled tasks' before killing them
  variables: { string: string } | [ variable | variableReference ] 
  steps: [ script | bash | pwsh | powershell | checkout | task | templateReference ]
  services: { string: string | container } # container resources to run as a service container
  
```

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

For a simple set of hardcoded variables:
```yaml
variables: { string: string }
```

To include variable groups, switch to this list syntax:

```yaml
variables:
- name: string # name of a variable
  value: any # value of the variable
- group: string # name of a variable group

```

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

Schema 

```yaml
resources:
  repositories:
  - repository: string  # identifier (A-Z, a-z, 0-9, and underscore)
    type: enum  # see below
    name: string  # repository name (format depends on `type`)
    ref: string  # ref name to use, defaults to 'refs/heads/master'
    endpoint: string  # name of the service connection to use (for non-Azure Repos types)
```

------


Repository resource
If your pipeline has templates in another repository, you must let the system know about that repository. The repository resource lets you specify an external repository.


------

Schema 
```yaml
resources:
  repositories:
  - repository: string  # identifier (A-Z, a-z, 0-9, and underscore)
    type: enum  # see below
    name: string  # repository name (format depends on `type`)
    ref: string  # ref name to use, defaults to 'refs/heads/master'
    endpoint: string  # name of the service connection to use (for non-Azure Repos types)
```

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

