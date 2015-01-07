# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = '2'

$provisioning_script = <<SCRIPT
echo 'Provisioning...'
export DEBIAN_FRONTEND=noninteractive
apt-get install apache2 php5 php5-mysql mysql-server nodejs npm -y -q
cd /vagrant
curl -sS https://getcomposer.org/installer | php
php composer.phar install
mysql -u root -e 'create database datawrapper;'
cp lib/core/build/conf/datawrapper-conf.php.master lib/core/build/conf/datawrapper-conf.php
cp config.template.yaml config.yaml
npm install
ln -s /usr/bin/nodejs /usr/bin/node # https://github.com/joyent/node/issues/3911
make clean
make
date > /etc/vagrant_provisioned_at
SCRIPT


Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = 'ubuntu/trusty64'

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  config.vm.network 'forwarded_port', guest: 80, host: 8080

  config.ssh.forward_agent = true

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  config.vm.provision 'shell', inline: $provisioning_script

  # Enable provisioning with chef solo, specifying a cookbooks path, roles
  # path, and data_bags path (all relative to this Vagrantfile), and adding
  # some recipes and/or roles.
  #
  # config.vm.provision "chef_solo" do |chef|
  #   chef.cookbooks_path = "../my-recipes/cookbooks"
  #   chef.roles_path = "../my-recipes/roles"
  #   chef.data_bags_path = "../my-recipes/data_bags"
  #   chef.add_recipe "mysql"
  #   chef.add_role "web"
  #
  #   # You may also specify custom JSON attributes:
  #   chef.json = { mysql_password: "foo" }
  # end
end
