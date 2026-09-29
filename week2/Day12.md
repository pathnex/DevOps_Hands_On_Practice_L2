Day 12 — Scaling Applications and Automation
🔹 Ansible — Setup Auto-Scaling Group (ASG)
- name: Setup Auto Scaling Group
  hosts: all
  become: yes
  tasks:
    - name: Create Launch Configuration
      ec2_asg:
        name: pathnex-asg
        region: us-east-1
        launch_config_name: pathnex-launch-config
        min_size: 1
        max_size: 3
        desired_capacity: 2
        vpc_zone_identifier: subnet-12345678
🔹 Terraform — Create a Load Balancer with EC2 Instances
resource "aws_lb" "pathnex_lb" {
  name               = "pathnex-lb"
  internal           = false
  load_balancer_type = "application"
  security_groups   = [aws_security_group.allow_ssh_http.id]
  subnets           = [aws_subnet.public.id]
}

resource "aws_instance" "pathnex_ec2" {
  ami           = "ami-0abcd1234abcd1234"
  instance_type = "t2.micro"
  security_groups = [aws_security_group.allow_ssh_http.name]
  tags = {
    Name = "Pathnex-EC2"
  }
}
🔹 Kubernetes — Horizontal Pod Autoscaler (HPA) with Load Balancer
apiVersion: apps/v1
kind: Deployment
metadata:
  name: pathnex-web-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: pathnex-web-app
  template:
    metadata:
      labels:
        app: pathnex-web-app
    spec:
      containers:
        - name: web
          image: nginx
          ports:
            - containerPort: 80
---
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: pathnex-web-app-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: pathnex-web-app
  minReplicas: 1
  maxReplicas: 5
  targetCPUUtilizationPercentage: 80
🔹 Jenkinsfile — Implement Parallel Stages
pipeline {
    agent any
    stages {
        stage('Build & Test') {
            parallel {
                stage('Build') {
                    steps {
                        echo 'Building project...'
                    }
                }
                stage('Test') {
                    steps {
                        echo 'Running tests...'
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying project...'
            }
        }
    }
}
🔹 GitLab CI/CD — Parallel Jobs for Build & Test
stages:
  - build
  - test
  - deploy

build:
  stage: build
  script:
    - docker build -t pathnex-web-app .

test:
  stage: test
  script:
    - docker run pathnex-web-app npm test

deploy:
  stage: deploy
  script:
    - kubectl apply -f kubernetes/deployment.yaml


🔹 Docker
# Docker Volumes
FROM ubuntu
VOLUME ["/opt/pathnex/data"]
CMD ["sleep", "1000"]

# Real Path
/opt/pathnex/data

# Bash command
docker volume create pathnex-volume

# Day 12 - Scaling Application and automation 
# Ansible _ setup  auto_scaling Group(ASG)
 - name: Setup Auto Scaling Group
   hosts: all
   becomee: yes
   tasks:
    - name: Creat Launch Configuration
      ec2_asg:
       name: pathnex-asg
       region: us-east-1
       launch_config_name: pathex-launch-config
       min_size: 1
       max_size: 3
       desired_capacity: 2
       vpc_zone_identifier: subnet-12345678
# terraform _ create a load balance with Ec2 instance
resource "aws_Ib" "pathnex-ib"{
 name     = "pathnex_ib"
 internal = false
 load_balance_type = "application"
 security_groups = [aws_security_group.allow_ssh_http.id]
 subnets        = [aws_subnet.public.id]
}

resource "aws_instance" "pathnex_ec2"{
ami     = "ami-0abcd1234abcd1234"
instance_type = "t2.micro"
security_group = [aws_security_group.allow_ssh_http.name]
tags = {
  Name = "pathnex-EC2"
 }
}

# Kubernets - HOrizontal Pod Autoscaler (HPA) with Load Balancer
apiVersion: apps/v1
kind: Deployment
metadata:
 name: pathnex-web-app
spec:
 replicas: 2
 selector:
  matchLabels:
   app: pathnex-web-app
template:
 metadata:
  labels:
   app: pathnex-web-app
 
template:
 metadata:
  labels:
   app: pathnex-web-app
 spec:
  containers:
   - name: web
     image: nginx
     ports:
      - containerPort: 80

apiVersion: autoscalling/v2
kind: HorizontalPodAutoscaler
metadata:
 name: pathnex-web-app-hpa
spec:
 scaleTargetRef:
  apiVersion: apps/v1
  kind: Deployment
  name: pathnex-web-app

 minReplicas: 1
 maxReplicas: 5
 targetCPUUtilizationPercentage: 80

 # Jenkinsfile - Implement Parallel Stages
 pipeline {
  agent any 
  stages{
    stage("Build & Test"){
      parallel {
        stage('Build'){
          steps {
            echo 'Building project...'
          }
        }
        stage('Test'){
          steps{
            echo 'Running tests..'
          }
        }
      }
    }
    stage('Deploy'){
      steps {
        echo 'Deploying project..'
      }
    }
  }
 }

# Gitlab CI/CD - Parrallel Jobs for Build & test
stages:
- build
- test
- deploy

build:
 stage: build
 script:
  - docker build -t pathnex-web-app 

test:
 stage: test
 script:
  - docker run pathnex-web-app npm test

deploy:
 stage: deploy
 script:
  - kubectl apply -f kubernetes/deployment.yml


# Docker

# Docker Volumes
FROM ubuntu
VOLUME ["/opt/pathnex/data"]
CMD ["sleep", "1000"]

# Real Path
/opt/pathnex/data

# Bash command
docker volume create pathnex-volume
