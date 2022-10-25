# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  #boximage
  config.vm.box = "gusztavvargadr/windows-10"

  #network
  config.vm.network "private_network", ip: "192.168.50.3"
  config.vm.network :forwarded_port, host_ip: "127.0.0.1", guest: 5985, host: 5985, id: "winrm", auto_correct: true
  config.vm.network :forwarded_port, host_ip: "127.0.0.1", guest: 3389, host: 3389, id: "rdp", auto_correct: true
  # config.vm.network :forwarded_port, guest: 80, host: 8080, id: "http"
  config.vm.boot_timeout = 600

  #especificar o tipo de SO
  config.vm.guest = :windows
  config.vm.hostname = "win10"
  config.vm.communicator = "winrm"

  #winrm 
  config.winrm.username = "vagrant"     
  config.winrm.password = "vagrant"              
  config.winrm.retry_delay = 10         
  config.winrm.retry_limit = 30 
  config.winrm.guest_port = 5986 
  config.winrm.port = 55986

  #winrm | ssh
  config.ssh.username = "vagrant"
  config.ssh.password = "vagrant"
  config.ssh.insert_key = false

  #provision
  config.vm.provision "shell", path: "scripts/enable-autologon.ps1", privileged: true
  config.vm.provision "reload"
  config.vm.provision "shell", path: "scripts/install-chocolatey.ps1", privileged: false
  config.vm.provision "reload"

  #config virtualbox provider
  config.vm.provider "virtualbox" do |vb|
    vb.name = "win-10"
    vb.gui = true
    vb.memory = "10240"
    vb.cpus = "6"
  end
end