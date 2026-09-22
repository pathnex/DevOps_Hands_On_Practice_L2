# Day 06 — Introduction to CloudFormation and Kubernetes Advanced Concepts

## 🔹 Ansible — Install Docker

```yaml
- name: Install Docker
  hosts: all
  become: yes
  tasks:
    - name: Install Docker
      yum:
        name: docker
        state: present
    - name: Start Docker
      service:
        name: docker
        state: started
        enabled: yes

        
🔹 Terraform — Provisioning EC2 with VPC
resource "aws_vpc" "main" {
  cidr_block = "10.0.0.0/16"
}

resource "aws_instance" "pathnex_ec2" {
  ami           = "ami-0abcd1234abcd1234"
  instance_type = "t3.medium"
  subnet_id     = aws_subnet.main.id
  tags = {
    Name = "Pathnex-EC2"
  }
}
🔹 Kubernetes — Pod with Volume Mount
apiVersion: v1
kind: Pod
metadata:
  name: pathnex-pod
spec:
  containers:
    - name: web
      image: nginx
      volumeMounts:
        - mountPath: /usr/share/nginx/html
          name: html-volume
  volumes:
    - name: html-volume
      hostPath:
        path: /data
        type: Directory
🔹 Shell Script — Check for Running Services
#!/bin/bash
services=("nginx" "docker" "httpd")
for service in "${services[@]}"
do
  if systemctl is-active --quiet $service; then
    echo "$service is running"
  else
    echo "$service is not running"
  fi
done


🔹 Docker
# Node.js Application (JavaScript)
console.log("Hello Pathnex");

# Docker File
FROM node:18
WORKDIR /opt/pathnex/node-app
COPY app.js /opt/pathnex/node-app/
CMD ["node", "/opt/pathnex/node-app/app.js"]

# Real Path
/opt/pathnex/node-app

##Ansible -Install Docker

```yml
-name: Install Docker
 hosts: all
 become: yes
 tasks: 
  - name: Install Docker
    yum:
     name: docker
     state: present
  - name: Start Docker
    service:
     name: docker
     state: started
     enabled: yes

# Terraform -Provisioning EC2 with VPC

resource "aws-vpc" "main"{
 cidr_block = "10.0.0.0/16"}

resource "aws_instance" "pathnex_ec2"{
ami     ="ami-0abcd1234abcd1234"
instance_type= "t3.medium"
subnet_id. = aws_subnet.main.id
tags={
Name = "pathnex-ec2"}}

# Kubernetes - Pod with Volume Mount
apiVersion: v1
kind: pod
metadata:
 name: pathnex-pod
spec:
 containers:
  -name: web
  image: nginx
  volumeMounts:
   -mountPath: /usr/share/nginx/html
    name: html-volume
volumes:
 - name: html-volume
   hostPath:
    path: /data
    type: Directory

#shell Script - Check For running Services
#!/bin/bash
services=("nginx" "docker" "httpd")
for service in "${services[@]}"
do
if systemctl is-active -- quiet $service; then
  echo "$service is running"
else
  echo "$service is not running"
 fi
 done

#Docker
#Node.js Application (javascript)
console.log("Hello Pathnex");

#Docker File
From node:18
WORKDIR /opt/pathnex/node-app
COPY app.js /opt/pathnex/node-app/
CMD ["node", "/opt/pathnex/node-app/app.js"]

