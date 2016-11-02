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
- liste des comptes sudoer à ajouter :
        ssh_sudo_users:
            - name: xxxx # nom du compte
              authorized: # liste des clefs autorisées
                - "ssh-rsa AAA"
              password: motdepasseCrypté  # mot de passe crypté manuellement en sha512 ( commande terminal : mkpasswd --method="SHA-512" )
              comment: "xxxx" # commentaire lié au compte
              no_history_protect: true # ne pas proteger l'history de ce user
- liste des comptes non sudoer à ajouter :

        ssh_standard_users:
          - name: toto
            comment: "Toto"
            password: motdepasseCrypté  # mot de passe crypté manuellement en sha512 ( commande terminal : mkpasswd --method="SHA-512" )
            authorized:
              - "ssh-rsa key 1"
              - "ssh-rsa key 2"
            group: maingroup
            groups: othergroup,otherothergroup
            createhome: true
- liste des comptes à supprimer :
        ssh_users_to_remove:
          - name: old_toto
- liste des comptes autres sur lesquels appliquer la sécurisation de l'historique et du bashrc/bash_profile :
        ssh_extra_user_to_protect:
          - name: tot2
            home: /toto2

Dependencies
------------


Example Playbook
----------------

# Exemple d'ajout d'un compte xxxx avec accès ssh pour toto :

    - hosts: all
      vars:
        ssh_sudo_users:
            - name: xxxx
              authorized:
                - "ssh-rsa AAA"
	      password: cryptedPassword
              comment: "xxxx"
              no_history_protect: true
        ssh_users_to_remove:
          - name: old_toto
        ssh_standard_users:
          - name: toto
            comment: "Toto"
            authorized:
              - "ssh-rsa key 1"
              - "ssh-rsa key 2"
      roles:
        - { role: steamroles/ssh }

License
-------


Author Information
------------------

STEAMULO - http://www.steamulo.com
