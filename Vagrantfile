IMAGE_NAME = "bento/ubuntu-16.04"
N = 2

Vagrant.configure("2") do |config|
      config.vm.provision "shell", inline: <<-SHELL
          apt-get update -y
          echo "10.0.1.10  master-node" >> /etc/hosts
          echo "10.0.1.11  worker-node01" >> /etc/hosts
          echo "10.0.1.12  worker-node02" >> /etc/hosts
      SHELL
      
      config.vm.define "k8s-master" do |master|
        master.vm.box = "bento/ubuntu-16.04"
        master.vm.hostname = "k8s-master-node"
        master.vm.network "private_network", ip: "10.0.1.10"
        master.vm.provider "virtualbox" do |vb|
            vb.memory = 4048
            vb.cpus = 2
        end
        master.vm.provision "shell", path: "scripts/common.sh"
        master.vm.provision "shell", path: "scripts/master.sh"
      end
  
      (1..N).each do |i|
    
      config.vm.define "node0#{i}" do |node|
        node.vm.box = "bento/ubuntu-16.04"
        node.vm.hostname = "k8s-worker-node0#{i}"
        node.vm.network "private_network", ip: "10.0.1.1#{i}"
        node.vm.provider "virtualbox" do |vb|
            vb.memory = 2048
            vb.cpus = 1
        end
        node.vm.provision "shell", path: "scripts/common.sh"
        node.vm.provision "shell", path: "scripts/node.sh"
      end
      
      end
    end





# Vagrant.configure("2") do |config|
#     config.vm.provision "shell", inline: <<-SHELL
#         apt-get update -y
#         echo "10.0.1.10  master-node" >> /etc/hosts
#         echo "10.0.1.11  worker-node01" >> /etc/hosts
#         echo "10.0.1.12  worker-node02" >> /etc/hosts
#     SHELL
    
#     config.vm.define "master" do |master|
#       master.vm.box = "bento/ubuntu-16.04"
#       master.vm.hostname = "master-node"
#       master.vm.network "private_network", ip: "10.0.1.10"
#       master.vm.provider "virtualbox" do |vb|
#           vb.memory = 4048
#           vb.cpus = 2
#       end
#       master.vm.provision "shell", path: "scripts/common.sh"
#       master.vm.provision "shell", path: "scripts/master.sh"
#     end

#     (1..2).each do |i|
  
#     config.vm.define "node0#{i}" do |node|
#       node.vm.box = "bento/ubuntu-16.04"
#       node.vm.hostname = "worker-node0#{i}"
#       node.vm.network "private_network", ip: "10.0.1.1#{i}"
#       node.vm.provider "virtualbox" do |vb|
#           vb.memory = 2048
#           vb.cpus = 1
#       end
#       node.vm.provision "shell", path: "scripts/common.sh"
#       node.vm.provision "shell", path: "scripts/node.sh"
#     end
    
#     end
#   end