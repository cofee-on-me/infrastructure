VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

	config.vm.box = "ubuntu/trusty64"
	config.vm.box_check_update = false

	config.ssh.forward_agent = true

	# folder sync
	config.vm.synced_folder "~/Repositories/infrastructure/backend", "/srv/backend",
		mount_options: ["dmode=755,fmode=644"]

	# port forwarding
	config.vm.network :forwarded_port, guest: 3000, host: 3000
	config.vm.network :private_network, ip: '192.168.10.2'

	config.vm.provider :virtualbox do |vb|
		vb.customize ["modifyvm", :id, "--memory", 2048]
		vb.customize ["modifyvm", :id, "--cpus", 2]
		vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
		vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
	end

	config.vm.provision "ansible" do |ansible|
		ansible.playbook = "provision.yml"
	end

end
