# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  ["master", "node"].each { |image|
      config.vm.define image do |node|
        node.vm.box = "ubuntu/xenial64"
        node.vm.network "private_network", :type => 'dhcp', :name => 'vboxnet0', :adapter => 2

        node.vm.synced_folder "data", "/vagrant_data"
        node.vm.provision "shell", path: "config.sh"

        node.vm.provider "virtualbox" do |vb|
          vb.name = image
          vb.memory = 2048
          vb.cpus = 2
        end
    end
  }
end
