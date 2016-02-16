# -*- mode: ruby -*-
# vi: set ft=ruby : 

VAGRANTFILE_API_VERSION = "2" 

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  config.hostmanager.ignore_private_ip = false
  config.hostmanager.include_offline = true
  config.ssh.insert_key = false
  config.ssh.pty = true

  config.vm.define "lb" do |machine|
    machine.vm.box = "centos7"
    machine.vm.synced_folder '.', '/vagrant'
    machine.vm.box_url = "https://f0fff3908f081cb6461b407be80daf97f07ac418.googledrive.com/host/0BwtuV7VyVTSkUG1PM3pCeDJ4dVE/centos7.box"
    machine.vm.network :private_network, ip: "10.0.0.20",
                       :netmask => "255.255.0.0"

    machine.vm.hostname = "lb"
    machine.vm.provider :virtualbox do |v|
      v.memory = 512
      v.cpus = 2
    end
  end
  
  (1..3).each do |i|
    config.vm.define "r#{i}" do |node|
    node.vm.box = "centos7"
    node.vm.box_url = "https://f0fff3908f081cb6461b407be80daf97f07ac418.googledrive.com/host/0BwtuV7VyVTSkUG1PM3pCeDJ4dVE/centos7.box"
    node.vm.network :private_network, ip: "10.0.0.3#{i}", :netmask => "255.255.0.0"
    node.vm.hostname = "r#{i}.tst"
    node.hostmanager.alias = %w(r#{i})
      node.vm.provider :virtualbox do |v|
	v.memory = 512
      end      
    end
  end
end