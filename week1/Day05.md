# Day 05 — Advanced CI/CD and Infrastructure Provisioning

## 🔹 Jenkinsfile — With Git Integration and Testing

```groovy
pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/pathnex/sample-repo.git'
            }
        }
        stage('Build') {
            steps {
                echo 'Building project from Git repository'
            }
        }
        stage('Test') {
            steps {
                echo 'Running unit tests'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying application'
            }
        }
    }
}
🔹 GitLab CI/CD — With Docker Build
stages:
  - build
  - push
  - deploy

build:
  stage: build
  script:
    - docker build -t pathnex-app .

push:
  stage: push
  script:
    - docker push pathnex-app

deploy:
  stage: deploy
  script:
    - kubectl apply -f kubernetes/deployment.yaml
🔹 Ansible — Create User and Set Permissions
- name: Create a new user
  hosts: all
  become: yes
  tasks:
    - name: Create user
      user:
        name: pathnex
        state: present
        shell: /bin/bash
    - name: Set permissions for the user
      file:
        path: /home/pathnex
        owner: pathnex
        group: pathnex
        mode: '0755'
🔹 Terraform — EC2 with Tags and Volume
resource "aws_instance" "PathnexEC2" {
  ami           = "ami-0abcd1234abcd1234"
  instance_type = "t2.medium"
  
  tags = {
    Name = "Pathnex-Server"
  }

  ebs_block_device {
    device_name = "/dev/sdh"
    volume_size = 50
  }
}


🔹 Docker
# Python Application
print("Hello Pathnex")

# Docker File
FROM python:3.11
WORKDIR /opt/pathnex/python-app
COPY app.py /opt/pathnex/python-app/
CMD ["python", "/opt/pathnex/python-app/app.py"]

# Real Path
/opt/pathnex/python-app



# Day 05 -Advanced Ci/CD and infrastructure Provisioning
# Jenkinsfile - With Git Integration and Testing

```groovy
pipeline{
  agent any
  stages{
    stage{'Clone Repository'}{
      steps{
        git 'https://github.com/pathnex/sample-repo.git'
      }
    }
    stage('build'){
      steps{
        echo 'Building project from Git repository'
      }
    }
    stage('Test'){
      steps{
        echo 'Run ing unit tests'
      }
    }
    stage('Deploy'){
      steps{
        echo 'Deploying application'
      }
    }
  }
}

# GitLab CI/CD - with Docker Build

stages:
-build
-push
-deploy

build:
 stage:build
 script:
 - docker build -t pathnex-app

push:
 stage: push
 svript:
 -docker push pathnex-app

deploy:
 stage: deploy
 script:
  -kubectl apply -f kubernets/deployment.yaml


# Ansible - Create User and Set Permissions
- name: Create a new user
  hosts: all
  become: yes
  tasks:
   -name: Create user
    user:
     name: pathnex
     state: present
     shell: /bin/bash

- name: Set permissions for the user
  file:
   path: /home/pathnex
   owner: pathnex
   group: pathnex
   mode: '0755'

# Terraform - EC2 with Tags and Volume
resource "aws_instance" "PathnexEC2"{
  ami   = "ami-0abcd1234abcd1234"
  instance_type = "t2.medium"
  tags = {
    Name = "Pathnex-Server"
  }
  ebs_block_device{
    device_name ="/dev/sdh"
    volume_size = 50
  }
}


 # Docker
 #Python Application
 print("Hello Pathnex")

 #Docker File
 From python:3.11
 WOEKDIR/opt/pathnex/python-app
 COPY app.py /opt/pathnex/python-app/
 CMD ["python", "/opt/pathnex/python-app/app.py"]

 # Real Path
 /opt/pathnex/python-app