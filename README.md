# Vagrant and Ansible
VirtualBox virtual machine environment integrated with Vagrant and Ansible.

## What's inside?
- Based on [centos/7](https://app.vagrantup.com/centos/boxes/7) box
- Defaults: 
    - Ansible (local) 2.x installed 
    - Machine "webapp":
        - private_network, ip: 192.168.33.10
        - 1 CPU, 1024MB of memory
        - SSH on port 22

## Prerequisities
- Git
- rsync (or rsync.exe) on the path
- Vagrant ver. >= 2.0
- Virtual Box ver. >= 2.0

Tested on:
- Virtual Box 6.0.4 and Vagrant 2.2.3
- Virtual Box 6.0.2 and Vagrant 2.2.3

## Installation
1. Install VirtualBox Guest Additions plugin
    ```
    vagrant plugin install vagrant-vbguest
    ```
2. Clone repository, pull sub-modules and start provisioning
    ```
    git clone https://github.com/budnerp/vagrant_ansible.git
    git submodule init
    git submodule update
    vagrant up
    ```
3. Set a domain in your hosts file (add a line in C:\Windows\System32\drivers\etc\hosts). Refer to Vagrantfile's web.vm.hostname configuration. Example:
    ```
    192.168.33.10 webapp.development
    ```
4. Validate www server. Example:
    ```
    http://webapp.development
    ```
5. SSH into the instance. Execute:
    ```
    vagrant ssh webapp
    ```

## Troubleshooting
#### Guest Addons. Discrepancies between versions od VirtualBox and Guest Additions   
Uninstall vagrant-vbguest plugin and install it back again.

## Links
- VirtualBox Guest Additions [https://www.vagrantup.com/docs/virtualbox/boxes.html#virtualbox-guest-additions]()
- Guest Additions manual [https://www.virtualbox.org/manual/ch04.html]()
- vagrant-vbguest repository [https://github.com/dotless-de/vagrant-vbguest]() 
- Basic writing and formatting syntax [https://help.github.com/articles/basic-writing-and-formatting-syntax/]()

## License
Copyright (c) We Are Interactive under the MIT license.

