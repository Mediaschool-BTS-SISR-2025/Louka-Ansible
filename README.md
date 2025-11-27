# 📚 Projet Louka-Ansible – Déploiement GLPI & serveurs (BTS SISR)

## 📁 Structure du dépôt

.
├── dev-server-setup.yml # Playbook principal
├── inventory # Inventaire des serveurs
├── group_vars/
│ └── all.yml # Variables globales (DB, utilisateurs, ports…)
└── roles/
├── common/ # Paquets de base (git, vim, sudo, etc.)
│ └── tasks/main.yml
├── docker/ # Installation et configuration de Docker
│ └── tasks/main.yml
├── firewall/ # Configuration du pare-feu (UFW)
│ └── tasks/main.yml
├── users/ # Gestion des utilisateurs via CSV
│ ├── tasks/main.yml
│ └── files/users.csv
└── glpi/ # Installation et configuration de GLPI + Apache + MySQL
├── tasks/main.yml
└── templates/glpi.conf.j2


## 🛠️ Prérequis

- Ansible installé sur ta machine de gestion (ou VM).  
- Accès SSH (clé privée) au serveur cible.  
- Sur le serveur cible : Debian/Ubuntu ou équivalent compatible apt.  
- (Optionnel) pour utiliser Docker : architecture x86_64 (amd64).

## ⚙️ Variables globales

Modifie `group_vars/all.yml` pour adapter à ton environnement :
- `glpi.db_name`, `glpi.db_user`, `glpi.db_password` → configuration de la base GLPI.  
- `docker_users` → utilisateurs à ajouter au groupe docker.  
- `allow_ssh_port`, `allow_http_port`, `allow_https_port` → ports autorisés par le firewall.

## 🚀 Exécution

1. Adapter le fichier `inventory` avec l'adresse du serveur et la clé SSH.  
2. (Optionnel) si besoin d’un alias : modifier `ansible_host` dans `inventory`.  
3. Lancer le playbook :  
   ```bash
   ansible-playbook -i inventory dev-server-setup.yml

4. Ansible va alors :
  - Mettre à jour le système,
  - Installer les paquets de base,
  - Installer Docker (si sélectionné),
  - Configurer le pare-feu,
  - Créer les utilisateurs définis dans users.csv,
  - Installer GLPI, sa base MySQL, Apache et PHP,
  - Déployer GLPI prêt à l’emploi.

## Licence / Auteurs

Projet réalisé dans le cadre du BTS SISR — auteur : Louka.
Destiné à un usage pédagogique.
