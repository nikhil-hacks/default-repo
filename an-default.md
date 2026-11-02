inventory.ini ---->
[webservers]
192.168.1.10
192.168.1.11

[webservers:vars]
ansible_user=ubuntu
ansible_become=true

playbook ---->

---
- name: User, File and Service Management
  hosts: webservers
  become: yes

  tasks:

    # USER MANAGEMENT
    - name: Create user
      ansible.builtin.user:
        name: developer
        state: present
        shell: /bin/bash

    # FILE MANAGEMENT
    - name: Create directory
      ansible.builtin.file:
        path: /opt/myapp
        state: directory
        owner: developer
        mode: '0755'

    - name: Create file
      ansible.builtin.file:
        path: /opt/myapp/index.html
        state: touch
        owner: developer
        mode: '0644'

    # SERVICE MANAGEMENT
    - name: Start Apache service
      ansible.builtin.service:
        name: apache2
        state: started
        enabled: yes
