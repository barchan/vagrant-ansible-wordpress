# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "centos8"
  config.vm.box_check_update = false

  config.vm.define "wordpress"
  config.vm.hostname = "wordpress.test"

  config.ssh.insert_key = false

  config.vm.network "private_network", ip: "192.168.21.33"

  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.synced_folder "wordpress/", "/var/www/wordpress"

  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--memory", 1024]
    vb.customize ["modifyvm", :id, "--name", "wordpress"]
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end

  config.vm.provision "ansible" do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.playbook = "provisioning/playbook.yml"
  end
end
