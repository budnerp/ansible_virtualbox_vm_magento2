# Vagrant and Ansible
VirtualBox virtual machine environment integrated with Vagrant and Ansible.

## What's inside?

- based on [centos/7](https://app.vagrantup.com/centos/boxes/7) Vagrant box

## Requirements

- Vagrant >= 2.0

## Installation
- Install VirtualBox Guest Additions plugin
```shell
vagrant plugin install vagrant-vbguest
```
- Clone repository, pull sub-modules and start provisioning
```
git clone https://github.com/budnerp/vagrant_ansible.git
git submodule init
git submodule update
vagrant up
```
- Set a domain in your hosts file (add a line in C:\Windows\System32\drivers\etc\hosts). Refer to Vagrantfile's web.vm.hostname configuration. Example:
```
192.168.33.222 webapp.development
```
- Validate www server. Example:
```
http://webapp.development
```
- SSH into the instance. Execute:
```
vagrant ssh webapp
```

## Links
- VirtualBox Guest Additions [https://www.vagrantup.com/docs/virtualbox/boxes.html#virtualbox-guest-additions]()
- Guest Additions manual [https://www.virtualbox.org/manual/ch04.html]()
- vagrant-vbguest repository [https://github.com/dotless-de/vagrant-vbguest]() 
- Basic writing and formatting syntax [https://help.github.com/articles/basic-writing-and-formatting-syntax/]()

## License
Copyright (c) We Are Interactive under the MIT license.

