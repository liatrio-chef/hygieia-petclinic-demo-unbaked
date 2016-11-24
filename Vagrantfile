# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = 'bento/centos-7.2'

  config.vm.network :private_network, ip: '192.168.100.120'
  config.vm.network 'forwarded_port', guest: 80, host: 1080
  config.vm.network 'forwarded_port', guest: 3000, host: 13000
  config.vm.network 'forwarded_port', guest: 8080, host: 18080
  config.vm.network 'forwarded_port', guest: 27017, host: 37017

  config.vm.provider 'virtualbox' do |v|
    v.customize ['modifyvm', :id, '--natdnshostresolver1', 'on']
    v.customize ['modifyvm', :id, '--cpus', 2]
    v.customize ['modifyvm', :id, '--memory', '1576']
    # v.customize ["modifyvm", :id, "--name", "hygieia"]
  end

  config.berkshelf.enabled = true

  config.vm.provision 'chef_solo' do |chef|
    chef.add_recipe 'hygieia-petclinic-demo-unbaked'
    chef.add_recipe 'hygieia-liatrio::mongodb'
    chef.add_recipe 'hygieia-liatrio::node'
    chef.add_recipe 'hygieia-liatrio'
    chef.add_recipe 'hygieia-liatrio::mongodb_sample_data'
    chef.add_recipe 'hygieia-liatrio::apache2'
    chef.json = {
      'java' => {
        'jdk_version' => '8'
      },
      'hygieia_liatrio' => {
        'parent_cookbook' => 'hygieia-petclinic-demo-unbaked',
        'dbname' => 'dashboard',
        'dbhost' => 'localhost',
        'dbport' => 27017,
        'dbusername' => 'db',
        'dbpassword' => 'dbpass'
      }
    }
  end
end
