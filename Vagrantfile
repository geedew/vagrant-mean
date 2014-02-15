# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.define "app1", primary: true do |app|
    # Every Vagrant virtual environment requires a box to build off of.
    app.vm.box = "ubuntu_saucy64"

    app.vm.hostname = "app1.localhost"

    # The url from where the 'config.vm.box' box will be fetched if it
    # doesn't already exist on the user's system.
    app.vm.box_url = "http://cloud-images.ubuntu.com/vagrant/saucy/current/saucy-server-cloudimg-amd64-vagrant-disk1.box"


    # Create a forwarded port mapping which allows access to a specific port
    # within the machine from a port on the host machine. 
    app.vm.network :forwarded_port, guest: 3000, host: 3000

    # Create a private network, which allows host-only access to the machine
    # using a specific IP.
    app.vm.network :private_network, ip: "192.168.33.101"

    # Create a public network, which generally matched to bridged network.
    # Bridged networks make the machine appear as another physical device on
    # your network.
    # app.vm.network :public_network

    # If true, then any SSH connections made will enable agent forwarding.
    # Default value: false
    # app.ssh.forward_agent = true

    # Share an additional folder to the guest VM. The first argument is
    # the path on the host to the actual folder. The second argument is
    # the path on the guest to mount the folder. And the optional third
    # argument is a set of non-required options.
    # app.vm.synced_folder "../data", "/vagrant_data" 
    app.vm.synced_folder "./code", "/mnt/code", :nfs => true

    # Provider-specific configuration so you can fine-tune various
    # backing providers for Vagrant. These expose provider-specific options.
    # Example for VirtualBox:
    #
    app.vm.provider :virtualbox do |vb|
      # Don't boot with headless mode
      # vb.gui = true
    
      # Use VBoxManage to customize the VM. For example to change memory:
      vb.customize ["modifyvm", :id, "--memory", "1024"]
      vb.customize ["modifyvm", :id, "--cpus", "4"]
      vb.customize ["modifyvm", :id, "--ioapic", "on"]
    end

    app.vm.provision "ansible" do |ansible|
      ansible.inventory_path = "files/hosts"
      ansible.playbook = "tasks/main.yml"
      # ansible.verbose = 'vvvv'
    end
  end

end
