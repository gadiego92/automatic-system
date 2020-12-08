# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|

  config.vm.box = "bento/centos-8"

  config.ssh.username = "vagrant"

  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    vb.gui = true

    # Customize the amount of memory on the VM:
    vb.memory = "10240"

    # Customize the amount of cpus on the VM:
    vb.cpus = "2"

    vb.customize ["modifyvm", :id, "--vram", "128"]
    vb.customize ["modifyvm", :id, "--accelerate3d", "on"]
    vb.customize ["modifyvm", :id, "--graphicscontroller", "vmsvga"]
    vb.customize ["modifyvm", :id, "--clipboard-mode", "bidirectional"]
    vb.customize ["modifyvm", :id, "--draganddrop", "bidirectional"]
  end

  config.vm.provision :ansible_local do |ansible|
    ansible.playbook_command = "ANSIBLE_CONFIG=/vagrant/ansible.cfg ansible-playbook"
    ansible.provisioning_path = "/vagrant/provision/ansible"
    ansible.playbook = "playbook.yml"
    ansible.verbose = true
  end

end
