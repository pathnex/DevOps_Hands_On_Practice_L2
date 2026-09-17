# Day 01 — Basics

## 🔹 Ansible Task — Install Nginx on Pathnex Server

Rewrite this YAML manually:

```yaml
- name: Install Nginx on Pathnex server
  hosts: all
  become: yes

  tasks:
    - name: Install nginx
      yum:
        name: nginx
        state: present


🔹 Docker
# Docker Installation & First Container
docker --version
docker run ubuntu echo "Hello Pathnex"


# Docker File
FROM ubuntu:22.04
CMD ["echo", "Hello Pathnex"]



- name: Install Nginx on Deepak Yadav Server
  hosts: all
  become: yes
  
  tasks:
   - name: Install nginx
     yum:
      name: nginx
      state: present

  Docker

  docker --version
  docker run ubuntu echo "Hello Bhai"

  #Docker File
  From ubuntu:22.04
  CMD ["echo","Hello bhai"]
