# -*- mode: ruby -*-
# vim: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
  end
  config.vm.define :master do |master_config|
    master_config.vm.box = "debian/jessie64"
    master_config.vm.host_name = 'master.local'
    master_config.vm.network "private_network", ip: "192.168.50.10"
    master_config.vm.synced_folder "states/", "/srv/salt/states/"
    master_config.vm.synced_folder "./", "/srv/salt/pillar/"

    master_config.vm.provision :salt do |salt|
      salt.master_config = "master_config"
#      salt.master_key = "saltstack/keys/master_minion.pem"
#      salt.master_pub = "saltstack/keys/master_minion.pub"
#      salt.minion_key = "saltstack/keys/master_minion.pem"
#      salt.minion_pub = "saltstack/keys/master_minion.pub"
#      salt.seed_master = {
#                          "minion1" => "saltstack/keys/minion1.pub",
#                          "minion2" => "saltstack/keys/minion2.pub"
#                         }

      salt.install_type = "stable"
      salt.install_master = true
      salt.no_minion = true
      salt.verbose = true
      salt.colorize = true
#      salt.bootstrap_options = "-P -c /tmp"
    end
  end

  config.vm.define :minion1 do |minion_config|
    minion_config.vm.box = "debian/jessie64"
    minion_config.vm.host_name = 'minion1.local'
    minion_config.vm.network "private_network", ip: "192.168.50.11"

    minion_config.vm.provision :salt do |salt|
      salt.minion_config = "minion1"
#      salt.minion_key = "saltstack/keys/minion1.pem"
#      salt.minion_pub = "saltstack/keys/minion1.pub"
      salt.install_type = "stable"
      salt.verbose = true
      salt.colorize = true
#      salt.bootstrap_options = "-P -c /tmp"
    end
  end

  config.vm.define :minion2 do |minion_config|
    minion_config.vm.box = "debian/jessie64"
    minion_config.vm.host_name = 'minion2.local'
    minion_config.vm.network "private_network", ip: "192.168.50.12"

    minion_config.vm.provision :salt do |salt|
      salt.minion_config = "minion2"
#      salt.minion_key = "saltstack/keys/minion2.pem"
#      salt.minion_pub = "saltstack/keys/minion2.pub"
      salt.install_type = "stable"
      salt.verbose = true
      salt.colorize = true
#      salt.bootstrap_options = "-P -c /tmp"
    end
  end
end
