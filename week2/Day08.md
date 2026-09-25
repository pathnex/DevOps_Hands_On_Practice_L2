Day 08 — Introduction to Docker and CI/CD Pipelines
🔹 Ansible — Install Docker Compose
- name: Install Docker Compose
  hosts: all
  become: yes
  tasks:
    - name: Install dependencies
      yum:
        name: "python3-pip"
        state: present
    - name: Install docker-compose
      pip:
        name: docker-compose
🔹 Terraform — EC2 with Security Group and EBS Volume
resource "aws_security_group" "allow_ssh_http" {
  name        = "allow_ssh_http"
  description = "Allow SSH and HTTP access"
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
}

resource "aws_instance" "pathnex_ec2" {
  ami           = "ami-0abcd1234abcd1234"
  instance_type = "t3.medium"
  security_groups = [aws_security_group.allow_ssh_http.name]

  ebs_block_device {
    device_name = "/dev/sdh"
    volume_size = 30
  }
}
🔹 Kubernetes — Service with NodePort
apiVersion: v1
kind: Service
metadata:
  name: pathnex-service
spec:
  type: NodePort
  selector:
    app: pathnex-app
  ports:
    - protocol: TCP
      port: 80
      nodePort: 30007
🔹 Jenkinsfile — Docker Build and Push
pipeline {
    agent any
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('pathnex-app')
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://docker.io', 'docker-credentials') {
                        docker.image('pathnex-app').push('latest')
                    }
                }
            }
        }
    }
}
🔹 GitLab CI/CD — Build & Push Docker Image
stages:
  - build
  - push

build:
  stage: build
  script:
    - docker build -t pathnex-app .

push:
  stage: push
  script:
    - docker login -u "$CI_REGISTRY_USER" -p "$CI_REGISTRY_PASSWORD"
    - docker push pathnex-app


🔹 Docker
# Alpine Linux
FROM alpine:latest
WORKDIR /opt/pathnex/alpine-app
CMD ["echo", "Hello Pathnex"]



# Day 08 - Introdyction to docker and CI?CD pipeline

# Ansible - Install Docker Compose 
- name: Install Docker Compose
  hosts: all
  become: yes
  tasks:
   - name: Install dependencies
     yum:
      name: "python3-pip"
      state: present
   - name: Install docker-compose
     pip:
      name: docker-compose

# Terraform -Ec2 with Security
Group and wbs Volume
resource "aws_security_group" "allow_ssh_http"{
  name  = "allow_ssh_http"
  description = "Allow SSH and HTTP access"
  ingress {
    from_port = 22
    to_port. = 22
    protocol  = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
 ingress{
  from_port = 80
  to_port = 80
  protocol = "tcp"
  cidr_block = ["0.0.0.0/0"]
 }


 resource "aws_instance" "pathnex_ec2" {
  ami = "ami-0abcd1234abcd1234"
  instance_type = "t3.medium"
  security_group = [aws_security_group.allow_ssh_http.name]
 }

  ebs_block_device{
    device_name = "/dev/sdh"
    volume_size = 30
  }
}

# kubernets - Service with NodePort
apiVersion:v1
kind:Service
metadata"
  name:pathnex-service
space:
 type: NodePort
 selector:
  app:pathnex-app
 ports:
  - protocol: TCP
    port: 80
    nodePort: 30007


# Jenkinsfile - Docker Build and Push
pipeline {
  agent any 
  stages{
    stage('Build Docker Image'){
      steps{
        script{
          docker.build('pathnex-app')
        }
      }
    }
    stage(''Push Docker Image){
      steps{
        script{
          docker.withRegistry('https://docker.io', 'docker-credentials'){
            docker.image('pathnex-app').push('latest')
          }
        }
      }
    }
  }
}


# Github CI/CD. - Build & Push 
Docker Image
stages:
- build
- push

build:
 stage: build
 script:
 - docker build -t pathnex-app.

push:
 stage: push
 script:
  - docker login -u "$CI_REGISTRY_USER" -p "$CI_REGISTRY_PASSWORD"
  - docker push pathnex-app


# Docker
# Alpine Linux
From alpine:latest
WORKDIR /opt/pathnex/alpine-app
CMD ["eco", "Hello Pathnex"]
