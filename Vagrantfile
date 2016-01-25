# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  config.vm.box = "hashicorp/precise32"
  config.vm.provider "virtualbox" do |vb|
     vb.memory = "512"
  end
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get -y install php5-dev
    sudo apt-get -y install make
    sudo apt-get -y install libxml2-dev
    sudo apt-get -y install firebird2.5-dev

    sudo mkdir /src
    sudo wget --quiet -O /src/php-5.5.29.tar.gz  http://de1.php.net/get/php-5.5.29.tar.gz/from/this/mirror
    sudo tar zxvf /src/php-5.5.29.tar.gz -C /src/
    cd /src/php-5.5.29/

    sudo './configure' '--with-pdo-firebird=shared'
    sudo make
    sudo cp /src/php-5.5.29/modules/pdo_firebird.so /vagrant/
    sudo cp /usr/lib/i386-linux-gnu/libfbclient.so.2 /vagrant/

    # Copy 'pdo_firebird.so' to '/usr/local/apache/modules/'
    # Copy 'libfbclient.so.2' to '/usr/local/lib/' on the Qnap
    # Run 'ldconfig' once to include the shared library
    # Run 'ldd /usr/local/apache/modules/pdo_firebird.so' to verify that all libraries found and can be loaded

  SHELL
end
