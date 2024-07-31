
Vagrant.configure("2") do |config|
config.vm.box = "alse-vanilla-gui-base/1.7.4"
config.vm.define "ipa_master" do |dc01|
  dc01.vm.network "private_network", 
    :ip => "192.168.56.3",
    :virtualbox__dhcp_enabled => false,
    :virtualbox__forward_mode => "nat",
    :virtualbox__netmask => "255.255.255.0",
    :virtualbox__network_name => "net"
  dc01.vm.network "forwarded_port", guest: 443, host: 8080
  dc01.vm.hostname = "dc01.test.local"
  dc01.vm.provision "ansible" do |ansible|
    ansible.playbook = "ipa.yml"
    ansible.limit = "all"
    ansible.verbose = "vvv"
  dc01.vm.provider "virtualbox" do |vb|
    vb.memory = "4098"
    vb.cpus = "2"
    vb.name = "dc01"
  end
end
end
config.vm.define "client" do |cli|
  cli.vm.network "private_network",
    :ip => "192.168.56.20",
    :virtualbox__dhcp_enabled => false,
    :virtualbox__forward_mode => "nat",
    :virtualbox__netmask => "255.255.255.0",
    :virtualbox__network_name => "net"
  cli.vm.hostname = "client1.test.local"
  cli.vm.provision "ansible" do |ansible|
    ansible.playbook = "cli.yml"
    ansible.limit = "all"
    ansible.verbose = "vvv"
  cli.vm.provider "virtualbox" do |vb|
    vb.memory = "2096"
    vb.cpus = "2"
    vb.name = "client1"
  end
end
end
  config.vm.define "monitor" do |mon|
    mon.vm.box = "alse-vanilla-base/1.7.4"
    mon.vm.network "private_network", 
      :ip => "192.168.56.10",
      :virtualbox__dhcp_enabled => false,
      :virtualbox__forward_mode => "nat",
      :virtualbox__netmask => "255.255.255.0",
      :virtualbox__network_name => "net"
    mon.vm.hostname = "monitor.test.local"
    mon.vm.provision "ansible" do |ansible|
      ansible.playbook = "monitor.yml"
      ansible.limit = "all"
      ansible.verbose = "vvv"
    mon.vm.provider "virtualbox" do |vb|
      vb.memory = "2096"
      vb.cpus = "1"
      vb.name = "monitor"
    end
  end
end
end