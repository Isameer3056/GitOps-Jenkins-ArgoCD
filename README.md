<<<<<<< HEAD
### GitLab YAML Pipeline Tutorial for Beginners. Setup Multi Stage/Job CI/CD Pipeline.
## Introduction
In this small project, we will learn basic of GitLab YAML pipeline and further we will setup the CI/CD.

Demo Use Case

    Setup Multi Stage/Multi Job Pipeline

    Setup Pipeline with variables

    Build Visual Studio Project 

## What is YAML?
YAML is a human-readable data-serialization language and it helps to configure pipeline as a Code.

Indentation is very important in YAML.

## GitLab YAML Pipeline
In GitLab, YAML Pipelines helps to setup Continuous Integration/ Continuous Deployment (CI/CD).


## GitLab YAML Pipeline Structure

## Hierarchy of YAML Pipeline File
```
stages:    
  - build
  - test
  - deploy

build-job:     
  stage: build
  tags:
    - "windows"
  script:
    -  write-host "I am in Build Stage"
test-job:      
  stage: test
  tags:
    - "windows"
  script:
    -  write-host "I am in Test Stage"
deploy-job: 
  stage: deploy
  tags:
    - "windows"
  script:
    -  write-host "I am in Deploy Stage"
```


## Component of GitLab YAML Pipeline


## workflow
Workflow helps to control when and what pipeline to run.
```markdown
var first = 1;
var second = 2;
var sum = first + second;
workflow:
    rules:
        - if: $CI_COMMIT_BRANCH == "master"
          changes:
            - <Project Path>
```


## variables
Here we can define all the variables which can be used during the job execution.
```
variables:
   BUILD_PROJECT:"https://example.com/"
   BUILD_SITE:"https://example.com/"
   MSBUILD_PATH:'<Path>\v4.0.30319\MSBuild.exe'
```


## before_script
This helps to execute any script you want execute before the Job script executes.
```
build-job:       # This job runs in the build stage, which runs first.
  stage: build
  before_script:
    - echo "Set the Deploy Version"
```

## stages
With stages we define list of stage which will be part of the CI/CD.

This also define order of execution.
```
stages:  # List of stages for jobs, and their order of execution
  - build
  - test
  - deploy
```

## Job<stage>
We can defined multiple jobs and each job must be part of the Stage.
```
build-job:       # This job runs in the build stage, which runs first.
  stage: build
  script:
    -  write-host "I am in Build Stage"
```

## Script
Here we define list of command for Runner to Execute.
```
build-job:       # This job runs in the build stage, which runs first.
  stage: build
  tags:
    - "windows"
  script:
    -  write-host "I am in Build Stage"
    - msbuild 
```

## Schema of YAML

```
variables: # Define List of Variables
stages: # Define List of Stages
build-job: # Define Job
  stage: build #Define which Stage 
  tags:
    - "windows" # Define Runner Tag
  script:
    -  write-host #Define command to execute 
```

## Demo

**Use Case 1:** Setup Multi Stage/Multi Job Pipeline
```
stages:    
  - build
  - test
  - deploy

build-job:     
  stage: build
  tags:
    - windows-demo
  script:
    - write-host "Build Application"
    
run-job:   
  stage: build  
  tags:
    - windows-demo
  script:
    - write-host "I am in run Job"
    
test-job:   
  stage: test 
  tags:
    - windows-demo
  script:
    - write-host "Run Test"
```

**Use Case 2:** Setup Pipeline with variables

```
variables:
  DEPLOY_PATH: 'C:\DeployIIS' 
stages:    
  - build
  - package
  - deploy

build-job:     
  stage: build
  tags:
    - windows-runner
  script:
    - Write-host "Deployment Path is $DEPLOY_PATH"
```


**Use Case 3:**  Build Visual Studio Project 
```
stages:    
  - build
  - test

build-job:     
  stage: build
  tags:
    - windows-demo
  script:
    - dotnet build $CI_PROJECT_DIR\BuildNugetPackage.sln /p:Configuration="Release"
```


=======
## GitOps with Jenkins and ArgoCD

YouTube Video Link: https://youtu.be/xbxJpZcFT78

This repository demonstrates a GitOps workflow using Jenkins Container and ArgoCD to deploy Kubernetes manifests to a Minikube cluster running on a Container. The project integrates Jenkins CI/CD with ArgoCD to enable automated deployments whenever changes are pushed to the GitHub repository.

### Project Overview

Jenkins: Runs as a container outside the Minikube cluster to handle CI/CD tasks.

Minikube: Serves as the Kubernetes cluster, with Docker as the driver.

ArgoCD: Manages the continuous deployment of Kubernetes manifests.

GitHub Webhooks: Triggers the Jenkins pipeline upon git push events.

Manifests Directory: Contains Kubernetes YAML files for deployment, located in the manifests directory of this repository.


### Architecture

Git Push: Changes to the repository trigger a GitHub webhook.

Jenkins Pipeline: Jenkins fetches the updated repository and interacts with ArgoCD to deploy the manifests.

ArgoCD: Syncs the manifests with the Minikube cluster, ensuring the cluster state matches the desired configuration.


### Prerequisites

#### Tools

Docker

Minikube

Jenkins

ArgoCD CLI

Git


#### Setup

A GitHub repository with Kubernetes manifest files in a manifests directory.

A Minikube cluster with Docker as the driver.

A Jenkins container running outside the Minikube cluster.

ArgoCD installed and configured in the Minikube cluster.




>>>>>>> e9888c0 (DONE)
