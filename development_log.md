# Dev log

Check repo list
```
yum repolist
```

Check Ansible modules
```
ansible-doc -l
```

New submodule creation
1. Create new repository
2. Add submodule in project repository
```
git su
```

Retry execution of playbook while working on it
```
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

Check what is the source repository from which the package was installed
```
yum list installed | grep httpd
yum info httpd 
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
