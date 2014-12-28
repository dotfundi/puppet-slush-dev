# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  
  config.vm.box = "ubuntu/trusty32"

  config.vm.define "nodedev" do | nodedev |
    nodedev.vm.hostname = "node-dev" 
    #sync folders
    nodedev.vm.synced_folder "./www", "/home/vagrant", create: true

    #port forward
    nodedev.vm.network  :forwarded_port, host: 9000,  guest: 9000    # Express
    nodedev.vm.network  :forwarded_port, host: 35729, guest: 35729   # LiveReload
    nodedev.vm.network  :forwarded_port, host: 27017, guest: 27017   # MongoDB

    nodedev.vm.provision :puppet do | puppet |
     puppet.module_path = "puppet/modules"
     puppet.manifests_path = "puppet/manifests"
     puppet.manifest_file = "nodedev.pp"
    end
  end

  
end
