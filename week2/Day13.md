Day 13 — Advanced Automation with CloudFormation and CI/CD
🔹 Ansible — Multi-Node Nginx Setup
- name: Setup Nginx on multiple nodes
  hosts: all
  become: yes
  tasks:
    - name: Install nginx
      yum:
        name: nginx
        state: present

    - name: Start nginx service
      service:
        name: nginx
        state: started
        enabled: yes
🔹 Terraform — Create IAM Users and Policies
resource "aws_iam_user" "example_user" {
  name = "pathnex_user"
}

resource "aws_iam_policy" "example_policy" {
  name        = "pathnex-policy"
  description = "Policy for Pathnex application"
  policy      = jsonencode({
    Version = "2012-10-17"
    Statement = [
      {
        Action = "s3:ListBucket"
        Effect = "Allow"
        Resource = "arn:aws:s3:::pathnex-bucket"
      },
    ]
  })
}
🔹 Kubernetes — Deploy Nginx with ConfigMap and Secrets
apiVersion: v1
kind: ConfigMap
metadata:
  name: nginx-config
data:
  nginx.conf: |
    server {
      listen 80;
      server_name localhost;
      location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
      }
    }

---
apiVersion: v1
kind: Secret
metadata:
  name: nginx-secret
type: Opaque
data:
  password: cGF0aG5leHBhc3M=

---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: pathnex-nginx
spec:
  replicas: 2
  selector:
    matchLabels:
      app: pathnex-nginx
  template:
    metadata:
      labels:
        app: pathnex-nginx
    spec:
      containers:
        - name: nginx
          image: nginx
          volumeMounts:
            - mountPath: /etc/nginx/nginx.conf
              name: nginx-config
              subPath: nginx.conf
      volumes:
        - name: nginx-config
          configMap:
            name: nginx-config
        - name: nginx-secret
          secret:
            secretName: nginx-secret
🔹 Jenkinsfile — Multi-Branch Pipeline with Docker Build
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    docker.build('pathnex-app')
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    kubectl apply -f kubernetes/deployment.yaml
                }
            }
        }
    }
}
🔹 GitLab CI/CD — Advanced Deployment with Helm
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
    - helm repo add pathnex https://charts.pathnex.com
    - helm install pathnex-nginx pathnex/nginx-ingress



🔹 Docker
# COPY vs ADD
FROM ubuntu
COPY pathnex-file.txt /opt/pathnex/files/
ADD pathnex.tar.gz /opt/pathnex/extracted/


# Day 13 - Advanced Automation with CloudFormation and CI/CD

# Ansible - Multi-Node Nginx Setup
- name: Setup Nginx on multiple nodes
  hosts: all
  become: yes
  tasks:
  - name: install nginx
    yum:
     name: nginx
     state: present

  - name : Start nginx service
    service:
     name: nginx
     state: started
     enabled: yes

# Terraform - Create IAM Users and policies
resource "aws_iam_user" "example_user"{
   name = "pathnex_user"
}

resource "aws_iam_policy" "example_policy"{
  name    = "pathnex-policy"
  description = "Policy for Pathnex application"
  policy    = jsonencode ({
    Version= "2012-10-17"
    Statement = [
      {
        Action = "s3:ListBucket"
        Effect = "Allow"
        Resource = "arn:aws:s3:::pathnex-bucket"
      }
    ]
  })
}

# Kubernets - Deploy Nginx with ConfigMap and Secrets
apiVersion: v1
kind: ConfigMap
metadata:
 name: nginx-config
data:
 nginx.conf: |
    server {
      listen 80;
      server_name localhost;
      location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
      }
    }

---
apiVersion: v1
kind: Secret
metadata:
  name: nginx-secret
type: Opaque
data:
  password: cGF0aG5leHBhc3M=

---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: pathnex-nginx
spec:
  replicas: 2
  selector:
    matchLabels:
      app: pathnex-nginx
  template:
    metadata:
      labels:
        app: pathnex-nginx
    spec:
      containers:
        - name: nginx
          image: nginx
          volumeMounts:
            - mountPath: /etc/nginx/nginx.conf
              name: nginx-config
              subPath: nginx.conf
      volumes:
        - name: nginx-config
          configMap:
            name: nginx-config
        - name: nginx-secret
          secret:
            secretName: nginx-secret
# Jenkinsfile — Multi-Branch Pipeline with Docker Build
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    docker.build('pathnex-app')
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    kubectl apply -f kubernetes/deployment.yaml
                }
            }
        }
    }
}
# GitLab CI/CD — Advanced Deployment with Helm
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
    - helm repo add pathnex https://charts.pathnex.com
    - helm install pathnex-nginx pathnex/nginx-ingress



# Docker
# COPY vs ADD
FROM ubuntu
COPY pathnex-file.txt /opt/pathnex/files/
ADD pathnex.tar.gz /opt/pathnex/extracted/


