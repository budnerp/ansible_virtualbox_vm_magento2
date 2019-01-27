# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.require_version ">= 2.0"

Vagrant.configure("2") do |config|
    config.vm.box = "centos/7"

    # If true, Vagrant will automatically insert a keypair to use for SSH,
    # replacing Vagrant's default insecure key inside the machine if detected.
    # By default, this is true.
    config.ssh.insert_key = false

    # config.ssh.forward_agent = true

    config.vm.provision "shell", inline: <<-SHELL
        # Install EPEL repository - Extra Packages for Enterprise Linux 7
        yum -y install epel-release

        # Install Ansible from EPEL repo
        yum -y install ansible
    SHELL

    config.vm.define "webapp", primary: true do |machine|
        machine.vm.hostname = "webapp"
        machine.vm.network "private_network", ip: "192.168.33.10"

        # TODO: Work on Ansible
        #machine.vm.provision :ansible_local do |ansible|
        #    # ansible.verbose = "v"
        #    ansible.playbook = "webapp_playbook.yml"
        #    ansible.compatibility_mode = "2.0"
        #end

        machine.vm.provider "virtualbox" do |vb|
            vb.name = "vagrant_ansible_webapp"
            vb.gui = true
            vb.memory = "1024"
            vb.cpus = 1
        end
    end
end
