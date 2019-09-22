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

    config.vm.synced_folder ".", "/vagrant"#, disabled: true

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
    sudo bash -c "sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config"
    sudo systemctl restart sshd
        
    #
    # Update and install basic linux programs for development
    #
    sudo yum update -y

    #
    # Install Ansible
    # 
    sudo yum install -y epel-release
    sudo yum install -y ansible nano
SCRIPT


    config.vm.define "ci-service-env" do |h|
        h.vm.box = "centos/7"
        h.vm.hostname = "ciservice.int"
        h.vm.network "private_network", ip: "192.168.10.100"
        h.vm.provider :virtualbox do |vb|
            vb.customize ["modifyvm", :id, "--memory", "8096"]
            vb.customize ["modifyvm", :id, "--cpus", "2"]
            vb.name = "ci-service-env"
        end
        
        # Configures new ssh key for server and creates a copy for the rest of the servers.
        h.vm.provision "shell", inline: $script_generate_ssh_key 

        # Install Ansible in control server  
        h.vm.provision "shell", inline: $script_install_ansible

        # Copy ansible playbook and roles. 
        h.vm.provision "file", source: "./ansible/" , destination: "$HOME/"


    end

end