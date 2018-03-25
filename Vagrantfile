# -*- mode: ruby -*-
# vi: set ft=ruby :

# README
#
# Getting Started:
# 1. vagrant plugin install vagrant-hostmanager
#       If you are running this Vagrantfile behind a corporate proxy: 
#           vagrant plugin install vagrant-proxyconf
# 2. vagrant up
# 3. vagrant ssh
#
# This should put you at the control host
#  with access, by name, to other vms
Vagrant.configure("2") do |config|
    
    config.hostmanager.enabled = true

    config.vm.synced_folder ".", "/vagrant", type: "virtualbox", disabled: false,
    rsync__exclude: ".git/"

    $script_generate_ssh_key = <<SCRIPT
    echo Updateing credentials
    if [ ! -f /home/vagrant/.ssh/id_rsa ]; then
          ssh-keygen -t rsa -N "" -f /home/vagrant/.ssh/id_rsa
    fi
         cp /home/vagrant/.ssh/id_rsa.pub /vagrant/control.pub

         cat << 'SSHEOF' > /home/vagrant/.ssh/config
     Host *
     StrictHostKeyChecking no
     UserKnownHostsFile=/dev/null
SSHEOF
        chown -R vagrant:vagrant /home/vagrant/.ssh/
SCRIPT

    $script_copy_key = 'cat /vagrant/control.pub >> /home/vagrant/.ssh/authorized_keys'

    $script_install_ansible = <<SCRIPT
        echo Installin ansible.
        
    #
    # Update and install basic linux programs for development
    #
    sudo yum update -y
    sudo yum install -y wget
    sudo yum install -y curl
    sudo yum install -y vim
    sudo yum install -y git
    sudo yum install -y build-essential
    sudo yum install -y unzip
    #
    # Install Ansible
    # 
    sudo yum install -y epel-release
    sudo yum install -y ansible nano

SCRIPT


    config.vm.define "controller" do |h|
        h.vm.box = "centos/7"
        h.vm.hostname = "controller.ciservice.int"
        h.vm.network "private_network", ip: "192.168.60.105"
        h.vm.provider :virtualbox do |vb|
            vb.customize ["modifyvm", :id, "--memory", "1024"]
            vb.customize ["modifyvm", :id, "--cpus", "2"]
            vb.name = "ci-service-controller"
        end
        
        # Configures new ssh key for server and creates a copy for the rest of the servers.
        h.vm.provision "shell", inline: $script_generate_ssh_key 

        # Install Ansible in control server  
        h.vm.provision "shell", inline: $script_install_ansible

        # Copy ansible playbook and roles. 
        h.vm.provision "file", source: "./ansible/" , destination: "$HOME/"


    end
    
    config.vm.define "jenkins" do |h|
        h.vm.box = "centos/7"
        h.vm.hostname = "jenkins.ciservice.int"
        h.vm.network "private_network", ip: "192.168.60.100"
        h.vm.provider :virtualbox do |vb|
            vb.customize ["modifyvm", :id, "--memory", "1024"]
            vb.customize ["modifyvm", :id, "--cpus", "1"]
            vb.name = "ci-service-jenkins"
        end

        # Copy ssh key from control server  
        h.vm.provision 'shell', inline: $script_copy_key
    end
  
    config.vm.define "gitlab" do |h|
        h.vm.box = "centos/7"
        h.vm.hostname = "gitlab.ciservice.int"
        h.vm.network "private_network", ip: "192.168.60.101"
        h.vm.provider :virtualbox do |vb|
            vb.customize ["modifyvm", :id, "--memory", "2048"]
            vb.customize ["modifyvm", :id, "--cpus", "2"]
            vb.name = "ci-service-gitlab"
        end
        
        # Copy ssh key from master 
        h.vm.provision 'shell', inline: $script_copy_key
    end
    
    config.vm.define "sonarqube" do |h|
        h.vm.box = "centos/7"
        h.vm.hostname = "sonarqube.ciservice.int"
        h.vm.network "private_network", ip: "192.168.60.102"
        h.vm.provider :virtualbox do |vb|
            vb.customize ["modifyvm", :id, "--memory", "2048"]
            vb.customize ["modifyvm", :id, "--cpus", "2"]
            vb.name = "ci-service-sonarqube"
        end

        # Copy ssh key from master 
        h.vm.provision 'shell', inline: $script_copy_key
    end
    
    config.vm.define "nexus" do |h|
        h.vm.box = "centos/7"
        h.vm.hostname = "nexus.ciservice.int"
        h.vm.network "private_network", ip: "192.168.60.103"
        h.vm.provider :virtualbox do |vb|
            vb.customize ["modifyvm", :id, "--memory", "1024"]
            vb.customize ["modifyvm", :id, "--cpus", "1"]
            vb.name = "ci-service-nexus"
        end

        # Copy ssh key from master 
        h.vm.provision 'shell', inline: $script_copy_key
    end

    config.vm.define "slave" do |h|
        h.vm.box = "centos/7"
        h.vm.hostname = "slave.ciservice.int"
        h.vm.network "private_network", ip: "192.168.60.104"
        h.vm.provider :virtualbox do |vb|
            vb.customize ["modifyvm", :id, "--memory", "2048"]
            vb.customize ["modifyvm", :id, "--cpus", "2"]
            vb.name = "ci-service-slave"
        end

        # Copy ssh key from master 
        h.vm.provision 'shell', inline: $script_copy_key
    end

end