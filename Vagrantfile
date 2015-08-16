# -*- mode: ruby -*-

Vagrant.configure("2") do |config|

    # Which box should we use for the VM?
    config.vm.box = "ubuntu/trusty64"

    # Insert SSH keys if needed.
    config.ssh.insert_key = true

    # Which (private) IP address should the VM have?
    config.vm.network :private_network, ip: "192.168.0.222"

    # Where should our synced folder exist on the VM?
    config.vm.synced_folder "#{ENV['HOME']}", "#{ENV['HOME']}"

    # Install docker on the VM.
    config.vm.provision "docker"

end
