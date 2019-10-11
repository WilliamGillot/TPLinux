Vagrant.configure(2) do |config|
  config.vm.define "wiki" do |wiki|
    config.vm.box = "debian/jessie64"
    config.vm.network "private_network", ip: "192.168.56.10"
    config.vm.hostname = "wiki"
  end

  config.vm.define "backup" do |backup|
    config.vm.box = "debian/jessie64"
    config.vm.network "private_network", ip: "192.168.56.20"
    config.vm.hostname = "backup"
  end

  config.vm.provision "shell", inline: <<-SHELL
    export DEBIAN_FRONTEND=noninteractive
    sudo apt-get update
    sudo apt-get install -y php-geshi
    cd /tmp
    wget https://download.dokuwiki.org/src/dokuwiki/dokuwiki-stable.tgz
    tar -xvf dokuwiki-stable.tgz
  SHELL
end
