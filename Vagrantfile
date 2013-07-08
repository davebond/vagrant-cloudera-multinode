# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  # Node settings
  node_count = 2
  node_ram = 2048

  # Create hosts data
  hosts = "192.168.50.2 hadoop-manager\n"
  node_count.times do |i|
    id = i+1
    hosts << "192.168.50.#{id+2} hadoop-node#{id}\n"
  end

  # Use ubuntu precise
  config.vm.box = "precise64"

  # Write hosts file
  config.vm.provision :shell, :inline => "echo \"#{hosts}\" | sudo tee -a /etc/hosts"

  # Manager
  config.vm.define :manager do |manager_config|
    manager_config.vm.hostname = "hadoop-manager"
    manager_config.vm.network :forwarded_port, guest: 7180, host: 7180
    manager_config.vm.network :private_network, ip: "192.168.50.2"
    manager_config.vm.synced_folder "files/", "/home/vagrant/files"
    manager_config.vm.provider :virtualbox do |vb|
      # Boot with headless mode
      vb.gui = false
      # Use VBoxManage to customize the VM. For example to change memory:
      vb.customize ["modifyvm", :id, "--memory", "512"]
    end
  end

  # Create nodes
  node_count.times do |i|
    id = i+1
    config.vm.define "node#{id}" do |node_config|
      node_config.vm.hostname = "hadoop-node#{id}"
      node_config.vm.network :private_network, ip: "192.168.50.#{id+2}"
      node_config.vm.provider :virtualbox do |vb|
        # Use VBoxManage to customize the VM. For example to change memory:
        vb.customize ["modifyvm", :id, "--memory", "#{node_ram}"]
      end
    end
  end

end
