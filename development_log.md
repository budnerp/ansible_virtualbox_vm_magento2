# Dev log

#####Initialize Vagrantfile with CentOS 7 
[https://app.vagrantup.com/centos/boxes/7]()
``` 
vagrant init centos/7
```

#####Check repo list on centos
```
vagrant ssh webapp
yum repolist
```

#####Check Ansible modules
```
ansible-doc -l
```

#####New submodule creation
1. Create new repository
2. Add submodule in project repository
```
git submodule add https://github.com/budnerp/ansible_role_apache2.git ansible_role_apache2
```

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
