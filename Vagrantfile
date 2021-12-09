# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "debian/buster64"
  config.vm.hostname = "pihole"
  config.vm.network "public_network", bridge: "eno1.201", auto_config: false
  config.vm.synced_folder ".", "/vagrant", type: "virtualbox"
  config.timezone.value = "Europe/Copenhagen"
  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = "768"
    vb.customize ["guestproperty", "set", :id, "/VirtualBox/GuestAdd/VBoxService/--timesync-set-threshold", 10000]
  end

  config.vm.provision "initnet", type: "ansible", run: "once" do |ansible|
    ansible.playbook = "setnetwork.yml"
  end

  config.vm.provision "pihole", type: "ansible", run: "never" do |ansible|
    ansible.playbook = "pihole-provision.yml"
  end

end
