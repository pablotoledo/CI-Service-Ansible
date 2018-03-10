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

    config.vm.define "controller" do |h|
        h.vm.box = "centos/7"
        h.vm.hostname = "controller.ciservice.int"
        h.vm.network "private_network", ip: "192.168.60.105"
        h.vm.provider :virtualbox do |vb|
            vb.customize ["modifyvm", :id, "--memory", "1024"]
            vb.customize ["modifyvm", :id, "--cpus", "2"]
            vb.name = "ci-service-controller"
        end
        h.vm.provision "shell", inline: <<-SHELL
            sudo yum install -y epel-release
            sudo yum install -y ansible
        SHELL
        h.vm.provision "shell", inline: <<-SHELL 
            sudo bash -c "cat /etc/ssh/sshd_config | sed -i '/PasswordAuthentication no/c\PasswordAuthentication yes' > cat /etc/ssh/sshd_config"
            sudo systemctl restart sshd
        SHELL
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
        h.vm.provision "shell", inline: <<-SHELL 
            sudo bash -c "cat /etc/ssh/sshd_config | sed -i '/PasswordAuthentication no/c\PasswordAuthentication yes' > cat /etc/ssh/sshd_config"
            sudo systemctl restart sshd
        SHELL
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
        h.vm.provision "shell", inline: <<-SHELL 
            sudo bash -c "cat /etc/ssh/sshd_config | sed -i '/PasswordAuthentication no/c\PasswordAuthentication yes' > cat /etc/ssh/sshd_config"
            sudo systemctl restart sshd
        SHELL
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
        h.vm.provision "shell", inline: <<-SHELL 
            sudo bash -c "cat /etc/ssh/sshd_config | sed -i '/PasswordAuthentication no/c\PasswordAuthentication yes' > cat /etc/ssh/sshd_config"
            sudo systemctl restart sshd
        SHELL
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
        h.vm.provision "shell", inline: <<-SHELL 
            sudo bash -c "cat /etc/ssh/sshd_config | sed -i '/PasswordAuthentication no/c\PasswordAuthentication yes' > cat /etc/ssh/sshd_config"
            sudo systemctl restart sshd
        SHELL
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
        h.vm.provision "shell", inline: <<-SHELL 
            sudo bash -c "cat /etc/ssh/sshd_config | sed -i '/PasswordAuthentication no/c\PasswordAuthentication yes' > cat /etc/ssh/sshd_config"
            sudo systemctl restart sshd
        SHELL
    end

end