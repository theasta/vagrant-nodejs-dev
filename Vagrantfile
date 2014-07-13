# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box     = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  config.vm.network :private_network, ip: "192.168.50.3"

  # config.vm.synced_folder "/local/path/to/myapp", "/srv/myapp"
  # config.vm.synced_folder "/local/path/to/anotherapp", "/srv/anotherapp"

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", 512]
    vb.customize ["modifyvm", :id, "--vtxvpid", "off"]
    vb.customize ["modifyvm", :id, "--cpus", "1"]
  end

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "ansible-playbooks/main.yml"
    # ansible.verbose = 'vvvv'
  end
end
