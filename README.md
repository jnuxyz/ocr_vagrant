# OCR Vagrant Projet 03

Construire avec Vagrant une machine virtuelle Debian 10 avec Emacs, Ansible et Docker.

## Prérequis

- Vagrant v2+
- VirtualBox v6+

## Installation

1. Cloner le projet et se déplacer dans son répertoire :

    ```shell
    git clone https://github.com/jnuxyz/ocr_vagrant.git
    cd ocr_vagrant
    ```

2. Crée et configure la machine virtuelle **ocr** en fonction du Vagrantfile :

    ```shell
    vagrant up
    ```

3. Vérifier l’état de la machine virtuelle **ocr** :

    ```shell
    vagrant status
    ```

4. Se connecter à la machine virtuelle **ocr** en SSH :

    ```shell
    vagrant ssh
    ```

5. Arrêter la machine virtuelle **ocr** en cours d’exécution :

    ```shell
    vagrant halt
    ```

6. Arrêter et détruire machine virtuelle **ocr** :

    ```shell
    vagrant destroy
    ```

Pour voir toutes les commandes Vagrant : `vagrant --help` ou voir la [documentation Vagrant](https://www.vagrantup.com/docs/cli).