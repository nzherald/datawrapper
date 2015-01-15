# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = '2'

$provisioning_script = <<SCRIPT
echo 'Provisioning...'
export DEBIAN_FRONTEND=noninteractive
apt-get update
apt-get install apache2 php5 php5-mysql mysql-server nodejs npm git -y -q
# git is required due to https://github.com/datawrapper/datawrapper/blob/master/lib/utils/add_header_vars.php#L213
a2enmod rewrite
service apache2 restart
cd /vagrant
curl -sS https://getcomposer.org/installer | php
php composer.phar install
mysql -u root -e 'create database datawrapper;'
cp lib/core/build/conf/datawrapper-conf.php.master lib/core/build/conf/datawrapper-conf.php
mysql -u root datawrapper < lib/core/build/sql/schema.sql
cp config.template.yaml config.yaml
npm install
ln -s /usr/bin/nodejs /usr/bin/node # https://github.com/joyent/node/issues/3911
make clean
make
php scripts/plugin.php install "*"
cp bootstrap/datawrapper.conf /etc/apache2/sites-available/datawrapper.conf
ln -s /etc/apache2/sites-available/datawrapper.conf /etc/apache2/sites-enabled/datawrapper.conf
cp -R /vagrant /var/www/datawrapper
chown -R www-data:www-data /var/www/datawrapper
service apache2 restart
date > /etc/vagrant_provisioned_at
SCRIPT


Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.provider :virtualbox do |vb|
      vb.customize ['modifyvm', :id, '--natdnshostresolver1', 'on']
  end
  config.vm.box = 'ubuntu/trusty64'
  config.vm.network 'forwarded_port', guest: 80, host: 8080
  config.ssh.forward_agent = true
  config.vm.provision 'shell', inline: $provisioning_script
  config.dns.tld = 'local'
  config.dns.patterns = [/^.*datawrapper.local$/]
  config.vm.hostname = 'datawrapper'
  config.vm.network :private_network, ip: '33.33.33.60'
end
