# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  if (/cygwin|mswin|mingw|bccwin|wince|emx/ =~ RUBY_PLATFORM) != nil
    config.vm.synced_folder ".", "/vagrant", mount_options: ["dmode=700,fmode=600"]
  else
    config.vm.synced_folder ".", "/vagrant"
  end 
  config.vm.box = "ubuntu/trusty64"

  config.vm.define :node1 do |node1_config|
      node1_config.vm.host_name = "node1"
#      node1_config.vm.network "private_network", ip:"172.17.8.104"
      node1_config.vm.network "public_network", bridge: "eno4", ip: "192.168.57.56", auto_config: "false", netmask: "255.255.255.0" , gateway: "192.168.57.1"
      default_router = "192.168.57.1"
      node1_config.vm.provision :shell, inline: "ip route delete default 2>&1 >/dev/null || true; ip route add default via #{default_router}"
      node1_config.vm.provision :shell, path: "scripts/bootstrap4Ubuntu_ansible.sh"
      node1_config.vm.provider :virtualbox do |vb|
          vb.customize ["modifyvm", :id, "--memory", "1024"]
          vb.customize ["modifyvm", :id, "--cpus", "1"]
      end
  end

  config.vm.define :node2 do |node2_config|
      node2_config.vm.host_name = "node2"
#      node2_config.vm.network "private_network", ip:"172.17.8.105"
      node2_config.vm.network "public_network", bridge: "eno4", ip: "192.168.57.57", auto_config: "false", netmask: "255.255.255.0" , gateway: "192.168.57.1"
      default_router = "192.168.57.1"
      node2_config.vm.provision :shell, inline: "ip route delete default 2>&1 >/dev/null || true; ip route add default via #{default_router}"
      node2_config.vm.provision :shell, path: "scripts/bootstrap4Ubuntu_ansible.sh"
      node2_config.vm.provider :virtualbox do |vb|
          vb.customize ["modifyvm", :id, "--memory", "1024"]
          vb.customize ["modifyvm", :id, "--cpus", "1"]
      end
  end
  
  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box
  end
end