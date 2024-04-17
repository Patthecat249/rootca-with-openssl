# rootca-with-openssl
This repository includes an Ansible Playbook and a Role to create a rootCA with Openssl. Under the folder examples, there are usefull ansible-playbook-examples to create a rootCA und SSL-Server-Certificates.

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
- Manipulate the `main.yaml` in the folder `vars` or
- Overwrite the default-vars in the example-playbooks

## Default Username and Password after Installation on SANNAV Management Portal
```bash
user=Administrator
pass=password

change_to=sannav24
```

## How to replace Certificates
Execute:
```bash
/sannav/binaries/Portal_2.2.2a_bld038/bin/replace-sannav-certificates.sh

# requirements

# Server-Certificate and Key
[root@sannav demo-CA]# ll /sannav/demo-CA/new-created-ssl-certs/serverLA.*
-rw-r--r-- 1 root root 1619 Feb  2 07:29 /sannav/demo-CA/new-created-ssl-certs/serverLA.crt
-rw-r--r-- 1 root root 1086 Feb  2 07:29 /sannav/demo-CA/new-created-ssl-certs/serverLA.csr
-rw------- 1 root root 1874 Feb  2 07:29 /sannav/demo-CA/new-created-ssl-certs/serverLA.key

# RootCA and key
[root@sannav demo-CA]# ll /sannav/demo-CA/rootca/*
-rw-r--r-- 1 root root 1241 Feb  2 07:29 /sannav/demo-CA/rootca/serverLA-rootca.crt
-rw------- 1 root root 1874 Feb  2 07:29 /sannav/demo-CA/rootca/serverLA-rootca.key
-rw-r--r-- 1 root root   41 Feb  2 07:29 /sannav/demo-CA/rootca/serverLA-rootca.srl
```

### BASH-Output
```bash
[root@sannav bin]# ./replace-sannav-certificates.sh
You are about to change the SSL certificates for SANnav. Ensure the following requirements are met before you proceed.
        1. Ensure the Common Name (CN) of the certificate matches the Fully Qualified Domain Name (FQDN) of the host.
        2. If you have root and intermediate CA certificates, chain them into a single certificate.(cat intermediate.cer root.cer > chained.cer)
        3. Have the password for the private key you are planning to replace with.
After importing the certificates successfully, the server will be restarted. After the server is up, it is recommended to un-monitor and re-monitor all the switches that have telemetry enabled for the new certificates to take effect.
Press Enter to proceed if all the requirements are met.

Enter the path for the chained CA certificate including the file name (If you have an intermediate certificate chain the same with root and provide the path including file name.) :
# Use the rootca-Certificate
/sannav/demo-CA/rootca/serverLA-rootca.crt

Enter the path for the private key including the file name :
# Use the private key of Server Certificate
/sannav/demo-CA/new-created-ssl-certs/serverLA.key

Enter the password for private key (/sannav/demo-CA/new-created-ssl-certs/serverLA.key). If the private key is not password protected, press Enter :

Enter the path for the SSL certificate to be installed on sannav including the file name. Ensure that the Common Name of the certificate matches the FQDN of the host sannav.
# Use the Server Certificate
/sannav/demo-CA/new-created-ssl-certs/serverLA.crt

Successfully validated the certificate and the private key.
Stopping the server to apply the certificates.
Stopped the server to apply the certificates.
Starting the server to apply the certificates.

SANnav Management Portal server has been successfully started.

SANnav Management Portal server startup may take up to 15 minutes.

To check SANnav Management Portal server status, run /sannav/binaries/Portal_2.2.2a_bld038/bin/check-sannav-status.sh

When startup has completed, launch the client using [https://10.0.249.68].
```