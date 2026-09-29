# Day 14 — Kubernetes Advanced Concepts & Multi-Environment Deployments

# Ansible — Setup Nginx with Reverse Proxy

```yaml
- name: Setup Nginx with Reverse Proxy
  hosts: all
  become: yes
  tasks:
    - name: Install nginx
      yum:
        name: nginx
        state: present
    - name: Configure nginx as reverse proxy
      template:
        src: reverse-proxy.conf.j2
        dest: /etc/nginx/conf.d/reverse-proxy.conf
    - name: Restart nginx service
      service:
        name: nginx
        state: restarted
        enabled: yes
# Terraform — Create S3 Bucket with Versioning and Logging
resource "aws_s3_bucket" "pathnex_bucket" {
  bucket = "pathnex-bucket"
  versioning {
    enabled = true
  }

  logging {
    target_bucket = "pathnex-log-bucket"
    target_prefix = "logs/"
  }
}
# Kubernetes — Ingress with Nginx Controller
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: pathnex-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
    - host: pathnex.local
      http:
        paths:
        - path: /
          pathType: Prefix
          backend:
            service:
              name: pathnex-service
              port:
                number: 80
# Jenkinsfile — Build, Test, and Deploy with Stages
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building Docker image...'
                docker.build('pathnex-web-app')
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
                    sh 'kubectl apply -f kubernetes/deployment.yaml'
                }
            }
        }
    }
}
# GitLab CI/CD — Multi-Stage Deployment with Helm
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
    - helm upgrade --install pathnex-nginx pathnex/nginx-ingress


# Docker
# CMD vs ENTRYPOINT
FROM ubuntu
ENTRYPOINT ["echo"]
CMD ["Hello Pathnex"]


# Day 14 — Kubernetes Advanced Concepts & Multi-Environment Deployments

# Ansible — Setup Nginx with Reverse Proxy

```yaml
- name: Setup Nginx with Reverse Proxy
  hosts: all
  become: yes
  tasks:
    - name: Install nginx
      yum:
        name: nginx
        state: present
    - name: Configure nginx as reverse proxy
      template:
        src: reverse-proxy.conf.j2
        dest: /etc/nginx/conf.d/reverse-proxy.conf
    - name: Restart nginx service
      service:
        name: nginx
        state: restarted
        enabled: yes
# Terraform — Create S3 Bucket with Versioning and Logging
resource "aws_s3_bucket" "pathnex_bucket" {
  bucket = "pathnex-bucket"
  versioning {
    enabled = true
  }

  logging {
    target_bucket = "pathnex-log-bucket"
    target_prefix = "logs/"
  }
}
# Kubernetes — Ingress with Nginx Controller
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: pathnex-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
    - host: pathnex.local
      http:
        paths:
        - path: /
          pathType: Prefix
          backend:
            service:
              name: pathnex-service
              port:
                number: 80
# Jenkinsfile — Build, Test, and Deploy with Stages
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building Docker image...'
                docker.build('pathnex-web-app')
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
                    sh 'kubectl apply -f kubernetes/deployment.yaml'
                }
            }
        }
    }
}
# GitLab CI/CD — Multi-Stage Deployment with Helm
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
    - helm upgrade --install pathnex-nginx pathnex/nginx-ingress


# Docker
# CMD vs ENTRYPOINT
FROM ubuntu
ENTRYPOINT ["echo"]
CMD ["Hello Pathnex"]