Vagrant.configure("2") do |config|
  # We will use Ubuntu 22.04 for the VMs
  config.vm.box = "ubuntu/jammy64" 

  # VM 1: 1 GB RAM, 1 CPU
  config.vm.define "vm1" do |v|
    v.vm.hostname = "vm1"
    v.vm.network "private_network", ip: "192.168.56.11"
    v.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.cpus = 1
    end
  end

  # VM 2: 2 GB RAM, 1 CPU
  config.vm.define "vm2" do |v|
    v.vm.hostname = "vm2"
    v.vm.network "private_network", ip: "192.168.56.12"
    v.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
      vb.cpus = 1
    end
  end

  # VM 3: 4 GB RAM, 2 CPUs
  config.vm.define "vm3" do |v|
    v.vm.hostname = "vm3"
    v.vm.network "private_network", ip: "192.168.56.13"
    v.vm.provider "virtualbox" do |vb|
      vb.memory = "4096"
      vb.cpus = 2
    end
  end
end