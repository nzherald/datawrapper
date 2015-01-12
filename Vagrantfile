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
rm /var/www/html/index.html
date > /etc/vagrant_provisioned_at
SCRIPT


Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = 'ubuntu/trusty64'
  config.vm.network 'forwarded_port', guest: 80, host: 8080
  config.ssh.forward_agent = true
  config.vm.provision 'shell', inline: $provisioning_script
  config.dns.tld = 'local'
  config.dns.patterns = [/^.*datawrapper.local$/]
  config.vm.hostname = 'datawrapper'
  config.vm.network :private_network, ip: '33.33.33.60'
end
