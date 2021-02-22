# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    # Spécifie le nom de la box sur laquelle la VM doit être construite
    config.vm.box = "hashicorp/bionic64"
    # Définit le nom d'hôte de la VM
    config.vm.hostname = 'ocr'
    # Spécifie de fonctionner en réseau privé et d'utiliser une adresse IP statique pour la VM
    config.vm.network "private_network", ip: "192.168.5.5"
    # Définit les redirections de ports de la VM 
    # Port invité suivi du port hôte par lequel le port invité est accessible
    config.vm.network "forwarded_port", guest: 80, host: 80
    config.vm.network "forwarded_port", guest: 443, host: 443
    config.vm.network "forwarded_port", guest: 22, host: 22

    #config.vm.synced_folder "home_vagrant", "/home/vagrant/"

    # Si on veut copier des fichiers dans la VM
    # config.vm.provision "file", source: "Dockerfile", destination: "Dockerfile"
    
    # Permet d'exécuter un script dans la VM
    config.vm.provision "shell", inline: <<-SHELL
        # Mise à jour dépôts
        apt update
        # Installe packages prérequis
        apt install -y apt-transport-https ca-certificates curl software-properties-common gnupg-agent
        # Ajoute clé GPG Ansible
        apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
        # Ajoute dépôt Ansible
        add-apt-repository "deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main"
        # Ajoute clé GPG Docker
        curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
        # Ajoute dépôt Docker
        add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
        # Ajoute clé GPG Terraform
        curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
        # Ajoute dépôt Terraform
        sudo apt-add-repository "deb [arch=$(dpkg --print-architecture)] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
        # Mise à jour dépôts
        apt update
        # Installe Vim, Ansible, Docker, Terraform et awscli
        apt install -y vim ansible docker-ce docker-ce-cli containerd.io terraform awscli
        # Ajoute l'utilisateur 'vagrant' au groupe 'docker'
        usermod -aG docker vagrant
    SHELL

    # Permet la configuration de paramètres VirtualBox
    config.vm.provider :virtualbox do |v|
        # Personnalise le nom qui apparaît dans l'interface graphique de VirtualBox
        v.name = "ocr"
        v.memory = 4096
        v.cpus = 2
    end
end
