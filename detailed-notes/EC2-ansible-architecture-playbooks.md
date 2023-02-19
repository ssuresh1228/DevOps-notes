Created: 2023-02-16 19:53
# Ansible Playbooks: Automating CI 
---
- Make sure to log in as `ansibleMaster` user created during the configuration 
- current path: `/opt/playbooks/`

>[!example] role 1: copyfile.yml
>```
>---
>- hosts: all
>  become: true
>  tasks:
>   - name: copy war file
>     copy:
>      src: /opt/playbooks/webapp/target/webapp.war
>      dest: /opt/apache-tomcat-8.5.56/webapp

>[!example] role 2: debian.yml
>```
>---
>- name: install curl package
>  ansible.builtin.apt:
>   name:"curl"
>   state: present

>[!example] role 3: redhat.yml
>```
>- name: install curl package
>  ansible.builtin.yum:
>   name:"curl"
>   state: present
 
>[!example] ansible-role.yml contents:
>```
>- hosts: all
>  become: true
>  tasks:
>   - name: install curl to test website from CLI on redhat 
>     import_tasks: redhat.yml
>     when: ansible_facts['os_family']\lower == 'redhat'
>   
>   - name: install curl to test website on CLI on debian
>     import_tasks: debian.yml
>     when: ansible_facts['os_family']\lower == 'debian






---
# References
- [[demo-playbook-with-roles|playbook with roles]]
- [[demo-ansible-playbook-with-modules|playbook with modules]]

## Tags
#ansible-playbook 

---