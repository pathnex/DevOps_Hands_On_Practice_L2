# Day 10 — Advanced Kubernetes, Jenkins, and GitLab CI

## 🔹 Ansible — Create Docker Containers for Multiple Applications

```yaml
- name: Setup Docker Containers for Multiple Apps
  hosts: all
  become: yes
  tasks:
    - name: Pull Web App Image
      docker_image:
        name: my-web-app
        source: pull

    - name: Pull Database App Image
      docker_image:
        name: my-database-app
        source: pull

    - name: Run Web App Container
      docker_container:
        name: web-app
        image: my-web-app
        state: started
        published_ports:
          - "8080:80"
    
    - name: Run Database App Container
      docker_container:
        name: database-app
        image: my-database-app
        state: started
        published_ports:
          - "3306:3306"
🔹 Terraform — VPC with Private and Public Subnets
resource "aws_vpc" "main" {
  cidr_block = "10.0.0.0/16"
}

resource "aws_subnet" "public" {
  vpc_id                  = aws_vpc.main.id
  cidr_block              = "10.0.1.0/24"
  availability_zone       = "us-east-1a"
  map_public_ip_on_launch = true
}

resource "aws_subnet" "private" {
  vpc_id            = aws_vpc.main.id
  cidr_block        = "10.0.2.0/24"
  availability_zone = "us-east-1b"
}
🔹 Kubernetes — Deploying StatefulSet
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: pathnex-db
spec:
  serviceName: "pathnex-db"
  replicas: 3
  selector:
    matchLabels:
      app: pathnex-db
  template:
    metadata:
      labels:
        app: pathnex-db
    spec:
      containers:
        - name: db
          image: mysql:5.7
          volumeMounts:
            - mountPath: /var/lib/mysql
              name: mysql-storage
  volumeClaimTemplates:
    - metadata:
        name: mysql-storage
      spec:
        accessModes: ["ReadWriteOnce"]
        resources:
          requests:
            storage: 1Gi
🔹 Jenkinsfile — Build and Deploy to Kubernetes
pipeline {
    agent any
    environment {
        IMAGE_NAME = 'pathnex-web-app'
    }
    stages {
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
🔹 GitLab CI/CD — Build, Push, and Deploy
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
    - kubectl apply -f kubernetes/deployment.yaml


🔹 Docker
# Working Directory & COPY
FROM ubuntu:22.04
WORKDIR /opt/pathnex/devops-project
COPY . /opt/pathnex/devops-project/
CMD ["ls", "-l", "/opt/pathnex/devops-project"]

# Real Path
/opt/pathnex/devops-project


#10 Day - Advanced kubernetes, Jenkins, and Github CI

## Ansible - Create Docker Containers for multiple Application

```yaml
- name: Setup Docker Containers for Multiple Apps
  hosts: all
  become: yes
  tasks:
   - name: Pull Web App Image
     docker_image:
      name: my-web-app
      soure: pull
  
   - name: Pull Database App Image
     docker_image:
      name: my-database-app
      source: pull


   - name: Run Web App Container
     docker_container:
      name: web-app
      image: my-web-app
      state: started
      published_port: 
       - "8080:80"

   - name: Run Database App Container
     docker_container:
      name: database-app
      state: started
      published_ports:
       - "3306:3306"

# Terraform — VPC with Private and Public Subnets
resource "aws_vpc" "main" {
  cidr_block = "10.0.0.0/16"
}

resource "aws_subnet" "public" {
  vpc_id                  = aws_vpc.main.id
  cidr_block              = "10.0.1.0/24"
  availability_zone       = "us-east-1a"
  map_public_ip_on_launch = true
}

resource "aws_subnet" "private" {
  vpc_id            = aws_vpc.main.id
  cidr_block        = "10.0.2.0/24"
  availability_zone = "us-east-1b"
}
# Kubernetes — Deploying StatefulSet
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: pathnex-db
spec:
  serviceName: "pathnex-db"
  replicas: 3
  selector:
    matchLabels:
      app: pathnex-db
  template:
    metadata:
      labels:
        app: pathnex-db
    spec:
      containers:
        - name: db
          image: mysql:5.7
          volumeMounts:
            - mountPath: /var/lib/mysql
              name: mysql-storage
  volumeClaimTemplates:
    - metadata:
        name: mysql-storage
      spec:
        accessModes: ["ReadWriteOnce"]
        resources:
          requests:
            storage: 1Gi
# Jenkinsfile — Build and Deploy to Kubernetes
pipeline {
    agent any
    environment {
        IMAGE_NAME = 'pathnex-web-app'
    }
    stages {
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
# GitLab CI/CD — Build, Push, and Deploy
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
    - kubectl apply -f kubernetes/deployment.yaml


# Docker
# Working Directory & COPY
FROM ubuntu:22.04
WORKDIR /opt/pathnex/devops-project
COPY . /opt/pathnex/devops-project/
CMD ["ls", "-l", "/opt/pathnex/devops-project"]

# Real Path
/opt/pathnex/devops-project