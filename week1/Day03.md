Day 03 — Ansible, Terraform & Kubernetes Basics
🔹 Ansible — Install Apache and Start Service
- name: Install and Start Apache
  hosts: all
  become: yes
  tasks:
    - name: Install apache
      yum:
        name: httpd
        state: present

    - name: Start apache
      service:
        name: httpd
        state: started
        enabled: yes


🔹 Terraform — EC2 Instance (t3.medium)
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "PathnexEC2" {
  ami           = "ami-0abcd1234abcd1234"
  instance_type = "t3.medium"
  tags = {
    Name = "Pathnex-T3"
  }
}
🔹 Kubernetes — Create a ReplicaSet with 3 Replicas
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: pathnex-replicaset
spec:
  replicas: 3
  selector:
    matchLabels:
      app: pathnex-app
  template:
    metadata:
      labels:
        app: pathnex-app
    spec:
      containers:
        - name: app
          image: nginx
          ports:
            - containerPort: 80
🔹 Shell Script — User Info
#!/bin/bash
echo "Current user: $(whoami)"
echo "Current user groups: $(groups)"


🔹 Docker
# Docker File for Nginx Web Server
FROM nginx:latest
COPY index.html /usr/share/nginx/html/index.html

# HTML
<h1>Hello Pathnex</h1>

# Bash
# Real Path
/usr/share/nginx/html

# Bash
docker build -t pathnex-nginx .
docker run -d -p 80:80 pathnex-nginx



# Day 03 - Ansible, Terraform & Kubernetes Basics
 # Ansible - Install Apache and start Service
-name: Install and Start Apache
 hosts: all
 become: yes
 tasks:
 - name: Install apache
   yum:
    name: httpd
    state: present

 - name: start apache
   service:
    name: httpd
    state: started
    enable: yes


# Terraform -EC2 Instance (t3.medium)
provider "aws"{
  region = "us-east-1"
}

resource "aws-instance" "PathnexEC2"{
  ami     = "ami-0abcd1234abcd1234"
  instance type = "t3.medium"
  tag = {
    Name = "env"
  }
}

# Kubernetes - Create a ReplicaSet with 3 Replicas
apiVersion: app/v1
kind: ReplicateSet
metadata"
  name: pathnex-replicaset
spec:
 replicas:3
 selector:
  matchLabels:
   app: pathnex-app

 template:
  metadata:
   labels:
    app:pathnex-app
  spec:
   containers:
    - name: app
      image: nginx
      ports:
       - containerPort: 80

#shell script - user Info
#i/bin/bash
echo "Current user: $(whoami)"
echo "Current user group: $(groups)"


#docker
# Docker File for Nginx Web Server
From nginx:latest
Copy index.html /user/share.nginx/html/index.html

# HTML
<h1>Hello Pathnex </h1>

# Bash
# Real Path
/usr/share/nginx/html

# bash
docker build -t pathnex-nginx .
docker run -d -p 80:80 pathnex-nginx


  
