# Ansible for Lavanet Services

This repository contains Ansible playbooks and roles dedicated to managing and automating the deployment and configuration of Lavanet services. By leveraging Ansible, an open-source automation tool, we aim to simplify the provisioning, configuration management, application deployment, and orchestration of Lavanet's services across different environments.

## Overview

Lavanet services are deployed in various environments, notably `testnet` and `staging`, requiring consistent and reproducible management methods to ensure systems are configured to our standards. This repository offers a suite of Ansible scripts designed for these purposes, alongside planned integration with GitHub Actions for automated workflows.

## Prerequisites

Before proceeding, ensure you have:

- Ansible 2.9 or newer.
- SSH access to the servers under management.
- Appropriate permissions to execute Ansible commands on target servers.
  - Make sure root users are not promoted for password:
    ```shell
    echo "$USER ALL=(ALL:ALL) NOPASSWD: ALL" | sudo tee /etc/sudoers.d/dont-prompt-$USER-for-sudo-password
    echo "ubuntu ALL=(ALL:ALL) NOPASSWD: ALL" | sudo tee /etc/sudoers.d/dont-prompt-ubuntu-for-sudo-password
    ```

## Getting Started

1. Clone this repository:
   ```bash
   git clone https://github.com/yourusername/lavanet-ansible.git
   ```
2. Update the `inventory` file with your servers' IP addresses or hostnames.
3. Customize the playbooks and roles within the `playbooks` and `roles` directories as needed.

## Running the Playbooks

Deploy or update Lavanet services with the following command:

```bash
ansible-playbook -i inventory playbooks/<playbook_name>.yml
``` 

Examples with additional switches:

```bash
 ansible-playbook  -i inventory/list.ini pre-run.yml  --private-key=~/.ssh/lava --diff --ask-vault-pass
``` 
**-i inventory/nodes**  -select the inventory file you want playbook to be run on
**pre-run.yml** - select the playbook you want to run
**--private-key=~/.ssh/lava** - use this ssh key to authorise to the machine(you can use yours)
**--diff** - displays the diff betwen curent state and incoming change
**--ask-vault-pass** - if you have anything encrypted with ansible vault, this will ask to input it

Ensure you replace <playbook_name> with the appropriate playbook for your target deployment.

## Structure

- **`inventory`**: Inventory files defining server groups and roles.
- **`playbooks`**: Playbooks for deploying and managing services.
- **`roles`**: Reusable roles for tasks and configurations.
  - `bootstrap`: Preparing servers for deployment.
  - `consumer`: Installing necessary consumer components.
  - `go`: Settinggo for the current setup.
  - `lavavisor`: Configuring lavavisor services.
  - `nginx`: Configuring default nginx.
  - `sshd`: Adding ssh keys and fixing.

## Task List

- [X] Create this readme
- [X] Create a bootstrap role for server preparation.
- [X] Crate a go installation with version pinining
- [X] Lavaviosr installation role 
- [X] Create sshd bootstrap role
- [X] Add wallet installation support
- [X] Create a iprpc installation under consumer.
- [ ] Hardening role needs to be updated fallowing this instructions [SSH Cryptographic Policy](https://www.ssh.com/academy/ssh/sshd_config#~Cryptographic%20policy)
- [ ] Create a gatewat installation under consumers.
- [ ] Create a docker installation role.
- [ ] Create a node installation role.
- [ ] Create a provider installation role.
- [ ] Integrate with GitHub Actions for CI/CD.
- [ ] Define workflows for testnet and staging environments in GitHub Actions.