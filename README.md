# rootca-with-openssl
This repository includes an Ansible Playbook folder called `ansible` with two playbooks it it and a Ansible-Role-folder `rootca-with-openssl` to create a rootCA with Openssl on a linux system. Under the folder `ansible`, there are two ansible-playbooks. The first one `01-playbook-create-rootca.yaml` is to create a rootCA. The seconds one `02-playbook-create-ssl-server-certificate.yaml` helps you with your day-2-operation tasks, when you will create custom-ssl-server-certificates.

# How to Use
```bash
# Create a folder and clone the git-repo
mkdir git && cd git
git clone https://github.com/Patthecat249/rootca-with-openssl.git

# Change to ansible-directory
cd rootca-with-openssl/ansible

# Execute the Playbook
ansible-playbook 01-playbook.yaml
```

# How it works
After you cloned the repository, you can run the playbook as described. It will create a rootCA, with private-Key, all sub-folders/working-folder you need for a rootCA. Then it creates a ssl-server-certificate.

Please have a look in the examples folder. Feel free to edit the vars to your needs.

## How to customize
If you want to change the Subject, the private key, or the folder, where everything will be created, feel free to use these ways for editing:
- Manipulate the `main.yaml` in the folder `vars` in the Ansible-Role-Folder `rootca-with-openssl`

# Disclaimer
This Setup is only tested in a lab environment and not in production state. It is more a learning experience project than a prduction-ready installation. The project was instantiated by the will of learning more about the SSL-Technology. 