# Continuous Integration, Development and Deployment

## Types

### Self-Hosted

- Runs on your hardware
- Could run in a data center, VM in a corporate cloud, or workstation
- Administrator is responsible for mantaining the tool

| Pros         | Cons         |
| ------------ | ------------ |
| Maximum flexibility | Difficult installation and maintenance |
| Data Control | Bounded scale (i.e. you have to administer everything) |
| | Getting started |


### Software as a Service (SaaS)

**Vendor**

- provides the tool
- maintains the tool
- Users have simple access

| Pros | Cons |
| ------------ | ------------ |
| Easy to get started | High cost at scale |
| Free options | Security concerns |
| Automatic triggers | |

### Cloud Service Providers

Offer

- SaaS-based tools
- Additional services such as VMs, container registries, and storage

| Pros | Cons |
| ------------ | ------------ |
| Easy integration with other services | Vendor lock-in |
| Identity and access management | |
| Unbounded scale | |

### Code Repositories

- Store code
- CI/CD solutions

| Pros | Cons |
| ------------ | ------------ |
| Repo and CI/CD in one tool | High cost at scale |
| Custom docker containers | |
| Free options | |

## Pipelines

### Typical Pipeline

| Git Push
| ---

| Requirements & Sanity Check
| ---

| Build
| ---

| Deploy & Test staging
| ---

| Deploy and Test Production
| ---

### Things to keep in mind

- pipelines are no good without as tests
- The pipelines can be though of as **stages** (sometimes called *Actions*) (e.g. build, staging, production) which contain **jobs** (e.g. test, deploy) which contain **tasks/commands** (e.g. ```pip install flask```)
- pipelines are configured from a config file in the root of the repo or through the service's web UI
- pipelines are run manually or on code commits to branches, or master depending on the CI/CD and setup
- Using CI/CD from a company where you are using their Cloud Services makes a lot of sense
- running multiple commands per step can help to decrease build time
- caching can be used in some formates to decrease build time

## Products

### [Jenkins](https://jenkins.io/)

##### **requires Java Runtime Environment**

- An **automation framework** that can be extended through plugins
- Checkout [Blue Ocean plugin](https://jenkins.io/doc/book/blueocean/) for pipeline UI
- Configurable in web UI or a **Jenkinfile** based on the [Groovy language](https://groovy-lang.org/documentation.html)

### [Bamboo]()

- Tight integration with other **Atlassian** products such as *Bitbucket*
- Configurable in web UI or a **YAML** or **Java** file

### [TeamCity]()

- Tight integration with **JetBrains IDEs** and **Visual Studio**
- Can automatically configure jobs based on project code
- Configured in web UI or **XML** or **Kotlin**

### [GoCD]()

- Focuses on using pipelines
- Pipelines are made of stages, jobs, and tasks
- Configured from the web UI or **XML** and plugins for working in **JSON** or **YAML**
- Shared commands are found in the Go Command Repo

### [Travic CI]()

- Go to choice for open source projects
- **ONLY works with projects on Github**
- Free builds for open-source projects
- Configured in a hidden file named ```.travis.yml```
- Many third-party applications, clients, tools, and libraries
- Can add a build status icon and list in ```README.md```

### [CodeShip]()

- Can connect to repos in Bitbucket, Github, or Gitlab
- Has Basic and Pro version
- Pro comes with dedicated VMs, docker support, and customization in **YAML** files

### [CircleCI]()

- Uses docker containers for running jobs
- Works through docker images in Ubuntu, Windows, and MacOS X
- Paid plans required for MacOS
- Configured in ```.circleci/config.yml```
- *Orbs* are shareable packages of CircleCI configurations
- Offers command-line tool for development

### AWS [CodePipeline]() and [CodeBuild]()

- Takes input for GitHub, AWS CodeCommit, AWS S3, or Amazon ECR
- Works with Linux, Windows, and MacOS X
- Each stage calls on an action provider (i.e. an **AWS Service**, third-party actions, or custom builds)
- **CodeBuild** is configured through ```buildspec.yml``` which specifies artifcats and where to store them. The build environment is a *Docker* container
- CodePipeline is Free for the first 30 days and then 1$/month per pipeline
- CodeBuild is free fro 100 minutes/month on the smallest instance
- **MASSIVE** customization

### [Azure Pipelines]()

- Access to other resources in Azure, can deploy to other resources on Azure
- Open-source projects have unlimited build time and 10 parallel job times
- Custom agents and tasks are open source and customizable on GitHub
- Works with Linux, Windows, and MacOS X
- Configurable in ```azure-pipelines.yml```

### [CloudBuild]() (previously Container Build)

- can access other Google Cloud Platform services
- First 120 builds-minutes per day are free
- Triggered when new commit is pushed to repo from Code Repository: GitHub, Bit Bucket, or GCP's Cloud Source Repository
- Can be configured to work on specific branches or tags
- Configurable through ```cloudbuild.yaml``` or ```cloudbuild.json```
- For projects that only need a container image the build file can be ommited and a **Dockerfile** can be used instead

### [GitHub Actions]()

- Best git source management
- Free unlimited public and private repositories
- Up to three people on a private free repo
- Configurable in ```.github/main.workflow```
- Commands run in containers called *Actions*
- Features and custom Actions
- Limited to 58 minutes of execution and 100 Actions
- Clicking into the ```main.workflow``` gives a graphical view of the **Pipeline**

### [GitLab]()

- Open source product
- Container registery
- Free unlimited public and private repositories
- Configurable through ```.gitlab-ci.yml```

### [BitBucket Pipelines]()

- Source code management for **Git** and **Mercurial**
- Jira and Trello Integration
- Unlimited private repos for small teams
- Configurable through ```bitbucket-pipelines.yml```
- Commands are run in containers
- Fifty build minutes per month for free