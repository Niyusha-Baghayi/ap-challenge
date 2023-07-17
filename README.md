Here is the README divided into two parts with separate sections for the Kafka setup and Python CI/CD pipeline in Markdown format:
# Table of Contents
- [Table of Contents](#table-of-contents)
- [Part 1 - Kafka Setup](#part-1---kafka-setup)
  - [Overview](#overview)
  - [Install Kafka Cluster](#install-kafka-cluster)
- [Part 2 - Python CI/CD Pipeline](#part-2---python-cicd-pipeline)
  - [Overview](#overview-1)
  - [GitLab CI Pipeline Stages](#gitlab-ci-pipeline-stages)
    - [Build Stage](#build-stage)
    - [Deploy Stage](#deploy-stage)
  - [Conclusion](#conclusion)

# Part 1 - Kafka Setup

## Overview
Kafka is deployed on a 3 node cluster using Ansible playbooks and roles.

## Install Kafka Cluster

In order to install Kafkacluster on your nodes, it is required to do the following steps.
1. Set global environment variables which are located at `inventory/group_vars/all.yaml` file. For example `kafka_installation_path` variable indicates that where to keep manifest of kafka files for Kafka components.

2. Consider `inventory/inventory.yaml` file and place the `IP` and `user` of the nodes there. You can easily create a new name and place it in inventory.yaml‍ file.

3. Execute the following command:
  ```bash
  ansible-playbook -i <path-to-inventory-file> cluster.yaml -v -b -kK
  # e.g.
  ansible-playbook -i inventory/inventory.yaml cluster.yaml -v -b -kK
  ```

# Part 2 - Python CI/CD Pipeline

## Overview
The GitLab CI/CD pipeline builds, tests, and deploys the Python app.

## GitLab CI Pipeline Stages
* `build` stage to build Docker image
* `deploy` stage to deploy app

### Build Stage
* Uses Kaniko executor to build Docker image
* Build context from GitLab repository
* Push image to GitLab container registry

### Deploy Stage
* Configure Kubernetes credentials
* Update deployment manifest with new image
* Rolling update to pull new image

## Conclusion
The GitLab CI automates the Python application from build to deployment based on code changes.