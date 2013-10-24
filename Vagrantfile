# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|  
  config.vm.define :controller do |controller|
    controller.vm.box = "wheezy64"
    controller.vm.hostname = "controller"
    controller.vm.network :private_network, ip: "192.168.222.101" # eth1 internal
    controller.vm.network :private_network, ip: "192.168.221.101" # eth2 external
    controller.vm.provider "virtualbox" do |vbox|
      vbox.customize ["modifyvm", :id, "--memory", "768"]
      vbox.customize ["modifyvm", :id, "--nicpromisc3", "allow-all"] # eth2
    end
  end

  config.vm.define :compute do |compute|
    compute.vm.box = "wheezy64"
    compute.vm.hostname = "compute"
    compute.vm.network :private_network, ip: "192.168.222.121" # eth1 internal
#    compute.vm.network :private_network, ip: "192.168.122.121" # eth2 external
    compute.vm.provider "virtualbox" do |vbox|
      vbox.customize ["modifyvm", :id, "--memory", "1024"]
    end
  end

  config.vm.define :storagenode do |storagenode|
    storagenode.vm.box = "wheezy64"
    storagenode.vm.hostname = "storagenode"
    storagenode.vm.network :private_network, ip: "192.168.222.111" # eth1 internal
#    storagenode.vm.network :private_network, ip: "192.168.122.111" # eth2 external
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
