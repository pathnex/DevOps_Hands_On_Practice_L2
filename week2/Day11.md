Day 11 — Kubernetes with Helm, Advanced Terraform and GitLab CI/CD

🔹 Ansible — Install Helm on Server
- name: Install Helm
  hosts: all
  become: yes
  tasks:
    - name: Download Helm
      get_url:
        url: https://get.helm.sh/helm-v3.7.0-linux-amd64.tar.gz
        dest: /tmp/helm.tar.gz

    - name: Extract Helm
      unarchive:
        src: /tmp/helm.tar.gz
        dest: /usr/local/bin/
        remote_src: yes

    - name: Set Helm binary permissions
      file:
        path: /usr/local/bin/helm
        mode: '0755'
🔹 Terraform — Provision EC2 with Elastic IP
resource "aws_eip" "pathnex_eip" {
  instance = aws_instance.pathnex_ec2.id
}

resource "aws_instance" "pathnex_ec2" {
  ami           = "ami-0abcd1234abcd1234"
  instance_type = "t3.medium"
  
  tags = {
    Name = "Pathnex-EC2"
  }
}
🔹 Kubernetes — Helm Chart for Nginx
helm repo add stable https://charts.helm.sh/stable
helm install pathnex-nginx stable/nginx-ingress
🔹 Jenkinsfile — Multi-Stage Pipeline
pipeline {
    agent any
    environment {
        IMAGE_NAME = 'pathnex-web-app'
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/pathnex/sample-repo.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${env.IMAGE_NAME}")
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://docker.io', 'docker-credentials') {
                        docker.image("${env.IMAGE_NAME}").push('latest')
                    }
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    sh 'kubectl apply -f deployment.yaml'
                }
            }
        }
    }
}
🔹 GitLab CI/CD — Build, Push, and Deploy with Helm
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
    - helm repo add stable https://charts.helm.sh/stable
    - helm install pathnex-nginx stable/nginx-ingress



🔹 Docker
# EXPOSE & Port Mapping
FROM nginx
EXPOSE 80
docker run -d -p 8080:80 nginx

# Day 11 - Kubernetes with Helm, Advanced Terraform And Gitlab CI/Cd

# Ansible - Install Helm on Server
- name: Install Helm
  hosts: all
  become:yes
  tasks:
   - name: Download Helm
     get_url:
       url: https:get.helm.sh/helm-v3.7.0-linux-amd64.tar.gz
        dest: /tmp/helm.tar.gz

   - name: Extract Helm
     unarchive:
     src: /temp/helm.tar.gz
     dest: /usr/local/bin/
     remote_src: yes

    - name: set Helm binary permisiions
      file:
       path:/usr/local/bin/helm
       mode: '0755'

# Terraform - Provision EC2 with Elastic IP
  resource "aws_eip" "pathnex_eip" {
    instance = aws_intence.pathnex_ec2.id
  }

  resource "aws_instance" "pathnex_ec2" {
    ami     = "ami-0abcd1234abcd1234"
    instance_type = "t3.medium"
    tags = {
      Name = "Pathnex-EC2"
    }
  }

# Kubernetes _ Helm Chart for Nginx
helm repo and stable https://charts.helm.sh/stable
helm install pathnex-nginx stable/nginx-ingress

# Jenkinsfile - Multi-Stage Pipeline
pipeline {
  agent any 
  environment {
    IMAGE_NAME = "pathnex-web-app"
  }
  stages {
    stage('Checkout'){
      steps {
        git 'https://github.com/pathnex/sample-repo.git'
      }
    }
    stage('Build Docker Image'){
      steps {
        script {
          docker.build("${env.Image_Name}")
        }
      }
    }
    stage('Push Docker image'){
      steps {
        script {
          docker.withRegistry('https://docker.io', 'docker-credentials') {
            docker.image("${env.IMAGE_NAME}").push('latest')
          }
        }
      }
    }
    stage('Deploy to Kubernets'){
      steps{
        script {
          sh 'kubectl apply -f deployment.yml'
        }
      }
    }
  }
}

# GitLab CI/CD - Build, Push, and Deploy with Helm

stages:
- build
- push
- deploy

build:
 stage: build
 script:
 - docker build -t pathnex-web-app.

push:
 stage: push
 script:
   - docker login -u "$CI_REGISTRY_USER" -p "$CI_REGISTRY_PASSWORD"
   - docker push pathnex-web-app

deploy:
 stage:deploy
 script:
  - helm repo add stable https://charts.helm.sh/stable
  - helm install pathnex-nginx stable/nginx-ingress

# Docker
# Expose & Port Mapping
FROM nginx
EXPOSE 80
docker run -d -p 8080:80 nginx


