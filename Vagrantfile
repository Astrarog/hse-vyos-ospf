Vagrant.configure("2") do |config|
  config.vm.define "rt0" do |server|
    server.vm.box = "ubuntu/trusty64"

    # for outside world
    # server.vm.network "private_network", ip: "10.10.0.1", netmask: "255.255.255.0"

    # do basic setup
    server.vm.provision "shell", privileged: false, path: "basic-setup.sh"

    # run native bgpd
    server.vm.provision "shell", path: "run-gobgpd.sh", args: "0"
  end

end
