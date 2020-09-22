# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    config.vm.box = "bento/centos-6.7"
  # config.vm.box_check_update = false
  # config.vm.network "forwarded_port", guest: 80, host: 8080
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
    config.vm.network :forwarded_port, guest: 22, host: 2222, id: 'ssh', auto_correct: true
  # config.vm.network "private_network", ip: "192.168.33.10"
  # config.vm.network "public_network"
    config.vm.synced_folder "./", "/vagrant", :mount_options => ["dmode=777", "fmode=777"]

  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end

    config.vm.provision "shell", inline: <<-SHELL
      sudo yum update
      sudo rm -rf /var/www/html
      sudo ln -fs vagrant/ /var/www/html
    SHELL

  # vagrant up時にplaybookを実行するように追加。
    config.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "test.yml"
    end

end