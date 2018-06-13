# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"

#  config.vm.network "public_network"
  config.vm.synced_folder "data", "/vagrant_data"

  config.vm.provision "shell", path: "config.sh"

end
