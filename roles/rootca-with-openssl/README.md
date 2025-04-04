rootca-with-openssl
=========

The Ansible-Role helps you to create a easy setup of a Root-Certified-Authority based on openssl on a linux system.

Requirements
------------

There are some requirements you must met, to get things running. I will post my configuration.
- It is tested on Rocky-Linux 9.3 running in Windows WSL as a container - Details: Linux myhostname 5.15.133.1-microsoft-standard-WSL2 #1 SMP Thu Oct 5 21:02:42 UTC 2023 x86_64 x86_64 x86_64 GNU/Linux
- It is also tested on RHEL9.2, RHEL9.3
- ansible core 2.14.9 (ansible-core.x86_64 | 1:2.14.9-1.el9 | @appstream)
- python 3.9.18 (python3.x86_64 | 3.9.18-1.el9_3 | @baseos)
- jinja 3.1.2
- OpenSSL 3.0.7 1 Nov 2022 (Library: OpenSSL 3.0.7 1 Nov 2022) (openssl.x86_64 | 1:3.0.7-25.el9_3 | @baseos)

Role Variables
--------------

The vars of the role are described in the `main.yml` file of the `vars`-Folder.

Dependencies
------------

There are no dependencies to other roles

Example Playbook
----------------

Use the playbooks in the `ansible` folder.

License
-------

BSD

Author Information
------------------

Have fun with this...
