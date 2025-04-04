# Description
To create a Certified Root Authority in your local lab, you can use this playbook with all default. It will create a subfolder-structure in your current directory with a name "my-root-ca", where everything will be placed, what you need to get a running root-CA-Instance based on openssl. I suggest that you first run the ansible-playbook `01-playbook-create-rootca.yaml` and have a look at the folder structure. Use some of these openssl-commands below in the troubleshooting section to analyze the created Root-CA-Certificate and server-certificate. At a later point feel free to customize the vars in the file `rootca-with-openssl/vars/main.yml` to get your own RootCA up and running.

# Requirements
There are some requirements you must met, to get things running. I will post my configuration.
- It is tested on Rocky-Linux 9.3 running in Windows WSL as a container - Details: Linux myhostname 5.15.133.1-microsoft-standard-WSL2 #1 SMP Thu Oct 5 21:02:42 UTC 2023 x86_64 x86_64 x86_64 GNU/Linux
- It is also tested on RHEL9.2, RHEL9.3
- ansible core 2.14.9 (ansible-core.x86_64 | 1:2.14.9-1.el9 | @appstream)
- python 3.9.18 (python3.x86_64 | 3.9.18-1.el9_3 | @baseos)
- jinja 3.1.2
- OpenSSL 3.0.7 1 Nov 2022 (Library: OpenSSL 3.0.7 1 Nov 2022) (openssl.x86_64 | 1:3.0.7-25.el9_3 | @baseos)

## Create your rootCA
```bash
## Create your RootCA
ansible-playbook 01-playbook-create-rootca.yaml
```

## Create a SSL-Server-Certificate, Private-Key and CSR by only adding a dns-name
```bash
## Create a SSL-Certificate, Private-Key and CSR
ansible-playbook 02-playbook-create-ssl-server-certificate.yaml -e "dnsname=test-server serverip=192.168.1.100"
ansible-playbook 02-playbook-create-ssl-server-certificate.yaml -e "dnsname=example-server serverip=192.168.1.101"

# Output
my-root-ca/new-created-ssl-certs:
-rw-r--r-- 1 root root 1472 Apr 20 13:14 test-server.crt
-rw-r--r-- 1 root root  985 Apr 20 13:14 test-server.csr
-rw------- 1 root root 1874 Apr 20 13:14 test-server.key
```

## Create a wildcard certificate

```bash
## Create a Wildcard-SSL-Certificate, Private-Key and CSR
ansible-playbook 02-playbook-create-ssl-server-certificate.yaml -e "dnsname=wildcard-server serverip=192.168.1.100 alt3=*.wildcard-server.home.local"


```


## Troubleshoot your CA

```bash
## PWD
# /root/git/rootca-with-openssl/ansible

# See your Root-CA-Certificate
openssl x509 -noout -text -in my-root-ca/rootca/pi-rootca.crt

# See your SSL-Server-Certificate
openssl x509 -noout -text -in my-root-ca/new-created-ssl-certs/patricks-server.crt

# Verify or Validate if your ssl-certificate is trusted by your CA
openssl verify -CAfile my-root-ca/rootca/pi-rootca.crt my-root-ca/new-created-ssl-certs/patricks-server.crt
```