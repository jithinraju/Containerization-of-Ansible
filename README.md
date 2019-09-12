# Containerization of Ansible

Here  I am devoloping a docker image to run ansible playbooks without any Ansible or dependecy installation in the local system

I have listed the commands in order 

```bash

touch Dockerfile 

```

I am using Alpine linux as the parent image

```bash

FROM alpine:3.8

RUN apk update
RUN apk add python3
RUN apk add ansible

WORKDIR /playbook/

ENTRYPOINT ["/usr/bin/ansible-playbook"]

```

Working directory for this image is added as /playbook and we are mounting our local directory with necessary files to the image.

#### Creating IMAGE

Run the following command from the directory where Dockerfile is added

```bash

docker build -t ansible .

```

#### Add the following files in common directory

I created a directory as **playbook** and added the following files

- ##### inventory.ini

```bash

[amazon]
Ansible_Client_IP ansible_ssh_port=SSH_port  ansible_ssh_user=SSH_user ansible_ssh_private_key_file=SSH_host_key


```

- ##### ansible.cfg

```bash

[defaults]
inventory = inventory.ini 
host_key_checking = False


```

- ##### Add the SSH private key for the client

#### Run the following command for running the Ansible-playbook in the container

```bash

docker run -v $(pwd)/playbook/:/playbook/  ansible  playbook

```
