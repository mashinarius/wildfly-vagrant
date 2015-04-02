# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure(2) do |config|

	boxes = {
		"gps-vader" => "005056b05074",
		"gps-chewey" => "005056b0a74b",
		"gps-jabba-hutt" => "000c29a0fa8b",
	}

	config.vm.box = "ubuntu64vagrant"
#	config.vm.box_url = "http://is-rational.iba/boxes/trusty-server-cloudimg-amd64-vagrant-disk1.box"

	boxes.each do |box_name, box_mac|
		config.vm.define box_name do |config|
			config.vm.network :public_network, :bridge => 'eth0', :mac=>box_mac
			config.vm.provision :ansible do |ansible| 
				ansible.playbook = "all.yml"
#				ansible.inventory_path = "vagrant_ansible_inventory"
				ansible.groups = {
					"wildflygroup" => ["gps-vader", "gps-chewey"],
					"httpgroup" => ["gps-jabba-hutt"],
					"all_groups:children" => ["wildflygroup", "httpgroup"]
				}
			end
		end

	end
end
