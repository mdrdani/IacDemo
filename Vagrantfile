Vagrant.configure("2") do |config|

     config.vm.box = "ubuntu/xenial64"
     config.vm.provision "file", source: "hosts", destination: "/tmp/hosts"
     config.vm.provision "file", source: "ssh/ansible_ssh_key.pub", destination: "/home/vagrant/.ssh/ansible_ssh_key.pub"
     config.vm.provision "shell", path: "common.sh"
     config.vm.synced_folder "../", "/devops"

     config.vm.define "ansible" do |node|
          node.vm.hostname = "ansible"
          node.vm.network "private_network", ip: "192.168.45.10"
          config.vm.provider :virtualbox do |vb|
               vb.customize ["modifyvm", :id, "--memory", "3048"]
               vb.customize ["modifyvm", :id, "--cpus", "2"]
          end
          config.vm.provision "file", source: "ssh/ansible_ssh_key", destination: "/home/vagrant/.ssh/id_rsa"
          node.vm.provision "shell", path: "install_ansible.sh"
          node.vm.provision "shell", path: "install_docker.sh"
     end
end