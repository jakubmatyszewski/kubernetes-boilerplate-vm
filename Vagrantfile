IMAGE_NAME = "bento/debian-11"
N = 1

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false
      
    config.vm.define "k8s-master" do |master|
        master.vm.box = IMAGE_NAME
        master.vm.network "private_network", ip: "192.168.50.10"
        master.vm.hostname = "k8s-master"
	master.vm.provider "virtualbox" do |vb|
	    vb.memory = 4096
	    vb.cpus = 2
	end
        master.vm.provision "ansible" do |ansible|
            ansible.playbook = "kubernetes-setup/ping.yml"
            ansible.extra_vars = {
                node_ip: "192.168.50.10",
            }
        end
    end

    (1..N).each do |i|
        config.vm.define "node-#{i}" do |node|
            node.vm.box = IMAGE_NAME
	    node.vm.network "private_network", ip: "192.168.50.#{i + 10}"
            node.vm.hostname = "node-#{i}"
            node.vm.provider "virtualbox" do |vb|
		vb.memory = 2048
		vb.cpus = 1
	    end
	    node.vm.provision "ansible" do |ansible|
                ansible.galaxy_command = 'ansible-galaxy collection install community.docker kubernetes.core'
                ansible.playbook = "kubernetes-setup/ping.yml"
                ansible.extra_vars = {
                    node_ip: "192.168.50.#{i + 10}",
                }
            end
        end
    end
end
