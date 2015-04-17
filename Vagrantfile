# -*- mode: ruby -*-

intnetname="dev"
intdomain="tanabata.dev"
vbnet="192.168.33"

VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.define :ryoko do |ryoko|
    ryoko.vm.box = "debian-7.8.0-amd64"
    ryoko.vm.box_url = "https://realloc.spb.ru/boxes/debian-7.8.0-amd64.box"
    ryoko.vm.hostname = "ryoko.#{intdomain}"
    ryoko.vm.provider :virtualbox do |vb|
      vb.name = "ryoko"
      vb.gui = false
      vb.memory = 512
      vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    end
    # Adapter 1 is default nat
    ryoko.vm.network "private_network", auto_config: true, ip:"#{vbnet}.12", :adapter => 2
    ryoko.vm.provision :chef_zero do |chef|
      chef.data_bags_path = "data_bags"
      chef.cookbooks_path = "cookbooks"
      chef.roles_path = "roles"
      chef.nodes_path = "nodes"
      chef.add_role "zero-vmbase"
    end
  end

end
