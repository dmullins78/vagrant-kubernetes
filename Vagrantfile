# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  ["kubmaster", "kubslave"].each { |image|
      config.vm.define image do |node|
        node.vm.hostname = image
        node.vm.box = "ubuntu/xenial64"
        node.vm.network "public_network", bridge: "en1: Wi-Fi (AirPort)"
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

