# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  #config.ssh.insert_key = false
  #config.ssh.password = "ubuntu"
  #config.ssh.username = "ubuntu"  
  #config.ssh.private_key_path = "id_rsa"
# The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.define "manager_box" do |master|
    master.vm.box = "ubuntu/xenial64"
    master.vm.hostname = "manager"
    master.vm.network :forwarded_port, guest:8080, host:8080
    master.vm.network :private_network, ip: "192.168.1.10"
    master.vm.provider "virtualbox" do |vb|
    
     # Display the VirtualBox GUI when booting the machine
     #vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
     vb.memory = "2048"
     vb.name = "mysql_server_manager"
    end
  end
##########################################3
  config.vm.define "mysql_datanode1" do |slave|
    slave.vm.provider "virtualbox" do |vb|
     vb.memory = "2048"
     vb.name = "mysql_node1"
    end
    slave.vm.network :private_network, ip: "192.168.1.11"
    slave.vm.hostname = "node1"
    slave.vm.box = "ubuntu/xenial64"
    slave.vm.network :forwarded_port, guest:8081, host:8081
  end
  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

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

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
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
  # config.vm.provision "shell", inline: <<-SHELL
  #   sudo apt-get update
  #   sudo apt-get install -y openjdk-8-jdk  && sed -i  '1iJAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd6' /vagrant/hadoop-2.7.3/etc/hadoop/hadoop-env.sh
  # SHELL
  # config.vm.provision "shell", path:  "init.sh" 
  # config.vm.provision "puppet" do |puppet|
  #  puppet.manifests_path = "manifests"
  #  puppet.module_path = "modules"
  #  puppet.manifest_file = "site.pp"
  # end
  config.vm.provision "ansible" do |ansible|
#    ansible.extra_vars = { ansible_ssh_user: 'ubuntu' }
    ansible.verbose = "v"
    ansible.playbook = "site.yml"
    ansible.inventory_path = "./staging"
  #  ansible.limit = "all"  ### <<-- adding this line

  end
end
