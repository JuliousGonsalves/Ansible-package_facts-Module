## Description


A shell installation command in linux will install pacake whenever the playboook is installed. 
So Here we are using "package_facts" ansible module to check whether a package is installed in a server and if not then install it.


## prerequisite for this project

1. Two Instances ( One with Ansible and other as a test server)
2. Basic knowledge in Ansible 

## Ansible Installation in Master server
~~~sh
amazon-linux-extras install ansible2 -y
~~~
## Playbook
~~~sh
---

- name: "Listing packages using package_facts"
  hosts: test
  become: true
  tasks:
    - name: "listing docker package in a instance"
      package_facts:
        manager: auto
        strategy: all

    - name: "checking for docker package"
      when: "'docker' in ansible_facts.packages"
      debug:
        msg: "Docker is available in server"

    - name: "Installing docker if not available"
      when: "'docker' not in ansible_facts.packages"
      shell: amazon-linux-extras install docker -y
~~~

## Syntax check
~~~sh
ansible-playbook -i hosts get_package.yml --syntax-check
~~~
## Playbook run
~~~sh
ansible-playbook -i hosts get_package.yml 
~~~

## First Run
![firstrun](https://user-images.githubusercontent.com/98936958/157738947-81df90ae-1d66-4acd-9d3f-c5b9d4a11901.PNG)

## Second Run
![secondrun](https://user-images.githubusercontent.com/98936958/157738964-762fd865-c1d8-42f7-97cd-7623a4213e86.PNG)


