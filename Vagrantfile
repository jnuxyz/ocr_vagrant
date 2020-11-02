# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    # Spécifie le nom de la box sur laquelle la VM doit être construite
    config.vm.box = "debian/buster64"
    # Définit le nom d'hôte de la VM
    config.vm.hostname = 'ocr'
    # Spécifie de fonctionner en réseau privé et d'utiliser une adresse IP statique pour la VM
    config.vm.network "private_network", ip: "192.168.66.6"
    # Définit les redirections de ports de la VM 
    # Port invité suivi du port hôte par lequel le port invité est accessible
    config.vm.network "forwarded_port", guest: 8080, host: 8080
    config.vm.network "forwarded_port", guest: 4433, host: 4433
    config.vm.network "forwarded_port", guest: 2022, host: 2022
    config.vm.network "forwarded_port", guest: 8000, host: 8000

    #config.vm.synced_folder "home_vagrant", "/home/vagrant/", type: "nfs"

    # Si on veut copier des fichiers dans la VM
    # config.vm.provision "file", source: "Dockerfile", destination: "Dockerfile"
    
    # Permet d'exécuter un script dans la VM
    config.vm.provision "shell", inline: <<-SHELL
        # Mise à jour dépôts
        apt update
        # Installe packages prérequis
        apt install -y apt-transport-https ca-certificates curl software-properties-common gnupg2
        # Ajoute clé GPG Ansible
        apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
        # Ajoute dépôt Ansible
        add-apt-repository "deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main"
        # Ajoute clé GPG Docker
        curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
        # Ajoute dépôt Docker
        add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"
        # Mise à jour dépôts
        apt update
        # Installe Vim, Ansible et Docker
        apt install -y vim ansible docker-ce docker-ce-cli containerd.io
        # Ajoute l'utilisateur 'vagrant' au groupe 'docker'
        usermod -aG docker vagrant
    SHELL

    # Permet la configuration de paramètres VirtualBox
    config.vm.provider :virtualbox do |v|
        # Personnalise le nom qui apparaît dans l'interface graphique de VirtualBox
        v.name = "ocr"
        v.memory = 5120
        v.cpus = 3
    end
end