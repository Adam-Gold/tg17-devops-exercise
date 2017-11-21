# -*- mode: ruby -*-
# vi: set ft=ruby :
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "ubuntu/xenial64"
  config.vm.network :private_network, ip: '192.168.50.200'

  config.vm.provider :virtualbox do |vbox|
    vbox.memory = 1024
    vbox.cpus = 2
  end

  config.vm.provision 'shell',
    inline: "sudo bash -c \"test -e /usr/bin/python || (apt-get -qqy update && apt-get install -qqy python-minimal)\""

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "base.yml"
    ansible.inventory_path = "dev"
    ansible.host_key_checking = false
  end

  config.ssh.forward_agent = true

  # Create a base machine 
  config.vm.define "base" do |base|
      base.vm.network :forwarded_port, host: 8080, guest: 8080
  end
end
