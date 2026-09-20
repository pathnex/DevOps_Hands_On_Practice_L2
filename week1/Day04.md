Day 04 — Basic CI/CD Concepts with Jenkins & GitLab


🔹 Jenkinsfile — Basic CI Pipeline
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building project'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying application'
            }
        }
    }
}


🔹 GitLab CI/CD — Basic Pipeline
stages:
  - build
  - test
  - deploy

build:
  stage: build
  script:
    - echo "Building project"

test:
  stage: test
  script:
    - echo "Running tests"

deploy:
  stage: deploy
  script:
    - echo "Deploying application"


🔹 Ansible — Install and Configure Nginx
- name: Install and configure Nginx
  hosts: all
  become: yes
  tasks:
    - name: Install nginx
      yum:
        name: nginx
        state: present
    - name: Configure nginx
      template:
        src: nginx.conf.j2
        dest: /etc/nginx/nginx.conf
    - name: Start nginx service
      service:
        name: nginx
        state: started
        enabled: yes


🔹 Terraform — EC2 with Security Group
resource "aws_security_group" "example" {
  name        = "example_security_group"
  description = "Allow SSH and HTTP"
  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}


🔹 Docker
# Apache Container
FROM ubuntu:22.04
RUN apt update && apt install apache2 -y
RUN echo "Hello Pathnex" > /var/www/html/index.html
CMD ["apachectl", "-D", "FOREGROUND"]

# Bash Real Path
/var/www/html



# Day 04 -Basic CI/CD Conscepts with Jenkins & GitLab

Jenkinsfile - Basic CI Pipeline
pipeline{
  agent any 
  stages{
    stage('Build'){
      steps{
        echo'Building project'
      }
    }
    stage('Test'){
      steps{
        echo 'Running tests'
      }
    }
    stage('Deploy'){
      steps{
        echi 'Deploying application'
      }
    }
  }
}

# GitLab CI/CD - Basic Pipeline
stages:
 -build
 -test
 -deploy

build:
 stage:build
 script:
  - echo "Building project"

test:
 stage: test
 script:
  -echo "Runing test"

deploy:
 stage: deploy
 script:
  -echo "Deployinh application"


# Ansible - Install and configure Nginx
-name: Install and configure Nginx
 host: all
 become : yes
 tasks:
 - name: install nginx
   yum:
   name: nginx
   state: present

 - name: Configure nginx
   template:
    src: nginx.conf.j2
    dest: /etc/nginx/nginx.conf

 - name: Start nginx service
   service:
    name: nginx
    state: started
    enabled: yes

# Terraform -Ec2 with security Group
resource "aws_security_group" "Deepak" {
  name    = "Deepak"
  description = "Allow SSH and HTTP"
  ingress{
    from_port = 22
    to_port = 22
    protocol = "tcp"
    cidr_blocks=["0.0.0.0/0"]
  }

 ingress{
  from_port = 80
  to_port = 80
  protocol = "tcp"
  cidr_block = ["0.0.0.0/0"]
 }

 egress{
  from_port =0
  to_port = 0
  protocol = "-1"
  cidr_blocks = ["0.0.0.0/0]
 }
}

# Docker
#Apache Constainer
FROM ubuntu:22.04
RUN apt update && apt install apache2 -y
Run echo "Hello Pathnex" >/var/www/hrml/index.html
CMD ["apachectl" , "-D", "FOREGROUND"]

# Bash Real Path
/var/www/html
