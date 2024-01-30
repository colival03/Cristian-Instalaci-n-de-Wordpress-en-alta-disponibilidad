# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "debian/buster64"
  config.vm.synced_folder ".", "/vagrant", disable: true

  config.vm.define "balanceadorwebcristian" do |m1|
        m1.vm.hostname = "cristianbalanceweb"
        m1.vm.network "forwarded_port", guest: 80, host: 8001
        m1.vm.provision "shell", path: "balanceador.sh"
        m1.vm.network "private_network", ip: "192.168.5.2",
                 virtualbox_intet: "lan"
        m1.vm.network "private_network", ip: "192.168.6.2",
                 virtualbox_intet: "inet"
  end

  config.vm.define "serverweb1cristian" do |m2|
        m2.vm.hostname = "cristianserweb1"
        m2.vm.provision "shell", path: "serverweb.sh"
        m2.vm.network "private_network", ip: "193.168.5.3",
                 virtualbox_intnet: "lan"
        m2.vm.network "private_network", ip: "192.168.6.3",
                 virtualbox_intnet: "inet"
  end

  config.vm.define "serverweb2cristian" do |m3|
        m3.vm.hostname = "cristianserweb2"
        m3.vm.provision "shell", path: "serverweb.sh"
        m3.vm.network "private_network", ip: "192.168.5.4",
                 virtualbox_intnet: "lan"
        m3.vm.network "private_network", ip: "192.168.6.4",
                 virtualbox_intnet: "inet"
  end

  config.vm.define "servernfscristian" do |m4|
        m4.vm.hostname = "cristiannfs"
        m4.vm.provision "shell", path: "servernfs.sh"
        m4.vm.network "private_network", ip: "192.168.5.5",
                 virtualbox_intnet: "lan"
        m4.vm.network "private_network", ip: "192.168.7.2",
                 virtualbox_intnet: "datos"
  end

  config.vm.define "balanceadorsqlcristian" do |m5|
        m5.vm.hostname = "cristianbalanceadorsql"
        m5.vm.provision "shell", path: "balanceadorsql.sh"
        m5.vm.network "private_network", ip: "192.168.6.5",
                 virtualbox_intnet: "inet"
        m5.vm.network "private_network", ip: "192.168.7.3",
                 virtualbox_intnet: "datos"
  end

  config.vm.define "serverdatos1cristian" do |m6|
        m6.vm.hostname = "cristiandatos1"
        m6.vm.provision "shell", path: "datos.sh"
        m6.vm.network "private_network", ip: "192.168.7.4",
                 virtualbox_intnet: "datos"
        m6.vm.network "private_network", ip: "192.168.6.6",
                 virtualbox_intnet: "inet"
  end

  config.vm.define "serverdatos1cristian" do |m7|
        m7.vm.hostname = "cristiandatos2"
        m7.vm.provision "shell", path: "datos.sh"
        m7.vm.network "private_network", ip: "192.168.7.5",
                 virtualbox_intnet: "datos"
        m7.vm.network "private_network", ip: "192.168.6.7",
                 virtualbox_intnet: "inet"
  end

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Disable the default share of the current code directory. Doing this
  # provides improved isolation between the vagrant box and your host
  # by making sure your Vagrantfile isn't accessable to the vagrant box.
  # If you use this you may want to enable additional shared subfolders as
  # shown above.
  # config.vm.synced_folder ".", "/vagrant", disabled: true

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
end
