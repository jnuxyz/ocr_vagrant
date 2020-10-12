# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    config.vm.box = "debian/buster64"
    config.vm.hostname = 'ocr'
    config.vm.network "private_network", ip: "192.168.66.6"
    config.vm.network "forwarded_port", guest: 8080, host: 8080
    config.vm.network "forwarded_port", guest: 2022, host: 2022

    # Si on veut copier des fichiers dans la VM
    # config.vm.provision "file", source: "Dockerfile", destination: "Dockerfile"
    
    config.vm.provision "shell", inline: <<-SHELL
        apt update
        apt install -y apt-transport-https ca-certificates curl software-properties-common gnupg2
        apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
        add-apt-repository "deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main"
        curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
        add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"
        apt update
        apt install -y emacs-nox ansible docker-ce docker-ce-cli containerd.io
        usermod -aG docker vagrant
    SHELL

    config.vm.provider :virtualbox do |v|
        v.name = "ocr"
    end
end
