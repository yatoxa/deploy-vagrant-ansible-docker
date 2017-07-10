# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.define "ci_33100" do |ci33100|
    ci33100.vm.box = "ubuntu/xenial64"
    ci33100.vm.box_check_update = false
    ci33100.vm.network "private_network", ip: "192.168.33.100"
    ci33100.vm.provider "virtualbox" do |vb|
      vb.cpus = 2
      vb.memory = "1024"
      vb.customize ["modifyvm", :id, "--cpuexecutioncap", "90"]
    end
  end

  config.vm.define "dev_trm_33101" do |dtrm33101|
    dtrm33101.vm.box = "ubuntu/xenial64"
    dtrm33101.vm.box_check_update = false
    dtrm33101.vm.network "private_network", ip: "192.168.33.101"
    dtrm33101.vm.provider "virtualbox" do |vb|
      vb.cpus = 2
      vb.memory = "1024"
      vb.customize ["modifyvm", :id, "--cpuexecutioncap", "90"]
    end
  end

  config.vm.provision "shell" do |s|
    ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
    s.inline = <<-SHELL
      if [ ! -f ~/runonce ]
        then
          echo #{ssh_pub_key} >> /home/ubuntu/.ssh/authorized_keys
          touch ~/runonce
      fi
      ln -f -s /usr/bin/python3 /usr/bin/python
      apt-get update
      apt-get -y install htop vim
    SHELL
  end

end
