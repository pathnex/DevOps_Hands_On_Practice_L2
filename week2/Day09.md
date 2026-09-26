Day 09 — Docker Integration with Jenkins & GitLab
🔹 Ansible — Setup Docker Container for Nginx
- name: Setup Docker Container for Nginx
  hosts: all
  become: yes
  tasks:
    - name: Pull Nginx image
      docker_image:
        name: nginx
        source: pull
    - name: Run Nginx container
      docker_container:
        name: nginx-container
        image: nginx
        state: started
        published_ports:
          - "8080:80"
🔹 Terraform — EC2 with Auto Scaling Group
resource "aws_launch_configuration" "example" {
  name = "example-config"
  image_id = "ami-0abcd1234abcd1234"
  instance_type = "t3.medium"
}

resource "aws_autoscaling_group" "example" {
  desired_capacity     = 2
  max_size             = 3
  min_size             = 1
  vpc_zone_identifier  = ["subnet-12345678"]
  launch_configuration = aws_launch_configuration.example.id
}
🔹 Kubernetes — Horizontal Pod Autoscaler (HPA)
apiVersion: apps/v1
kind: Deployment
metadata:
  name: pathnex-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: pathnex-app
  template:
    metadata:
      labels:
        app: pathnex-app
    spec:
      containers:
        - name: nginx
          image: nginx
          ports:
            - containerPort: 80

---

apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: pathnex-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: pathnex-deployment
  minReplicas: 1
  maxReplicas: 10
  targetCPUUtilizationPercentage: 50
🔹 Jenkinsfile — Deploy to Kubernetes
pipeline {
    agent any
    stages {
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    sh 'kubectl apply -f deployment.yaml'
                }
            }
        }
    }
}
🔹 GitLab CI/CD — Deploy to Kubernetes
stages:
  - deploy

deploy:
  stage: deploy
  script:
    - kubectl apply -f kubernetes/deployment.yaml


🔹 Docker
# Environment Variables
FROM ubuntu:22.04
ENV INSTITUTE=Pathnex
ENV COURSE=DevOps
CMD echo "$INSTITUTE - $COURSE"


# Day 09 - Docker Integration with Jenkins & GItlab

# Ansible - Setup Docker Container for Nginx
- name: Setup Docker Container for Nginx
  hosts: all
  become: yes
  tasks:
   - name: Pull Nginx image
     docker_image:
     name: nginx
     source: pull
   - name: Run Nginx container
     docker_container:
      name: nginx-container
      image: nginx
      state: started
      published_ports:
       - "8080:80"

# Terraform _EC2 with Scalling Grouo
resource "aws_launch_configuration" "pathnex-app"{
  name = "pathnex-app-config"
  image_id = "ami-0abcd1234abcd1234"
  instance_type = "t3.medium"
}

resource "aws_autoscaling_group" "pathnex"{
  desired_capacity  = 2
  max_size        = 3
  min_size      = 1
  vpc_zone_identifier = ["subnet-12345678"]
   launch_configuration = aws_launch_configuration.example.id
}

# Kubernetes - Horizontal Pod Autoscaler (HPA)
apiVersion: app/v1
kind: Deployment
metadata:
 name: pathnex-deployment
spec:
 replicas: 1
 selector:
  matchLabels:
    app:pathnex-app
 template:
  metadata:
   labels:
    app: pathnex-app
   spec:
    containers:
     - name: nginx
       image: nginx
       ports:
        -containerPort: 80

apiVersion: autoscalling/v2
kind: HorizontalPodAutoscaler
metadata:
 name: pathnex-hpa
spec:
 scaleTargetRef:
  apiVersion: app/v1
  kind: Deployment
  name: pathnex-deployment
minReplicas: 1
maxReplicas: 10
targetCPUUtillizationPercentage: 50

# Jenskinsfile - Deploy to kubernates
pipeline {
  agent any
  stages{
    script {
      sh 'kubect apply -f deployment.yml'
    }
  }
}


# Gitlab CI/CD -deploy to kubernates
stages:
- deploy

deploy:
 stage:deploy
 script:
  -kubectl apply -f
  kubernetes/deployment.yaml


# Docker
# Environment Variables
FROM ubuntu:22.04
ENV INSTITUTE=Pathnex
ENV COURSE=DevOps
CMD echo "$INSTITUTE - $COURSE"

