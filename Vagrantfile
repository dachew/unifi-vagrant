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
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "ubuntu/xenial64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  #
  # Controller interface
  config.vm.network "forwarded_port", guest: 8443, host: 8443, protocol: "tcp"
  # TCP port for UAP to inform controller
  config.vm.network "forwarded_port", guest: 8080, host: 8080, protocol: "tcp"
  # throughput measurement
  config.vm.network "forwarded_port", guest: 6789, host: 6789, protocol: "tcp"
  # local-bound TCP port for DB server
  config.vm.network "forwarded_port", guest: 27117, host: 27117, protocol: "tcp"
  # UDP port used for STUN v4.5.2+
  config.vm.network "forwarded_port", guest: 3478, host: 3478, protocol: "udp"
  # UDP AP-EDU broadcasts
  for i in 5656..5699
  	config.vm.network "forwarded_port", guest: i, host: i, protocol: "udp"
  end
  # redirectors for wireless & wired clients
  config.vm.network "forwarded_port", guest: 8881, host: 8881, protocol: "tcp"
  config.vm.network "forwarded_port", guest: 8882, host: 8882, protocol: "tcp"
  # AP Discovery
  config.vm.network "forwarded_port", guest: 10001, host: 10001, protocol: "udp"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.1.36"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  #config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  config.vm.synced_folder "./data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  #config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  #end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    set -e

    # From https://help.ubnt.com/hc/en-us/articles/220066768-UniFi-How-to-Install-Update-via-APT-on-Debian-or-Ubuntu
    echo "deb http://www.ubnt.com/downloads/unifi/debian stable ubiquiti" > /etc/apt/sources.list.d/ubiquiti.list
    apt-key adv --keyserver keyserver.ubuntu.com --recv 06E85760C0A52C50
    apt update
	apt install -y unifi
   SHELL
end
