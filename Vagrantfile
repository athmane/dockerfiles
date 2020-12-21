# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "fedora/33-cloud-base"
  config.vm.box_version = "33.20201019.0"

  # config.vm.box_check_update = false

  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # config.vm.network "private_network", ip: "192.168.33.10"

  # config.vm.network "public_network"

  # config.vm.synced_folder "../data", "/vagrant_data"

  #
  config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
     vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
     vb.memory = "4000"
  end
  config.vm.provision "shell", inline: <<-SHELL
    # Prepare the VM
    dnf -y update
    dnf -y install fedora-packager fedora-review
    dnf install -y @c-development @development-tools @rpm-development-tools

    # Docker installation
    dnf -y install dnf-plugins-core
    dnf config-manager \
        --add-repo \
        https://download.docker.com/linux/fedora/docker-ce.repo
    dnf install -y docker-ce docker-ce-cli containerd.io
    systemctl start docker
    systemctl enable docker

    #User creatation and repos setup
    useradd -G mock,docker athmane
    su - athmane sh -c "curl -s https://src.fedoraproject.org/user/athmane/projects | grep -o '>rpms/.*<' | tr -d '<>' | tee ~athmane/pkg_list"

  SHELL
end
