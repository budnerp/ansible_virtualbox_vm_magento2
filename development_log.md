# Dev log

####27.01.2019
Initialize Vagrantfile with CentOS 7 [https://app.vagrantup.com/centos/boxes/7]()
``` 
vagrant init centos/7
```
Add initial VM configuration

Check repo list in webapp VM. Expecting EPEL repo to be in a list.
```
vagrant ssh webapp
yum repolist
```

Check Ansible modules
```
ansible-doc -l
```
