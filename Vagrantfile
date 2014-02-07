# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.hostname = "chefbox"
  config.vm.box = "opscode-ubuntu-12.04"
  config.vm.box_url = "https://opscode-vm.s3.amazonaws.com/vagrant/opscode_ubuntu-12.04_provisionerless.box"

  config.vm.network :private_network, ip: "33.33.33.10"

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024"]
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end

  config.berkshelf.enabled = true
  config.omnibus.chef_version = :latest

  # config.vm.provision :chef_solo do |chef|
  #   chef.run_list = [
  #       "recipe[vps]"
  #   ]
  # end

  config.vm.provision :chef_client do |chef|
    chef.chef_server_url = "https://api.opscode.com/organizations/chance"
    chef.validation_client_name = "chance-validator"
    chef.validation_key_path = "#{ENV['HOME']}/.chef/chance-validator.pem"
    chef.client_key_path = "#{ENV['HOME']}/.chef/ecnahc515.pem"
    chef.node_name = "vagrant-chef"

    # chef.delete_node = true
    # chef.delete_client = true

    chef.run_list = [
        "recipe[base]"
    ]
  end
end
