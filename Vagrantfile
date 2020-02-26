Vagrant.configure("2") do |config|
  config.vm.define "rt1" do |server|
    server.vm.box = "higebu/vyos"

    # for outside world
    server.vm.network "private_network", ip: "10.10.0.10", netmask: "255.255.255.0"
    # for inside world
    server.vm.network "private_network", ip: "172.20.10.10", netmask: "255.255.255.0"

    server.vm.provider "virtualbox" do |virtualbox|
        # Enable promiscuous mode so the server can receive traffic
        # for the virtual machines and containers.
        virtualbox.customize [
            "modifyvm", :id,
            "--nicpromisc2", "allow-all"
        ]
    end

  end



  config.vm.define "rt2" do |server|
    server.vm.box = "higebu/vyos"

    # for outside world
    server.vm.network "private_network", ip: "10.10.0.20", netmask: "255.255.255.0"
    # for inside world
    server.vm.network "private_network", ip: "172.20.20.10", netmask: "255.255.255.0"

    server.vm.provider "virtualbox" do |virtualbox|
        # Enable promiscuous mode so the server can receive traffic
        # for the virtual machines and containers.
        virtualbox.customize [
            "modifyvm", :id,
            "--nicpromisc2", "allow-all"
        ]
    end

  end

  config.vm.define "rt3" do |server|
    server.vm.box = "higebu/vyos"

    # for outside world
    server.vm.network "private_network", ip: "10.10.0.30", netmask: "255.255.255.0"
    # for inside world
    server.vm.network "private_network", ip: "172.20.30.10", netmask: "255.255.255.0"

    server.vm.provider "virtualbox" do |virtualbox|
        # Enable promiscuous mode so the server can receive traffic
        # for the virtual machines and containers.
        virtualbox.customize [
            "modifyvm", :id,
            "--nicpromisc2", "allow-all"
        ]
    end

  end


end
