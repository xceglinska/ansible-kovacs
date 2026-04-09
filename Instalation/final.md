# Installer Ansible

**Challenge n°1 :**

![challenge 1.png](:/8acfd5db71e741beb8d1bc971a27a3ed)


L'exécution de la commande ansible --version confirme que le paquet a été correctement installé sur la VM.




**Challenge n°2 :** 

L'ajout du dépôt PPA `ppa:ansible/ansible` permet d'accéder à une version plus récente d'Ansible.

![challenge 2.png](:/a91503dc4f7a41e594be524d19483d9c)

**Challenge n°3 :** 

L'installation a été effectuée dans un environnement virtuel isolé sur Rocky Linux, permettant d'utiliser une version spécifique d'Ansible indépendamment du système.

![challenge 3.png](:/921ee3c00b07423591adb61e951620e1)

# Authentification

Test de connexion Ansible vers les trois nœuds cibles (`target01`, `target02`, `target03`) en utilisant l'utilisateur `vagrant` et le module `ping`.

![pingtarget.png](:/943965504a9e420a8fc62a7b3d3c9223)

# Configuration de base


# Idempotence

Installation des paquets `tree`, `git` et `nmap` sur l'ensemble des cibles (`suse`, `debian`, `rocky`) en utilisant le module générique `package`.

![idempotence1.png](:/f930758064bf479386b75c197245cef5)

Suppression des paquets `tree`, `git` et `nmap` sur toutes les cibles en basculant l'état souhaité sur `absent`.

![idempotence2.png](:/dc6c1ea694ca4e94acbd50363dbc520e)

Transfert du fichier `/etc/fstab` depuis le nœud de contrôle vers les nœuds cibles sous le nom `/tmp/test3.txt`.

![idempotence3.png](:/0d216fdf50e24a228b8e86c8d64f2e06)

Suppression du fichier `/tmp/test3.txt` sur l'ensemble des cibles en utilisant le module `file` avec l'état `absent`.

![idempotence4.png](:/9e4fe595795649ec923ae1ceed60ef17)

Exécution de la commande système `df -h /` via le module par défaut `command` pour vérifier l'occupation de la partition racine sur toutes les cibles.

Statut CHANGED : Bien qu'il s'agisse d'une commande de lecture seule, Ansible retourne CHANGED car il a exécuté un binaire arbitraire sur le système distant et ne peut pas garantir que l'état de la machine n'a pas été modifié.

![idempotence5.png](:/124e1e4c44784e78b368b352a0f98832)

# Un serveur web simple

Un premier playbook apache-debian.yml qui installe Apache sur l'hôte debian avec une page personnalisée Apache web server running on Debian Linux:

![apachedebian.png](:/fbf55e51701f4209b2632ee313b28017)

Un deuxième playbook apache-rocky.yml qui installe Apache sur l'hôte rocky avec une page personnalisée Apache web server running on Rocky Linux.

![apacherocky.png](:/1024fa7c928042e88b77e0acc0af71d0)

Un troisième playbook apache-suse.yml qui installe Apache sur l'hôte suse avec une page personnalisée Apache web server running on SUSE Linux.

![apachesuse.png](:/84df057b7b4340979be493a4949d88df)

# Les handlers

Rédaction d'un playbook `chrony.yml` pour automatiser l'installation, la configuration et la gestion du service NTP sur l'ensemble des hôtes.

![chrony.png](:/e5a8ed8288d844b699c93c4b491a71cb)

# Les variables

Rédaction du playbook `myvars1.yml` pour démontrer la définition et l'appel de variables simples au sein d'un Play.

![myvars1.png](:/4827f17bb7e84da6ba71437f6be0d547)

Test de la priorité des variables en utilisant l'option `-e` (extra vars) pour surcharger les valeurs définies dans le playbook `myvars1.yml`.

![myvars1extravars.png](:/c8850da5bf874885bdc4e03e2ab42752)

Rédaction du playbook `myvars2.yml` utilisant le module `set_fact` pour définir des variables de manière dynamique durant l'exécution des tâches.

![myvars2.png](:/caa17841383f42e7be56f12e5729a777)

Test de la priorité des *extra vars* sur les variables définies dynamiquement avec `set_fact` dans le playbook `myvars2.yml`.

![myvars2extravars.png](:/11adc1859f6d419a9f1ae760fbf79c3c)

Rédaction du playbook `myvars3.yml` et configuration des valeurs par défaut via l'arborescence des variables d'inventaire. Pour répondre à l'énoncé, les variables sont définies dans `group_vars/all.yml` afin d'être appliquées à tous les hôtes.

![myvars3.png](:/9660884e4f3144c086e101b06a242ee5)
![myvars3result.png](:/0c0742dbc6f44f029e03e3ff288c0523)

Pour surcharger les valeurs par défaut (définies précédemment dans `group_vars/all.yml`) spécifiquement pour l'hôte `target02`, on utilise le répertoire `host_vars`.

![myvars3target02.png](:/2472670234a84a77883efecc6f043689)

Rédaction du playbook `display_users.yml` utilisant la directive `vars_prompt` pour définir les variables `user` et `password` avec leurs valeurs par défaut, tout en activant l'option `private: true` pour masquer la saisie du mot de passe.

![display_users.png](:/f9025f66a17645f7a126096fd6efdf1e)

# Les variables enregistrées

Exécution du playbook `kernel.yml` sur les différents hôtes cibles (`debian`, `rocky`, `suse`), illustrant la récupération des informations système via la commande `uname -a` et leur affichage détaillé dans la console grâce au module `debug`.

![kernelyml.png](:/b06a76edf2bd4180a19cfd45549551ce)
![variable_enregistre1.png](:/f9c43add4fa24fb2b749aa1d0560f833)

Exécution du playbook `kernel2.yml` démontrant l'utilisation du paramètre `var` du module `debug` pour afficher directement le contenu de la variable `uname_output.stdout`, offrant une structure de sortie au format JSON pour les informations du noyau.

![kernel2yml.png](:/498859904afa4c87852df3bccd4afde5)
![var_enregistre2.png](:/4cce9ec8b0234c4985e1d6085c7f0659)

Lancement du playbook `packages.yml` ciblant les hôtes `rocky` et `suse` pour exécuter la commande de comptage des paquets RPM et afficher le résultat formaté via un message de debug.

![packagesyml.png](:/ec594bf9752c40819f98c004cb9980ac)
![var_enregistre3.png](:/d2844abe30a54c6c9661ed5847bb67b6)

# Facts et variables implicites

Définition du playbook `pkg-info.yml` exploitant la variable de fact `ansible_pkg_mgr` pour identifier automatiquement le gestionnaire de paquets (`apt`, `dnf` ou `zypper`) propre à chaque distribution.

![pkg-infoyml.png](:/9333b089f41648d6b29491b5781da47a)
![pkginforesult.png](:/0d57ccf08a7246b5ab6a6e2fbdf4766b)

`python-info.yml` pour afficher la version de Python installée:

![python-infoyml.png](:/7b5dfe27943744c197241cccb5f7f37a)
![python-inforesult.png](:/a6bf80f5c72a4d75824dd2e683db3927)

`dns-info.yml` pour afficher le(s) serveur(s) DNS utilisé(s)

![dns-infoyml.png](:/d006e9bca4164480a57261b684d6aeb2)
![dns-inforesult.png](:/903a5522a60f4f4c961a5692c38bef5a)

# Cibles hétérogènes

Premier playbook `chrony01.yml`

```yml
---
- name: Installation de Chrony avec modules natifs
  hosts: all
  become: true

  tasks:
    - name: Installation sur Debian/Ubuntu
      apt: { name: chrony, state: present }
      when: ansible_os_family == "Debian"

    - name: Installation sur Rocky Linux
      dnf: { name: chrony, state: present }
      when: ansible_os_family == "RedHat"

    - name: Installation sur SUSE
      zypper: { name: chrony, state: present }
      when: ansible_os_family == "Suse"

    - name: Configuration pour Debian/Ubuntu
      copy:
        dest: /etc/chrony/chrony.conf
        content: |
          server 0.fr.pool.ntp.org iburst
          server 1.fr.pool.ntp.org iburst
          server 2.fr.pool.ntp.org iburst
          server 3.fr.pool.ntp.org iburst
          driftfile /var/lib/chrony/drift
          makestep 1.0 3
          rtcsync
          logdir /var/log/chrony
      when: ansible_os_family == "Debian"
      notify: Restart Chrony

    - name: Configuration pour Rocky/SUSE
      copy:
        dest: /etc/chrony.conf
        content: |
          server 0.fr.pool.ntp.org iburst
          server 1.fr.pool.ntp.org iburst
          server 2.fr.pool.ntp.org iburst
          server 3.fr.pool.ntp.org iburst
          driftfile /var/lib/chrony/drift
          makestep 1.0 3
          rtcsync
          logdir /var/log/chrony
      when: ansible_os_family in ["RedHat", "Suse"]
      notify: Restart Chrony

    - name: Service sur Debian/Ubuntu
      service: { name: chrony, state: started, enabled: true }
      when: ansible_os_family == "Debian"

    - name: Service sur Rocky/SUSE
      service: { name: chronyd, state: started, enabled: true }
      when: ansible_os_family in ["RedHat", "Suse"]

  handlers:
    - name: Restart Chrony
      service:
        name: "{{ 'chronyd' if ansible_os_family in ['RedHat', 'Suse'] else 'chrony' }}"
        state: restarted

```

