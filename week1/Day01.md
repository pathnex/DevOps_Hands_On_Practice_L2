- name: Install Nginx on Pathnex server
  hosts: all
  become: yes

  tasks:
    - name: Install nginx
      yum:
        name: nginx
        state: present
      # Day 01 — Basics

## 🔹 Ansible Task — Install Nginx on Pathnex Server

Rewrite this YAML manually:

```yaml
- name: name: Install Nginx on Pathnex server
  hosts: all
  become: yes

  tasks:
    - name: Install nginx
      yum:
        name: nginx
        state: present
-name: install Ngnix on Pathnex server
hosts: all
become: yes

tasks :
-name Suhail
state present
# Day one bascis learning code
