# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|  
  config.vm.define :controller do |controller|
    controller.vm.box = "wheezy64"
    controller.vm.hostname = "controller"
    controller.vm.network :private_network, ip: "10.0.10.10" # eth1 mgt
    controller.vm.network :private_network, ip: "192.168.10.10" # eth2 tenant api
    controller.vm.provider "virtualbox" do |vbox|
      vbox.customize ["modifyvm", :id, "--memory", "768"]
    end
  end

  config.vm.define :netnode do |netnode|
    netnode.vm.box = "wheezy64"
    netnode.vm.hostname = "netnode"
    netnode.vm.network :private_network, ip: "10.0.10.11" # eth1 mgt
    netnode.vm.network :private_network, ip: "10.0.20.11" # eth2 vm traffic
    netnode.vm.network :private_network, ip: "192.168.101.101", :auto_config => false # eth3 
    netnode.vm.provider "virtualbox" do |vbox|
      vbox.customize ["modifyvm", :id, "--memory", "512"]
      vbox.customize ["modifyvm", :id, "--nicpromisc4", "allow-all"] # eth3
    end
  end

  config.vm.define :compute do |compute|
    compute.vm.box = "wheezy64"
    compute.vm.hostname = "compute"
    compute.vm.network :private_network, ip: "10.0.10.12" # eth1 mgt
    compute.vm.network :private_network, ip: "10.0.20.12" # eth2 vm traffic
    compute.vm.provider "virtualbox" do |vbox|
      vbox.customize ["modifyvm", :id, "--memory", "1024"]
    end
  end

  config.vm.define :storagenode do |storagenode|
    storagenode.vm.box = "wheezy64"
    storagenode.vm.hostname = "storagenode"
    storagenode.vm.network :private_network, ip: "10.0.10.13" # eth1 mgt
    storagenode.vm.network :private_network, ip: "192.168.10.13" # eth2 tenant api
    storagenode.vm.provider "virtualbox" do |vbox|
      vbox.customize ["modifyvm", :id, "--memory", "512"]
      vbox.customize ["createhd",
                      '--filename', "tmp/disk",
                      '--size', "2000" ]
      vbox.customize ['storageattach', :id,
                     '--storagectl', 'SATA Controller',
                     '--port', 1,
                     '--device', 0,
                     '--type', 'hdd',
                     '--medium', "tmp/disk.vdi"]
    end
  end
end
