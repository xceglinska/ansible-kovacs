# Installer Ansible

**Challenge n°1 :**

!<img width="903" height="141" alt="image" src="https://github.com/user-attachments/assets/e612fd0f-033b-4f0f-a30b-980c08e34422" />



L'exécution de la commande ansible --version confirme que le paquet a été correctement installé sur la VM.




**Challenge n°2 :** 

L'ajout du dépôt PPA `ppa:ansible/ansible` permet d'accéder à une version plus récente d'Ansible.

<img width="888" height="202" alt="image" src="https://github.com/user-attachments/assets/975b192a-3893-4e6b-a407-58b47311a8d0" />


**Challenge n°3 :** 

L'installation a été effectuée dans un environnement virtuel isolé sur Rocky Linux, permettant d'utiliser une version spécifique d'Ansible indépendamment du système.

<img width="901" height="219" alt="image" src="https://github.com/user-attachments/assets/a62af88b-a8d7-428c-902f-14f76b5f614c" />


# Authentification

Test de connexion Ansible vers les trois nœuds cibles (`target01`, `target02`, `target03`) en utilisant l'utilisateur `vagrant` et le module `ping`.

<img width="726" height="403" alt="image" src="https://github.com/user-attachments/assets/fdf22543-e669-42de-b2cb-dfbcce757c58" />


# Configuration de base


# Idempotence

Installation des paquets `tree`, `git` et `nmap` sur l'ensemble des cibles (`suse`, `debian`, `rocky`) en utilisant le module générique `package`.

<img width="634" height="419" alt="image" src="https://github.com/user-attachments/assets/a4818468-c66c-474f-9c40-7634ab6e75b1" />


Suppression des paquets `tree`, `git` et `nmap` sur toutes les cibles en basculant l'état souhaité sur `absent`.

<img width="786" height="375" alt="image" src="https://github.com/user-attachments/assets/1aa1da59-b267-496f-9ed5-0809f498e8d7" />

Transfert du fichier `/etc/fstab` depuis le nœud de contrôle vers les nœuds cibles sous le nom `/tmp/test3.txt`.

<img width="907" height="787" alt="image" src="https://github.com/user-attachments/assets/2b63ff24-d04b-44d8-b0f3-b51b3540ae6b" />

Suppression du fichier `/tmp/test3.txt` sur l'ensemble des cibles en utilisant le module `file` avec l'état `absent`.

<img width="728" height="284" alt="image" src="https://github.com/user-attachments/assets/2cbed476-80d5-41ea-8af1-017896639225" />

Exécution de la commande système `df -h /` via le module par défaut `command` pour vérifier l'occupation de la partition racine sur toutes les cibles.

Statut CHANGED : Bien qu'il s'agisse d'une commande de lecture seule, Ansible retourne CHANGED car il a exécuté un binaire arbitraire sur le système distant et ne peut pas garantir que l'état de la machine n'a pas été modifié.

<img width="593" height="186" alt="image" src="https://github.com/user-attachments/assets/36ee0362-d272-4559-a394-2530bdaec61c" />

# Un serveur web simple

Un premier playbook apache-debian.yml qui installe Apache sur l'hôte debian avec une page personnalisée Apache web server running on Debian Linux:

<img width="605" height="696" alt="image" src="https://github.com/user-attachments/assets/22212cb3-51b3-40d2-a914-72be3681ffd0" />

Un deuxième playbook apache-rocky.yml qui installe Apache sur l'hôte rocky avec une page personnalisée Apache web server running on Rocky Linux.

<img width="593" height="641" alt="image" src="https://github.com/user-attachments/assets/bfe99e8f-93d8-4c8a-929d-96488a38e601" />

Un troisième playbook apache-suse.yml qui installe Apache sur l'hôte suse avec une page personnalisée Apache web server running on SUSE Linux.

<img width="571" height="620" alt="image" src="https://github.com/user-attachments/assets/7f9286fb-a3aa-4772-8c8e-35f57443c457" />

# Les handlers

Rédaction d'un playbook `chrony.yml` pour automatiser l'installation, la configuration et la gestion du service NTP sur l'ensemble des hôtes.

<img width="507" height="747" alt="image" src="https://github.com/user-attachments/assets/2b7f9310-7034-4a80-8241-fbe2ce0e7504" />

# Les variables

Rédaction du playbook `myvars1.yml` pour démontrer la définition et l'appel de variables simples au sein d'un Play.

<img width="498" height="353" alt="image" src="https://github.com/user-attachments/assets/7b071fa5-3759-4c5a-9457-0306ca657040" />

Test de la priorité des variables en utilisant l'option `-e` (extra vars) pour surcharger les valeurs définies dans le playbook `myvars1.yml`.

<img width="1063" height="303" alt="image" src="https://github.com/user-attachments/assets/b5b662fe-e982-4569-8f23-cf32b7faf30c" />

Rédaction du playbook `myvars2.yml` utilisant le module `set_fact` pour définir des variables de manière dynamique durant l'exécution des tâches.

<img width="492" height="366" alt="image" src="https://github.com/user-attachments/assets/e6b87bdc-968f-47ad-b53b-2e077f41b78f" />

Test de la priorité des *extra vars* sur les variables définies dynamiquement avec `set_fact` dans le playbook `myvars2.yml`.

<img width="1048" height="354" alt="image" src="https://github.com/user-attachments/assets/09aa84ad-4711-4bf5-8fc1-d843169b3c0a" />

Rédaction du playbook `myvars3.yml` et configuration des valeurs par défaut via l'arborescence des variables d'inventaire. Pour répondre à l'énoncé, les variables sont définies dans `group_vars/all.yml` afin d'être appliquées à tous les hôtes.

<img width="434" height="268" alt="image" src="https://github.com/user-attachments/assets/5610a359-2ae0-4cf7-9834-5973cc964067" />
<img width="1033" height="294" alt="image" src="https://github.com/user-attachments/assets/df86bcb0-0282-4290-9469-b0b929425aa0" />

Pour surcharger les valeurs par défaut (définies précédemment dans `group_vars/all.yml`) spécifiquement pour l'hôte `target02`, on utilise le répertoire `host_vars`.

<img width="204" height="84" alt="image" src="https://github.com/user-attachments/assets/d930e2cc-6a2a-4819-b1d9-e1330edffebc" />

Rédaction du playbook `display_users.yml` utilisant la directive `vars_prompt` pour définir les variables `user` et `password` avec leurs valeurs par défaut, tout en activant l'option `private: true` pour masquer la saisie du mot de passe.

<img width="805" height="400" alt="image" src="https://github.com/user-attachments/assets/f05580bc-9aab-43af-92b8-6bf76cf56222" />

# Les variables enregistrées

Exécution du playbook `kernel.yml` sur les différents hôtes cibles (`debian`, `rocky`, `suse`), illustrant la récupération des informations système via la commande `uname -a` et leur affichage détaillé dans la console grâce au module `debug`.

<img width="528" height="255" alt="image" src="https://github.com/user-attachments/assets/8888eea8-275f-40bf-a765-b5c1acba3a9c" />
<img width="900" height="525" alt="image" src="https://github.com/user-attachments/assets/5710d76c-412b-467e-8820-b93c76cab760" />

Exécution du playbook `kernel2.yml` démontrant l'utilisation du paramètre `var` du module `debug` pour afficher directement le contenu de la variable `uname_output.stdout`, offrant une structure de sortie au format JSON pour les informations du noyau.

<img width="508" height="252" alt="image" src="https://github.com/user-attachments/assets/741e735e-ac78-45ce-b16c-4f08e422d6e2" />
<img width="901" height="533" alt="image" src="https://github.com/user-attachments/assets/52df95e7-037a-474c-a38d-9c871de9f268" />

Lancement du playbook `packages.yml` ciblant les hôtes `rocky` et `suse` pour exécuter la commande de comptage des paquets RPM et afficher le résultat formaté via un message de debug.

<img width="768" height="257" alt="image" src="https://github.com/user-attachments/assets/d4b1dfe8-ee35-4568-b988-84ed6d026beb" />
<img width="896" height="379" alt="image" src="https://github.com/user-attachments/assets/b6957f04-5b16-4b7e-9664-7bf03f2b015c" />

# Facts et variables implicites

Définition du playbook `pkg-info.yml` exploitant la variable de fact `ansible_pkg_mgr` pour identifier automatiquement le gestionnaire de paquets (`apt`, `dnf` ou `zypper`) propre à chaque distribution.

<img width="744" height="185" alt="image" src="https://github.com/user-attachments/assets/db452d49-b198-48e2-86df-02bcfce5dc1c" />
<img width="899" height="478" alt="image" src="https://github.com/user-attachments/assets/91dbc15b-1d17-4ab4-a045-d1426469ed08" />

`python-info.yml` pour afficher la version de Python installée:

<img width="822" height="184" alt="image" src="https://github.com/user-attachments/assets/3cde4f8c-ea6d-49e6-83ba-3cd3e2cf78b0" />
<img width="903" height="479" alt="image" src="https://github.com/user-attachments/assets/0a19ccf3-7512-4764-aee9-b0696d19c9a8" />

`dns-info.yml` pour afficher le(s) serveur(s) DNS utilisé(s)

<img width="865" height="197" alt="image" src="https://github.com/user-attachments/assets/1535af87-6e0f-4dd9-8136-72432c41d3f4" />
<img width="898" height="488" alt="image" src="https://github.com/user-attachments/assets/045d2ef7-2fa0-4433-ab8e-2ded1ca076d3" />

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

