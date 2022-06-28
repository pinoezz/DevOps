# CI/CD With Jenkins

Untuk CI/CD Jenkins saya akan jalankan on top docker dan berikut ansible-playbook `jenkins.yml`.


```
- hosts: jenkins
  become: true
  tasks:
  - name: jenkins volume
    file:
     path: /home/jenkins/jenkins_home
     state: directory
     owner: 1000
     group: 1000
  - name: Pull jenkins
    docker_image:
     name: jenkins/jenkins:latest
     source: pull
  - name: Container jenkins
    docker_container:
     name: jenkins
     image: jenkins/jenkins
     ports:
      - 8080:8080
      - 50000:50000
     volumes: /home/jenkins/jenkins_home:/var/jenkins_home
```
