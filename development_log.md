# Dev log

Check repo list
```
yum repolist
yum repolist enabled | grep mysql
```

Check Ansible modules
```
ansible-doc -l
```

New submodule creation
1. Create new repository
2. Navigate to Ansible's role folder 
3. Add submodule in project repository
```
git submodule add https://github.com/budnerp/ansible_role_magento23_commerce.git provisioning/roles/ansible_role_magento23_commerce
```

Removing submodule
```
git submodule deinit -f provisioning/roles/ansible_role_magento23
rm -rf .git/modules/provisioning/roles/ansible_role_java8
git rm -f provisioning/roles/ansible_role_java8
```

Execute playbook inside VM
```
ansible-playbook /vagrant/provisioning/jenkins_playbook.yml -i /vagrant/provisioning/development.yml
ansible-playbook /vagrant/provisioning/webapp_playbook.yml -i /vagrant/provisioning/development.yml
```

Retry execution of playbook while working on it
```
vagrant ssh
cd /vagrant
ansible-playbook provisioning/webapp_playbook.yml -i provisioning/development.yml --limit @/vagrant/provisioning/webapp_playbook.retry
```

List of modules loaded by httpd
1. CentOS
    ```
    httpd -M
    ```
2. Ubuntu/Debian
    ```
    apache2 -M
    ```

Check if a package is available in repositories
1. CentOS
    ```
    yum info php72
    yum search xdebug
    yum repolist all | grep mysql
    ```
2. Ubuntu/Debian
    ```
    apt-cache search php 
    ```

Check server MPM
```
httpd -V
```

Check what is the source repository from which the package was installed
```
yum list installed | grep httpd
yum info httpd 
```

Check PHP loaded modules
```
php --modules
```

Check memory status
```
free -h
```

Python pexpect Ansible tasks
```
  - yum:
      name: http://widehat.opensuse.org/opensuse/distribution/leap/42.3/repo/oss/suse/noarch/python-pexpect-3.3-6.1.noarch.rpm
      state: present
  - yum:
      name: python-pexpect
      state: present
```

To get PHP current `memory_limit` value:
```
php -r "echo ini_get('memory_limit').PHP_EOL;"
```

Increase memory on VM
1. Change values in Vagrant file
    ```
    vb.memory = "2048"
    vb.cpus = 2
    ```
2. Increase PHP memory_limit
    ```
    php_memory_limit: '1024M'
    ```

Check vagrant VM status and remove invalid VMs 
```
vagrant global-status
vagrant global-status --prune
```    

Destroy machine after Vagrant upgrade 2.2.3 to 2.2.5 issues
```
vagrant plugin expunge --reinstall // permanently deletes all currently installed user plugins
```

Pass arguments to Ansible via Vagrant
https://gist.github.com/phantomwhale/9657134

### Issues:
#### Unreachable:
CLI message:
```
TASK [Gathering Facts] *********************************************************
fatal: [webapp]: UNREACHABLE! => {"changed": false, "msg": "Failed to connect to the host via ssh: Host key verification failed.\r\n", "unreachable": true}
        to retry, use: --limit @/vagrant/provisioning/webapp_playbook.retry

PLAY RECAP *********************************************************************
webapp                     : ok=0    changed=0    unreachable=1    failed=0

Ansible failed to complete successfully. Any error output should be
visible above. Please fix these errors and try again.

```
#####Suggestion:
Add extra verbose setting ansible.verbose="vvv"
#####Solution:
1. Make sure inventory file has correct format
2. In case usage of ansible_local provisioner, add following to variables (in playbook or inventory):
    ```
    vars:
        ansible_connection: local
    ```

### Warnings
#### Warnings about inventory
Example of message in CLI:
```
webapp: Running ansible-playbook...
[...]
/vagrant/provisioning/development.yml did not meet host_list requirements, check plugin documentation if this is unexpected
/vagrant/provisioning/development.yml did not meet script requirements, check plugin documentation if this is unexpected
```
#####Suggestion
Add extra verbose setting ansible.verbose="vvv"
#####Solution (?)
```
[inventory]
enable_plugins = yaml
```

###Transition to docker
https://medium.com/inloopx/speeding-up-project-setup-and-development-with-vagrant-db41061363a3

https://www.netcentric.biz/insights/2017/08/aem-and-docker.html
