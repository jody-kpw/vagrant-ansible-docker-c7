# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"

  config.vm.define "control" do |control|
    control.vm.hostname = "control"
    control.vm.network "private_network", ip: "192.168.50.10"
    control.vm.provision :shell, :path => "provision/control/provision-control.sh"

    # Disable default /vagrant synced folder
    control.vm.synced_folder ".", "/vagrant", disabled: true

    # custom synced folder and set permissions
    control.vm.synced_folder "~/Projects/vagrant-ansible-docker-c7/provision", "/provision",
        owner: "vagrant",
        group: "vagrant",
        mount_options: ["dmode=755,fmode=644"]

    control.vm.synced_folder "~/Projects/vagrant-ansible-docker-c7/ansible", "/home/vagrant/ansible",
        owner: "vagrant",
        group: "vagrant",
        mount_options: ["dmode=755,fmode=644"]
  end


  config.vm.define "dockermaster" do |dockermaster|
    dockermaster.vm.hostname = "dockermaster"
    dockermaster.vm.network "private_network", ip: "192.168.50.20"

    # Disable default /vagrant synced folder
    dockermaster.vm.synced_folder ".", "/vagrant", disabled: true

    # custom synced folder and set permissions
    dockermaster.vm.synced_folder "~/Projects/vagrant-ansible-docker-c7/provision", "/provision",
        owner: "vagrant",
        group: "vagrant",
        mount_options: ["dmode=755,fmode=644"]

    dockermaster.vm.provision "shell",
        ##inline: "cat /provision/control/ssh/id_rsa.pub >> ~/.ssh/authorized_keys"
        inline: "cat /provision/control/ssh/id_rsa.pub >> /home/vagrant/.ssh/authorized_keys"
  end

end
