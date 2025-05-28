# DevOps-Ansible-Scripts
DevOps-Ansible-Scripts automates infrastructure management with Ansible playbooks, streamlining server provisioning, configuration, and deployment for efficient DevOps workflows. 🚀


# Ansible Repository

## Introduction
Ansible is an open-source automation tool used for configuration management, application deployment, and task automation. It is agentless, relying on SSH to communicate with remote servers.

### Difference Between Ansible, SaltStack, and Terraform
- **Ansible**: Primarily used for configuration management and automation using YAML-based playbooks.
- **SaltStack**: Designed for infrastructure management and provisioning using a Python-based approach with high scalability.
- **Terraform**: Focused on Infrastructure as Code (IaC), mainly used for provisioning and managing cloud infrastructure.

## Installation on Amazon Linux 2
To install Ansible on an Amazon Linux 2 AMI, follow these steps:

```bash
sudo amazon-linux-extras enable ansible2
sudo yum install -y ansible
ansible --version
```

Configuring the Hosts File
Update the /etc/ansible/hosts file with the following configuration:

```bash
[servers]
server_1 ansible_host=65.0.95.217
server_2 ansible_host=35.154.121.199

[prd]
server_3 ansible_host=13.233.165.122

[all:vars]
ansible_python_interpreter=/usr/bin/python3
ansible_user=ec2-user
ansible_ssh_private_key_file=/home/ec2-user/key/mykp.pem
```


Copying SSH Key to EC2 Instance
To transfer your private key to an EC2 instance, run:

```bash
scp -i .\mykp.pem .\mykp.pem ec2-user@3.110.46.29:/home/ec2-user/key
```
Testing Connectivity
Verify connectivity to configured servers with:

```bash
ansible servers -m ping
ansible servers -a "free -h"
```
Playbooks
Below are the playbooks included in this repository:

1. date_play.yml
Retrieves the system date and uptime for connected servers.

Run Command:

```bash
ansible-playbook date_play.yml
```

2. install_httpd_play.yml
Installs and starts the HTTPD server on port 80.

Run Command:

```bash
ansible-playbook install_httpd_play.yml
```

3. install_nginx_play.yml
Installs and starts Nginx on the production (prd) server.

Run Command:

```bash
ansible-playbook install_nginx_play.yml
```

4. install_nginx_play_8080.yml
Installs Nginx and changes the default port 80 to 8080, since port 80 is already used by HTTPD.

Run Command:

```bash
ansible-playbook install_nginx_play_8080.yml
```

5. web_play.yml
Deploys index.html to multiple servers by copying it to /usr/share/nginx/html and /var/www/html.

Run Command:

```bash
ansible-playbook web_play.yml
```

Expected Output: Once this playbook runs successfully, access the deployed web pages using:

HTTPD Server: http://your_public_ip:80

Nginx Server: http://your_public_ip:8080

