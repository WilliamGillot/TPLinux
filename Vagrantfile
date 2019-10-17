Vagrant.configure("2") do |config|
  config.vm.box = "debian/stretch64"
  config.vm.box_check_update = false

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "384"
  end

  config.vm.provision "init", type: "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get install -qq apache2
    sudo apt-get install -qq libapache2-mod-php
    sudo apt-get install -qq php-mbstring
    sudo apt-get install -qq rsync
    wget  https://download.dokuwiki.org/src/dokuwiki/dokuwiki-stable.tgz
    tar -xvf dokuwiki-stable.tgz
    useradd -m -s /bin/bash -G www-data wiki
    chown -R wiki:www-data dokuwiki-2018-04-22b
    chmod -R g+w /var/www/html/dokuwiki/data
    chmod -R g+w /var/www/html/dokuwiki/conf
    mkdir /home/wiki/.ssh
    cp /vagrant/id_rsa_wiki /home/wiki/.ssh/
    cat /vagrant/id_rsa_wiki.pub >> /home/wiki/.ssh/authorized_keys
    chmod 700 /home/wiki/.ssh
    chmod 600 /home/wiki/.ssh/*
    chown -R wiki:wiki /home/wiki/.ssh
  SHELL

  config.vm.define "wiki" do |wiki|
  	wiki.vm.network "private_network", ip: "192.168.56.11"
    wiki.vm.hostname = "wiki"
  end

  config.vm.define "backup" do |backup|
    backup.vm.network "private_network", ip: "192.168.56.12"
    backup.vm.hostname = "backup"
  end
end