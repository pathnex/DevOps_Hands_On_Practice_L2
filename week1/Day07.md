Day 07 — Automating Cloud Infrastructure with Terraform & Ansible
🔹 Ansible — Setup Nginx with Custom Config
- name: Setup Nginx with Custom Config
  hosts: all
  become: yes
  tasks:
    - name: Install nginx
      yum:
        name: nginx
        state: present
    - name: Copy custom nginx.conf
      copy:
        src: nginx.conf
        dest: /etc/nginx/nginx.conf
    - name: Start nginx service
      service:
        name: nginx
        state: started
        enabled: yes
🔹 Terraform — Provision EC2 with IAM Role
resource "aws_iam_role" "ec2_role" {
  name               = "pathnex_ec2_role"
  assume_role_policy = jsonencode({
    Version = "2012-10-17"
    Statement = [
      {
        Action = "sts:AssumeRole"
        Effect = "Allow"
        Principal = {
          Service = "ec2.amazonaws.com"
        }
      },
    ]
  })
}

resource "aws_instance" "pathnex_ec2" {
  ami           = "ami-0abcd1234abcd1234"
  instance_type = "t2.medium"
  iam_instance_profile = aws_iam_role.ec2_role.name
  tags = {
    Name = "Pathnex-EC2"
  }
}
🔹 Kubernetes — ConfigMap and Secret Management
apiVersion: v1
kind: ConfigMap
metadata:
  name: pathnex-config
data:
  app.properties: |
    key=value

---
apiVersion: v1
kind: Secret
metadata:
  name: pathnex-secret
type: Opaque
data:
  password: cGF0aG5leHBhc3M=
🔹 Shell Script — Archive Logs
#!/bin/bash
tar -czf /var/log/archived_logs.tar.gz /var/log/*.log


🔹 Docker Java Application 
# JavaScript
class Hello {
    public static void main(String[] args) {
        System.out.println("Hello Pathnex");
    }
}

# Docker File
FROM openjdk:17
WORKDIR /opt/pathnex/java-app
COPY Hello.java /opt/pathnex/java-app/
RUN javac /opt/pathnex/java-app/Hello.java
CMD ["java", "-cp", "/opt/pathnex/java-app", "Hello"]


# Day 07 Automating Cloud Infrastructure with terraform & ansible

# ansible - Setup nginx with Custim Config
 -name: Setup Nginx with custom Config
  host: all
  become:yes
  tasks:
   - name: Install nginx
     yum:
      name:nginx
      state: present
   - name: Copy custom nginx.conf
     copy:
      src: nginx.conf
      dest: /etc/nginx/nginx.conf
   - name : Start nginx service
     service:
      name: nginx
      state: started
      enabled: yes

# Terraform - Provision EC2 with IAM Role
resource "aws_iam_role" "ec2_role"{
  name    = "pathnex_ec2_role"
  assume_role_policy = jsonencode({
    Version = "2012-10-17"
    Statement =[
      {
        Action = "sts:AssumeRole"
        Effect = "Allow"
        Principal= {
          Service = "ec2.amazonaws.com"
        }
      }
    ]
  })
}

resource "aws_instance" "pathnex_ec2"{
  ami   = "ami-0abcd1234abcd1234"
  instance_type= "t2.medium"
  iam_instance_profile = aws_iam_role.ec2_role.name
  tags= {
    Name = "Pathnex-ec2"
  }
}

#Kubernets - ConfigMap and Secret Management
apiVersion: v1
kind: ConfigMap
metadata:
 name: pathnex-config
data:
 app.properties: |
  key=value


---
apiVersion: v1
kind: Secret
metadata:
 name: pathnex-secret
type: Opaque
data:
 password: cGF0aG5leHBhc3M=

#shell Script - Archive Logs
#!/bin/bash
tar -czf /var/log/archived_logs.tar.gz/var/log/*.log

# Docker Java application
# javascript
class Hello{
  public static void main(String[] args){
    System.out.printIn("Hello Pathnex");
  }
}

#Docker File
From openjdk:17
WORKDIR /opt/pathnex/java-app
COPY Hello.java /opt/pathnex/java-app/
RUN javac /opt/pathnex/java-app/Hello.java
CMD ["java" , "-cp" "/opt/pathnex/java-app", "Hello"]