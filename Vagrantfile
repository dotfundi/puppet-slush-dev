# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  
  config.vm.box = "ubuntu/trusty32"

  config.vm.define "slushdev" do | slushdev |
    slushdev.vm.hostname = "slush-dev" 
    #sync folders
    slushdev.vm.synced_folder "./www", "/home/vagrant/www", create: true

    #port forward
    slushdev.vm.network  :forwarded_port, host: 9000,  guest: 9000    # Express
    slushdev.vm.network  :forwarded_port, host: 35729, guest: 35729   # LiveReload
    slushdev.vm.network  :forwarded_port, host: 27017, guest: 27017   # MongoDB

    config.vm.provision :shell do |shell|
      shell.inline = "mkdir -p /etc/puppet/modules;
                  puppet module install willdurand-nodejs;
                  puppet module install puppetlabs-mongodb;
                  puppet module install puppetlabs-git"
    end

    slushdev.vm.provision :puppet do | puppet |
     #puppet.module_path = "puppet/modules"
     puppet.manifests_path = "puppet/manifests"
     puppet.manifest_file = "slushdev.pp"
    end
  end

  
end
