# Virtualbox based machine for Magento 2 development
Virtual machine environment based on VirtualBox, Vagrant and Ansible for Magento 2 development.

## What's inside?
- Based on [centos/7](https://app.vagrantup.com/centos/boxes/7) box
    - Python 2.7
- Defaults: 
    - Ansible (local) 2.x installed 
    - Machine "webapp":
        - private_network, ip: 192.168.33.10
        - 2 CPU, 4096MB of memory
        - SSH on port 22
- Epel and Remi's RPM repositories
- Common tools: `htop`, `vim`, `nano`, `mc`, `lsof`, `wget`, `zip`, `unzip`, `nc`
- GIT 2.9
- SELinux disabled
- Apache 2.4
- PHP 7.2 with PHP-FPM
    - memory_limit: 1.5G
    - opcache_memory_consumption: '512MB'
- Composer (global)
- Xdebug for PHP 7.2 on port 9000
- MySQL 5.7 on port 3306
    - mysql_innodb_buffer_pool_size: 512MB
- Redis 5.0 on port 6379, 3 databases by default
- RabbitMQ 3.7 and it's dependency Erlang 21.3
- MailCatcher (not started by default)
- Siege 4.0.2
- Java 1.8
- ElasticSearch 6 on port 9200
    - Cluster health under: `http://magento23ee.local:9200/_cluster/health`
- Magento 2.3 Commerce (Community is available, just use ansible-role-magento23-community)
    - Frontend: https://magento23ee.local/
    - Backend: https://magento23ee.local/admin (default admin user: `admin`, password: `Admin12`)
    - Optional sample data
    - Creates `magento23ee` MySQL database, user `magento23ee`, password `magento`
    - Consumes 3 Redis databases 0, 1 and 2

## Prerequisities
- Git
- rsync (or rsync.exe) on the path
- Vagrant ver. >= 2.0
- Virtual Box ver. >= 2.0

## Tested on
- Virtual Box 6.0.10, Vagrant 2.2.5, Ansible 2.7.6, ContOS 7 build 1905.1
- Virtual Box 6.0.4, Vagrant 2.2.3, Ansible 2.7.6, ContOS 7 build 1812.01
- Virtual Box 6.0.2, Vagrant 2.2.3, Ansible 2.7.6, ContOS 7 build 1812.01

## Installation
1. Install VirtualBox Guest Additions plugin
    ```
    vagrant plugin install vagrant-vbguest
    ```
2. Clone repository, pull sub-modules and start provisioning
    ```
    git https://github.com/budnerp/ansible_virtualbox_vm_magento2.git
    git submodule init
    git submodule update
    ```
3. Provide Magento 2 repository credentials (magento_public_key, magento_private_key).
    ```
    vim provisioning/roles/ansible_role_magento23_commerce/defaults/main.yml
    ```
    If you want to install sample data, set `magento_sampledata_install: '1'` in above yaml.
4. Run the machine
    ```
    vagrant up
    ```
5. Set a domain in your hosts file (add a line in C:\Windows\System32\drivers\etc\hosts). Refer to Vagrantfile's web.vm.hostname configuration. Example:
    ```
    192.168.33.10 magento23ee.local
    ```
6. Validate if Magento is installed:
    ```
    https://magento23ee.local
    ```
7. SSH into the instance. Execute:
    ```
    vagrant ssh
    ```
8. Setup GIT config (if ansible-role-git is a part of playbook)
    ```
    $ git config --global user.name "John Doe"
    $ git config --global user.email johndoe@example.com
    ```

## MailCatcher
1. Set a domain in your hosts file (add a line in C:\Windows\System32\drivers\etc\hosts). Refer to Vagrantfile's web.vm.hostname configuration. Example:
    ```
    192.168.33.10 mailcatcher.local
    ```
2. SSH into the instance. Execute:
    ```
    vagrant ssh
    ```
3. Start the service
    ```
    sudo systemctl start mailcatcher.service
    ```
4. Validate MailCatcher service. Example:
    ```
    http://mailcatcher.local:1080
    ```

## Troubleshooting
#### Magento credentials issue
If provisioning ended up with error with Magento credentials add them in file:
```
provisioning/roles/ansible_role_magento23_commerce/defaults/main.yml
```
and re-provision the VM
```
vagrant rsync
vagrant provision
```

#### Vagrant files on VM does not reflect local repository
If you made changes on host machine (eg. changed roles, Vagranfile etc.) run
```
vagrant rsync
```
or upload files manually (eg. via GUI like PhpStorm)
   
#### Guest Addons. Discrepancies between versions od VirtualBox and Guest Additions   
Uninstall vagrant-vbguest plugin and install it back again.
```
vagrant plugin uninstall vagrant-vbguest
vagrant plugin install vagrant-vbguest
```

## Links
- VirtualBox Guest Additions [https://www.vagrantup.com/docs/virtualbox/boxes.html#virtualbox-guest-additions]()
- Guest Additions manual [https://www.virtualbox.org/manual/ch04.html]()
- vagrant-vbguest repository [https://github.com/dotless-de/vagrant-vbguest]() 
- Git Tools - Submodules [https://git-scm.com/book/en/v2/Git-Tools-Submodules]()
- Basic writing and formatting syntax [https://help.github.com/articles/basic-writing-and-formatting-syntax/]()
- Latest configuration ansible.cfg in source control [https://raw.githubusercontent.com/ansible/ansible/devel/examples/ansible.cfg]()
- 7 Tips To Turbo-charge Your Ansible [https://shadow-soft.com/turbo-charge-your-ansible/]()

## License
Copyright (c) We Are Interactive under the MIT license.
