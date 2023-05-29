---
sidebar_position: 2
sidebar_label: CI/CD Setup in Our Project
---
# How we are setting up the things
--- 
![CI CD FLOW](../../../static/img/ci_cd_flow.png)
 
 * Visual Demo of different services that are up through portainer.io
 * Multibranch pipelines instead of freestyle project
 * DB pipelines to provide any DB
 * Configuration of Vault for secrets
 * Single source of truth, everything is on a git repo and fetched from there only
 * Explanation of next steps to integrate ansible-galaxy and host ansible collections

### Components
 * **GitHub Repos**: Microservices are developed on this platform, code is pushed merged etc. We can also leverage GitHub Actions for CI - (testing and building of the image).

* **Jenkins Pipeline**:  [Jenkins](https://www.jenkins.io/) is a job runner which executes a series of tasks depending on the config.
        **Development Pipelines**: Pipelines to manager for development  environment.
        **Production Pipelines**: Pipelines to manager for development  environment.

* **Private Docker registry**: To hold build artefacts
Hashicorp Vault: Used to store secrets and credentials in one place to be used by different microservices. Developers can specify creds here and ansible can pick up those creds from here. It also provides RBAC.

* **Docker Swarm**: Docker swarm to deploy services on a docker swarm cluster
Ansible Galaxy (Future Scope): Add ansible roles to an ansible-galaxy of the building blocks in Samagra. One can easily pull the ansible roles accordingly depending upon their use case. 


In every repo/project we have a folder name **build** inside which there is a **Jenkinsfile** file which contains the automation code.

sample jenkins file in nodejs



```tsx 
 pipeline {
    agent { docker { image 'node:16.17.1-alpine' } }
    stages {
        stage('build') {
            steps {
                sh 'node --version'
            }
        }
    }
}
```
So once a developer pushed a code to the repo (main or any particular branch) .Whenever code is avaialable jenkins pull the code and make a build.Once build is completed it generates artifact. 

This artifact should be deployed in the target env.Target env may be a vm/docker/kubernetes container.In our case we are using [**Docker**](https://www.docker.com/).So we should have some tool to deploy this to the target environment. In our case we have [**ansible**](https://www.ansible.com/) as a deployment service which deploys our docker container.

For some particular case we need to have access to some secret keys and credentials and in order to use them safely we are using [**vault**](https://www.hashicorp.com/products/vault/secrets-management) to store such values and fetch them from it safely.