#Vagrant.configure("2") do |config|
#  config.vm.box = "mjacobus/ubuntu-20.04-gui"
#  config.vm.hostname = "ubuntu-test"
#  config.vm.box_check_update = false
#  config.vm.network "private_network", ip: "192.168.56.110"
#  config.vm.synced_folder ".", "/vagrant", disabled: true
#  config.ssh.username = "vagrant"
#  config.ssh.private_key_path=["~/.vagrant.d/insecure_private_key"]
#  config.ssh.insert_key = false
#  config.vm.provider "virtualbox" do |vb|
#    vb.gui = true
#    vb.memory = "2048"
#    vb.cpus = "2"
#    vb.name = "ubuntu-test"
#  end
#    config.vm.provision :shell, inline: "sudo usermod -a -G sudo vagrant"
#end

Vagrant.configure("2") do |config|
  servers=[
      {
        :hostname => "master",
        :box => "mjacobus/ubuntu-20.04-gui",
        :ip => "192.168.56.110",
        :ssh_port => '2200'
      }
#      ,{
#        :hostname => "node1",
#        :box => "ubuntu/bionic64",
#        :ip => "192.168.56.120",
#        :ssh_port => '2201'
#      }
#      ,{
#        :hostname => "node2",
#        :box => "ubuntu/bionic64",
#        :ip => "192.168.56.130",
#        :ssh_port => '2202'
#      }
    ]

  servers.each do |machine|
      config.vm.define machine[:hostname] do |node|
          node.vm.box = machine[:box]
          node.vm.hostname = machine[:hostname]
          node.vm.network :private_network, ip: machine[:ip]
          node.vm.network "forwarded_port", guest: 22, host: machine[:ssh_port], id: "ssh"
          node.vm.provider :virtualbox do |vb|
              vb.customize ["modifyvm", :id, "--memory", 1024]
              vb.customize ["modifyvm", :id, "--cpus", 1]
              vb.name = node.vm.hostname
          end
      end
  end
      config.vm.provision :shell, inline: "sudo usermod -a -G sudo vagrant"
end

