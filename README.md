# ansible-ssh-key-management

Automate SSH key creation and deployment using Ansible, with secure, idempotent management of keys for local and remote servers.

## Purpose
This repository provides Ansible playbooks to:
- Generate RSA SSH key pairs locally with optional passphrases.
- Deploy public keys to remote servers securely.
- Maintain idempotent key management for multiple hosts.
- Easily share variables like username and key passphrase across plays using inventory or playbook vars.

## Requirements
- Ansible >= 2.10
- Python 3 installed on localhost and remote servers
- SSH access to remote servers
- Optional: Ansible inventory file with remote hosts and variables

## How to Use

1. **Clone the repository**
```
git clone https://github.com/yourusername/ansible-ssh-key-management.git
cd ansible-ssh-key-management
```

Edit inventory.ini

Add your remote servers under [remote_servers].

Define variables new_user and new_user_birth to set the SSH key comment and passphrase.

Example:

ini
Copy code
[remote_servers]
target_server ansible_host=44.239.147.194 ansible_user=ubuntu ansible_ssh_private_key_file=/home/ubuntu/.ssh/id_rsa

[all:vars]
new_user=saman
new_user_birth=2000
Tip: The key comment and passphrase are automatically generated as:

Comment: {{ new_user }}

Passphrase: {{ new_user }}_{{ new_user_birth }}

Run the playbook

bash
Copy code
ansible-playbook -i inventory.ini playbook.yml
