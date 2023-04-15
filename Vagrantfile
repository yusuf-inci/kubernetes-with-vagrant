# -*- mode: ruby -*-
# vi: set ft=ruby :

# Define the number of control plane and worker nodes
NUM_CONTROLLERS = 1
NUM_WORKERS = 2

Vagrant.configure("2") do |config|

    # Enable and configure hostmanager plugin
    config.hostmanager.enabled = true 
    config.hostmanager.manage_host = true
  
  # Install the Ubuntu 20.04 LTS image
    config.vm.box = "ubuntu/bionic64"

  # Create the control plane nodes
  (1..NUM_CONTROLLERS).each do |i|
    config.vm.define "k8s-control#{i}" do |node|
      node.vm.hostname = "k8s-control#{i}"
      node.vm.network "private_network", ip: "192.168.101.#{i+10}"
      node.vm.provider "virtualbox" do |vb|
        vb.memory = "2048"
        vb.cpus = "2"
      end
    #   node.vm.provision "shell", inline: <<-SHELL
        # # Install Docker
        # sudo -i
        # apt-get update
        # apt-get install -y apt-transport-https ca-certificates curl gnupg lsb-release
        # # curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
        # # # echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
        # apt-get update
        # apt-get install -y docker-ce docker-ce-cli containerd.io
        # sudo systemctl start containerd

        # # Install kubeadm, kubelet, and kubectl
        # apt-get update
        # apt-get install -y apt-transport-https curl
        # curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
        # # echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | tee -a /etc/apt/sources.list.d/kubernetes.list
        # apt-get update
        # apt-get install -y kubelet kubeadm kubectl
        # apt-mark hold kubelet kubeadm kubectl

        # # Initialize the control plane node
        # # kubeadm init --control-plane-endpoint "192.168.101.10:6443" --upload-certs --pod-network-cidr=10.244.0.0/16

        # # Copy the kubeconfig file to the vagrant user's home directory
        # mkdir -p /home/vagrant/.kube
        # cp -i /etc/kubernetes/admin.conf /home/vagrant/.kube/config
        # chown vagrant:vagrant /home/vagrant/.kube/config

        # # Install the Flannel network plugin
        # # su - vagrant -c "kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml"

        # # Install the Kubernetes dashboard
        # # su - vagrant -c "kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0/aio/deploy/recommended.yaml"
    #   SHELL
        end
    end

   # Create the worker nodes
  (1..NUM_WORKERS).each do |i|
    config.vm.define "k8s-worker#{i}" do |node|
        node.vm.hostname = "k8s-worker#{i}"
        node.vm.network "private_network", ip: "192.168.101.#{i+20}"
        node.vm.provider "virtualbox" do |vb|
            vb.memory = "2048"
            vb.cpus = "2"
        end
    # node.vm.provision "shell", inline: <<-SHELL
    #   # Install Docker
    #   sudo -i
    #   apt-get update
    #   apt-get install -y apt-transport-https ca-certificates curl gnupg lsb-release
    # #   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
    # # #   echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    #   apt-get update
    #   apt-get install -y docker-ce docker-ce-cli containerd.io

    #   # Install kubeadm, kubelet, and kubectl
    #   apt-get update
    #   apt-get install -y apt-transport-https curl
    #   curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
    # #   echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | tee -a /etc/apt/sources.list.d/kubernetes.list
    #   apt-get update
    #   apt-get install -y kubelet kubeadm kubectl
    #   apt-mark hold kubelet kubeadm kubectl

    #   # Join the worker node to the cluster
    # #   su - vagrant -c "kubeadm join 192.168.101.10:6443 --token TOKEN --discovery-token-ca-cert-hash SHA256:HASH"
    # SHELL
        end
    end
end
