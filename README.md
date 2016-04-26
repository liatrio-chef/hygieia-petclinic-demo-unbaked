hygieia-petclinic-demo-unbaked Cookbook
========================
An unbaked vagrant box / wrapper cookbook that uses hygieia-liatrio to install hygieia with mock data in a local mongodb. 

* This is a wrapper cookbook using hygieia-liatrio primarily to change attributes via json in the Vagrantfile (location of mongodb in this case, mongodata, etc).

Instructions:
* Unbaked https://github.com/liatrio/liatrio-petclinic-demo-unbaked
* Baked https://github.com/liatrio/liatrio-petclinic-demo-baked

Supported Platforms
-------------------

CentOS 7

Requirements
------------
Ensure the ChefDK is installed from https://downloads.chef.io/chef-dk/

Vagrant 1.8.1

Ensure the vagrant-berkshelf plugin is installed: `vagrant plugin install vagrant-berkshelf`

Usage
-----
`vagrant up` will install mongodb with mock data, build hygieia, and start on boot. You may need to ssh to the VM and `cd ~/Hygieia; mvn clean install` multiple times due to network issues pulling down artifacts followed by logging out of ssh and running a `vagrant provision` to ensure the chef run completes.

If working on hygieia development you can easily restart the api, ui, and all collectors via `cd /etc/systemd/system; sudo systemctl restart hygieia-*`.

* Browse to http://localhost:13000/
* Login with admin / password

License and Authors
-------------------
Authors: Drew Holt <drew@liatrio.com>
