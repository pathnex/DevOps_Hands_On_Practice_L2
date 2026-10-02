Day 15 — Automation with Terraform, Ansible, and CI/CD Pipelines
🔹 Ansible — Deploy a Web Application to Multiple Hosts
- name: Deploy web application to multiple hosts
  hosts: all
  become: yes
  tasks:
    - name: Copy web app files
      copy:
        src: /path/to/web/app/
        dest: /var/www/html/
    - name: Start web app service
      service:
        name: apache2
        state: started
        enabled: yes
🔹 Terraform — Create EC2 with ALB (Application Load Balancer)
resource "aws_lb" "pathnex_lb" {
  name               = "pathnex-lb"
  internal           = false
  load_balancer_type = "application"
  security_groups    = [aws_security_group.allow_ssh_http.id]
  subnets            = [aws_subnet.public.id]
}

resource "aws_instance" "pathnex_ec2" {
  ami             = "ami-0abcd1234abcd1234"
  instance_type   = "t2.micro"
  security_groups = [aws_security_group.allow_ssh_http.name]

  tags = {
    Name = "Pathnex-EC2"
  }
}
🔹 Kubernetes — Helm Chart for Redis with Persistence
helm install pathnex-redis bitnami/redis --set persistence.enabled=true --set persistence.size=8Gi
🔹 Jenkinsfile — Multi-Environment Deployment
pipeline {
    agent any
    environment {
        IMAGE_NAME = 'pathnex-web-app'
        DEPLOY_ENV = 'production'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building Docker image...'
                docker.build("${env.IMAGE_NAME}")
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    if (env.DEPLOY_ENV == 'production') {
                        sh 'kubectl apply -f kubernetes/prod-deployment.yaml'
                    } else {
                        sh 'kubectl apply -f kubernetes/dev-deployment.yaml'
                    }
                }
            }
        }
    }
}
🔹 GitLab CI/CD — Environment-Specific Deployments
stages:
  - build
  - push
  - deploy

build:
  stage: build
  script:
    - docker build -t pathnex-web-app .

push:
  stage: push
  script:
    - docker login -u "$CI_REGISTRY_USER" -p "$CI_REGISTRY_PASSWORD"
    - docker push pathnex-web-app

deploy:
  stage: deploy
  script:
    - |
      if [ "$CI_COMMIT_REF_NAME" == "main" ]; then
        kubectl apply -f kubernetes/prod-deployment.yaml
      else
        kubectl apply -f kubernetes/dev-deployment.yaml
      fi


🔹 Docker
# Multi RUN Commands
FROM ubuntu
RUN apt update && \
    apt install curl -y && \
    apt install vim -y
CMD ["echo", "Hello Pathnex"]


Day 15 Automation with terraform ansible and ci/cd piplelines

# ansible - Deploy a web application to multiple hosts

hosts: all
become: yes
tasks:
 - name: Copy web app file
   copy:
    src: /path/to/web/app/
    dest: /var/www/html/
- name: Start web app service
  service:
   name: apache2
   state: started
   enabled: yes

# Terraform - create ec2 with Alb (Application load balancer)
resource "aws_ib" "pathnex_ib" {
  name: "pathnex-ib"
  internal = false
  load_balance_type = "application"
  security_group = [aws_security_group.allow_ssh_http.id]
  subnets    =  [aws_subnet.public.id]
}

resource "aws_instance" "pathnex_ec2"{
ami       = "ami-0abcd1234abcd1234"
instance_type = "t2.micro"
security_group = [aws_security_group.allow_ssh_http.name]

tags = {
  Name = "Pathnex-EC2"
 }
}

# kubernets - Helm chart for redis with presistence
helm install pathnex-redis bitnami/redis -- set persistence.enabled=true --set persistence.size=8Gi

# Jenkinsfile - Multi- Environment Deployment
pipeline {
  agent any 
  environment {
    IMAGE_NAME = 'pathnex-web-app'
    DEPLOY_ENV = 'production'
  }
  stages {
    stage('Build'){
     steps{
      eco 'Building Docker Image..'
      docker.build("${env.IMAGE_NAMR}")
     }
    }
    stage('Test'){
      steps{
          echo 'Running tests...'
      }
  }
  stage('Deploy to Kubernetes') {
    steps{
      script{
    if (env.DEPLOY_ENV == 'production'){
      sh 'kubectl apply -f kubernetes/pod-deployment.yml'
    } else {
      sh 'kubectl apply -f kubernetes/dev-deployment.yml'
       }
     } 
   } 
  }
 }
} 

#Gitlab CI/CD - Environment- Specific Deployments
stages:
- build
- push
- deploy

build:
 stage: build
 script:
  - docker build -t pathnex-web-app

push
 stage: ousg
 script:
  - docker login - u "$CI_REGISTRY_USER" -p "$CI_REGISTRY_PASSWORD"
  - docker push pathnex-web-app

docker:
 stage: deploy
  script:
   -|
    if ["$CI_COMMIT_REF_NAME" == "main"];then
       kubectl apply -f kubernetes/prod-deployment.yml
    else
    kubectl apply -f kubernets/dev-deployment.yml
    
# Docker
# multi Run Commands
From ubuntu
RUN apt update &&\
 apt install cirl -y &&\
 apt install vim -y
CMD ["echo" , "hello Pathnex" ]


