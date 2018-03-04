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

    config.vm.define "jenkins" do |jenkins|
        jenkins.vm.box = "centos/7"
        jenkins.vm.hostname = "jenkins.ciservice.int"
        jenkins.vm.network "private_network", ip: "192.168.60.100"
        jenkins.vm.provider :virtualbox do |vb|
            vb.customize ["modifyvm", :id, "--memory", "1024"]
            vb.customize ["modifyvm", :id, "--cpus", "1"]
            vb.name = "ci-service-jenkins"
        end
    end
  
    config.vm.define "gitlab" do |gitlab|
        gitlab.vm.box = "centos/7"
        gitlab.vm.hostname = "gitlab.ciservice.int"
        gitlab.vm.network "private_network", ip: "192.168.60.101"
        gitlab.vm.provider :virtualbox do |vb|
            vb.customize ["modifyvm", :id, "--memory", "2048"]
            vb.customize ["modifyvm", :id, "--cpus", "2"]
            vb.name = "ci-service-gitlab"
        end
    end
    
    config.vm.define "sonarqube" do |sonarqube|
        sonarqube.vm.box = "centos/7"
        sonarqube.vm.hostname = "sonarqube.ciservice.int"
        sonarqube.vm.network "private_network", ip: "192.168.60.102"
        sonarqube.vm.provider :virtualbox do |vb|
            vb.customize ["modifyvm", :id, "--memory", "2048"]
            vb.customize ["modifyvm", :id, "--cpus", "1"]
            vb.name = "ci-service-sonarqube"
        end
    end
    
    config.vm.define "nexus" do |nexus|
        nexus.vm.box = "centos/7"
        nexus.vm.hostname = "nexus.ciservice.int"
        nexus.vm.network "private_network", ip: "192.168.60.103"
        nexus.vm.provider :virtualbox do |vb|
            vb.customize ["modifyvm", :id, "--memory", "1024"]
            vb.customize ["modifyvm", :id, "--cpus", "1"]
            vb.name = "ci-service-nexus"
        end
    end

    config.vm.define "slave" do |slave|
        slave.vm.box = "centos/7"
        slave.vm.hostname = "slave.ciservice.int"
        slave.vm.network "private_network", ip: "192.168.60.104"
        slave.vm.provider :virtualbox do |vb|
            vb.customize ["modifyvm", :id, "--memory", "2048"]
            vb.customize ["modifyvm", :id, "--cpus", "2"]
            vb.name = "ci-service-slave"
        end
    end

end