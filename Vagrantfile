# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
require "yaml"

Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-22.04"
  config.vm.usable_port_range = 2400..2499

  machines = YAML.safe_load(
  File.read(File.join(__dir__, "machines.yml"))
)
config.hostmanager.enabled = true
config.hostmanager.manage_guest = true
config.hostmanager.manage_host = false
config.hostmanager.include_offline = true

  #Machine 1 - DB
config.vm.define "db01" do |db|
  db_specs = machines["db01"]
  db.vm.hostname = db_specs["hostname"]
  db.vm.network "private_network",
    ip: db_specs["ip"]
  db.vm.provider "virtualbox" do |vb|
    vb.memory = db_specs["memory"]
    vb.cpus = db_specs["cpus"]
    end
  end
  #machine 2 - Memcached
  config.vm.define "mc01" do |memcached|
    mc_specs = machines["mc01"]
    memcached.vm.hostname = mc_specs["hostname"]
    memcached.vm.network "private_network",
      ip: mc_specs["ip"]
    memcached.vm.provider "virtualbox" do |vb|
      vb.memory = mc_specs["memory"]
      vb.cpus = mc_specs["cpus"]
    end
  end
  #machine 3 - rmq01
  config.vm.define "rmq01" do |rmq|
    rmq_specs = machines["rmq01"]
    rmq.vm.hostname = rmq_specs["hostname"]
    rmq.vm.network "private_network",
      ip: rmq_specs["ip"]
    rmq.vm.provider "virtualbox" do |vb|
      vb.memory = rmq_specs["memory"]
      vb.cpus = rmq_specs["cpus"]
    end
  end

  #machine 4 - app01
  config.vm.define "app01" do |app|
    app_specs = machines["app01"]
    app.vm.hostname = app_specs["hostname"]
    app.vm.network "private_network",
      ip: app_specs["ip"]
    app.vm.provider "virtualbox" do |vb|
      vb.memory = app_specs["memory"]
      vb.cpus = app_specs["cpus"]
    end
  end

  #machine 5 - web01
  config.vm.define "web01" do |web|
    web_specs = machines["web01"]
    web.vm.hostname = web_specs["hostname"]
    web.vm.network "private_network",
      ip: web_specs["ip"]
    #web.vm.network "forwarded_port",
      #guest: 80,
      #host: 8088,
      #host_ip: "127.0.0.1"
    web.vm.provider "virtualbox" do |vb|
      vb.memory = web_specs["memory"]
      vb.cpus = web_specs["cpus"]
    end
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
  # by making sure your Vagrantfile isn't accessible to the vagrant box.
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
