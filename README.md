SSH Access
==========

Gestion de l'accès ssh à la machine.

2 principales actions :

(0. Installation de la commande sudo si nécessaire) 
1. Création d'un compte ssh avec accès sudo, sur le groupe admin (crée si non présent)
2. Ajout de clefs ssh publiques sur ce compte

Requirements
------------

Role Variables
--------------

- doit-on vérifier la présence de la commande sudo ? (dans ce cas le user de lancement doit pouvoir passer root)
    check_sudo_cmd: False
- nom du compte sudoer sur lequel ajouter des clefs d'accès (obligatoire)
    ssh_account: xxx
- liste des clefs ssh publiques à ajouter sur le compte sudoer
    ssh_users:
        - name: xxx
          key: "ssh-rsa AAAABBBBBCCCCCCCCCC"

Dependencies
------------


Example Playbook
----------------

# Exemple d'ajout d'un compte xxxx avec accès ssh pour toto :

    - hosts: all
      vars:
        - ssh_account: xxxx
        - ssh_users:
          - name: toto
            key: "ssh-rsa AAA"
      roles:
        - { role: steamroles/ssh }

License
-------


Author Information
------------------

STEAMULO - http://www.steamulo.com