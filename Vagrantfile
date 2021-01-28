# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV['VAGRANT_NO_PARALLEL'] = 'yes'

Vagrant.configure(2) do |config|

  config.vm.provision "shell", path: "bootstrap.sh"

  # Docker Host
  config.vm.define "docker" do |docker|
    docker.vm.box = "bento/ubuntu-18.04"
    docker.vm.hostname = "docker.example.com"
    docker.vm.network "private_network", ip: "192.168.65.211"
    docker.vm.provider "virtualbox" do |v|
      v.name = File.basename(File.dirname(__FILE__)) + "_" + Time.now.to_i.to_s
      v.memory = 4096
      v.cpus = 2
    end
  end

end
