# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'yaml'
options = YAML.load_file File.join(File.dirname(__FILE__), 'vagrant.yaml')
domains = [
    "app.dev",
    "backend.app.dev",
    "storage.app.dev"
]

Vagrant.configure(2) do |config|
  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = options['vm']['memory']
    vb.cpus = options['vm']['cpus']
  end

  # based on ubuntu/trusty64 (virtualbox, 14.04)
  config.vm.box = "base"
  config.vm.hostname = domains[0]
  config.vm.network "private_network", ip: options['network']['ip']
  config.vm.synced_folder "./", "/var/www", id: "vagrant-root", :nfs => false, owner: "www-data", group: "www-data"

  config.vm.provision :hostmanager
  config.hostmanager.enabled            = true
  config.hostmanager.manage_host        = true
  config.hostmanager.ignore_private_ip  = false
  config.hostmanager.include_offline    = true
  config.hostmanager.aliases            = domains

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

end
