# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/zesty64"

  config.vm.provider "virtualbox" do |vb|
    # Customize the amount of memory on the VM
    vb.memory = "2048"
  end

  #Share the root of the repo
  config.vm.synced_folder "../", "/termux-packages"
  #Disable the default /vagrant share directory, as it shares the directory with the Vagrantfile in it, not the repo root
  config.vm.synced_folder ".", "/vagrant", disabled: true


  #Run provisioning scripts
  config.vm.provision "shell", path: "./setup-ubuntu.sh", privileged: false
  config.vm.provision "shell", path: "./setup-android-sdk.sh", privileged: false

  #Fix permissions on the /data directory in order to allow the "ubuntu" user to write to it
  config.vm.provision "shell",
    inline: "sudo chown -R ubuntu /data"

  #Tell the user how to use the VM
  config.vm.post_up_message = "Box has been provisioned! Use 'vagrant ssh' to enter the box. The repository root is available under '/termux-packages'."
end
