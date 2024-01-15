# -*- mode: ruby -*-
# vi: set ft=ruby :

def configure_vm(config, name, box, addr)
  config.vm.define name do |name|
    name.vm.box = box
    name.vm.network "private_network", ip: addr

    config.vm.provider "virtualbox" do |v|
      v.memory = 512
      v.cpus = 1
    end
  end
end

$prov = <<-SCRIPT
  apt-get update ; apt-get install ansible -y
  sudo su - ; echo "ansible" > /etc/hostname
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.define "ansible" do |ansible|
    ansible.vm.box = "ubuntu/focal64"
    ansible.vm.network "private_network", ip: "10.10.10.10"
    ansible.vm.provision "shell", inline: $prov
  end

  configure_vm(config, "ubuntu", "ubuntu/bionic64", "10.10.10.11")
  configure_vm(config, "debian", "generic/debian9", "10.10.10.12")
  configure_vm(config, "centos", "centos/7", "10.10.10.13")
end
