# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "debian-7.3.0-amd64"
  config.vm.box_url = "https://dl.dropboxusercontent.com/s/u0uyn1cxgzyui9f/debian-7.3.0-amd64.box"

  config.vm.network :forwarded_port, guest: 80, host: 8080
  config.vm.network :private_network, ip: "192.168.111.222"

  # config.vm.provider :virtualbox do |vb|
  #   vb.customize ["modifyvm", :id, "--memory", "2048"]
  # end

  # If true, then any SSH connections made will enable agent forwarding.
  # Default value: false
  # config.ssh.forward_agent = true

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/ansible-playbook.yml"
    ansible.inventory_path = "provisioning/hosts"
    ansible.host_key_checking = false
    ansible.extra_vars = { ntp_server: "pool.ntp.org", nginx: { port: 8008, workers: 4 } }
    ansible.sudo = true
    ansible.verbose = false
  end
end
