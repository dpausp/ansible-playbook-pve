Proxmox VE 3.0 Ansible Playbook
===============================

An Ansible Playbook to setup Proxmox VE a Debian 7 machine.
Ansible 1.2 is required.

Install Ansible Dependencies
----------------------------

Install some requirements:

    sudo apt-get install python-jinja2 python-paramiko python-yaml git


Installing Ansible
------------------

Simple installation of a current version via git:
    
    # user installation
    git clone git://github.com/ansible/ansible.git
    cd ./ansible
    source ./hacking/env-setup

Run the _source_ command in new terminals before using the _ansible-playbook_ command.


Playbook Preparation
--------------------

Host Preparation
----------------

The main Playbook needs access via SSH to a user who is able to sudo (with password is ok). To configure a freshly installed Debian machine for proper access, use access.yml.
This playbook creates an admin user.

* configure host for root SSH access via password, if neccessary
* change host, admin\_user and admin\_user\_pubkeyfile in hosts file
* run playbook:

    ansible-playbook -i hosts access.yml -u root -k

Running The Playbook
--------------------

The mail playbook is called all.yml. This will install Proxmox VE and its dependencies. The target host is rebooted once to start the Proxmox linux kernel.

    ansible-playbook -i hosts all.yml -u <admin_user> -Ks

The -K option asks for a sudo password. For passwordless sudo (if allowed), don't specify -K.



