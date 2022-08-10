# -*- mode: ruby -*-
# vi: set ft=ruby :
VAGRANTFILE_API_VERSION = "2"
cluster = {
  "master" => { :ip => "192.168.56.200", :cpus => 2, :mem => 2048 },
  "slave" => { :ip => "192.168.56.210", :cpus => 2, :mem => 2048 }
}
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  cluster.each_with_index do |(hostname, info), index|
    config.vm.define hostname do |cfg|
      cfg.vm.provider :virtualbox do |vb, override|
        config.vm.box = "ubuntu/bionic64"
        override.vm.network :private_network, ip: "#{info[:ip]}"
        override.vm.hostname = hostname
        vb.name = hostname
        vb.customize ["modifyvm", :id, "--memory", info[:mem], "--cpus", info[:cpus], "--hwvirtex", "on"]
      end # end provider
    end # end config
  end # end cluster
  # Update repositories
  config.vm.provision :shell, inline: "sudo apt update -y"
  # Upgrade installed packages
  config.vm.provision :shell, inline: "sudo apt upgrade -y"
end
