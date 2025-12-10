# 📦 Projet Serveur GLPI – Louka (BTS SISR)

Ce projet contient l’infrastructure Docker permettant de déployer **GLPI**, **MariaDB** et **phpMyAdmin** sur un serveur Linux. Il est conçu pour être facilement déployable sur n’importe quel serveur (VM locale ou serveur physique).

---

## Structure du projet :

/
├── README.md
├── LICENSE            # (optionnel, selon licence du projet)
├── docker-compose.yml
├── .env.example       # modèle de fichier .env (variables d’environnement)
├── configs/           # configurations externes / custom (volumes Docker, overrides, etc.)
│    ├── apache/       # config Apache / Nginx / VirtualHost, ssl, etc.
│    ├── php/          # config PHP (php.ini, etc.) si besoin de customisation
│    └── mariadb/      # config base de données (my.cnf, init scripts, etc.) si utile
├── data/              # données persistantes (volumes Docker), ignorées par git
│    ├── glpi_data/    # données GLPI (fichiers uploadés, logs, fichiers config externes, etc.)
│    └── mysql_data/   # données MariaDB / MySQL
├── scripts/           # scripts utiles (setup, backup, restore, migration, etc.)
│    ├── backup.sh
│    ├── restore.sh
│    └── update_glpi.sh  # script d’update si automatisation
├── docs/              # documentation du projet
│    ├── INSTALL.md    # instructions d’installation (prérequis, étapes, ports, etc.)
│    ├── USAGE.md      # comment utiliser le serveur, accéder à GLPI, etc.
│    ├── CONFIG.md     # documentation des variables .env, options, custom config, ...
│    └── ARCHITECTURE.md  # diagramme / description de l’architecture (réseau, conteneurs, volumes…)
├── .gitignore         # ignorer data/, logs, .env, etc.
└── (optional) ansible/ or provisioning/  # si tu veux gérer via Ansible ou autre outil d’automatisation
     ├── playbook.yml
     └── roles/




