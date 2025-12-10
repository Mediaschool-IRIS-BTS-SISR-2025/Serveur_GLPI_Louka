# 📦 Projet Serveur GLPI – Louka (BTS SISR)

Ce projet contient l’infrastructure Docker permettant de déployer **GLPI** et **MariaDB** sur un serveur Linux. Il est conçu pour être facilement déployable sur n’importe quel serveur (VM locale ou serveur physique).
---

# 📁 Structure du projet — Serveur GLPI

Ce projet permet de déployer un serveur **GLPI** avec **Docker** (GLPI + MariaDB).
L’objectif est d’avoir une solution de gestion de parc informatique **facile à installer, configurer et maintenir**.

---

## 🧱 Arborescence du projet

```
Serveur_GLPI/
├── README.md                # Documentation principale du projet
├── docker-compose.yml       # Orchestration des conteneurs (GLPI + DB)
├── .env.example             # Modèle de fichier .env (variables d’environnement)
├── .gitignore               # Fichiers/dossiers à ne pas versionner
│
├── configs/                 # Configurations personnalisées (optionnel)
│   ├── apache/              # Config Serveur Web (SSL, vhost…)
│   ├── php/                 # Config PHP (php.ini…)
│   └── mariadb/             # Config DB (my.cnf, init scripts…)
│
├── data/                    # Données persistantes des conteneurs (non versionnées)
│   ├── glpi_data/           # Données GLPI (documents, plugins, logs…)
│   └── mysql_data/          # Base de données MariaDB
│
├── scripts/                 # Scripts utiles pour l’administration
│   ├── backup.sh            # Sauvegarde BDD + données GLPI
│   ├── restore.sh           # Restauration complète
│   └── update_glpi.sh       # Mise à jour de GLPI
│
└── docs/                    # Partie documentation du projet
    ├── INSTALL.md           # Installation et prérequis
    ├── USAGE.md             # Accès au service, utilisateurs, FAQ
    ├── CONFIG.md            # Variables .env, configuration Docker
    └── ARCHITECTURE.md      # Schéma + description du fonctionnement
```

---

## 📌 Description rapide

| Élément              | Rôle                                                               |
| -------------------- | ------------------------------------------------------------------ |
| `docker-compose.yml` | Déploie automatiquement GLPI + MariaDB                             |
| `.env.example`       | Sert de modèle pour créer le `.env` avec les bons paramètres       |
| `data/`              | Contient les fichiers persistant au redémarrage des conteneurs     |
| `configs/`           | Permet de personnaliser la configuration par défaut                |
| `scripts/`           | Aide pour sauvegarder / restaurer / mettre à jour le serveur       |
| `docs/`              | Documentation complète du projet pour installation & compréhension |

---

## 🚀 Déploiement rapide

1️⃣ Copier le fichier `.env.example` → `.env`
2️⃣ Modifier les mots de passe et paramètres dans `.env`
3️⃣ Lancer l’installation :

```bash
docker compose up -d
```

4️⃣ Accéder à GLPI :

```
http:/glpi.iris.a3n.fr/:8080
```

---

## 🔐 Sécurité

✔ Ne **jamais** pousser le fichier `.env` sur GitHub
✔ Le dossier `data/` doit **rester local** → ajouté au `.gitignore`
✔ Sauvegardes régulières recommandées (script fourni)

---

## 🧩 Services compris

| Service | Port | Description                      |
| ------- | ---- | -------------------------------- |
| GLPI    | 80   | Interface Web de gestion de parc |
| MariaDB | 3306 | Base de données de GLPI          |

---

## 🛠 Maintenance

| Fonction         | Script                   |
| ---------------- | ------------------------ |
| Sauvegarde       | `scripts/backup.sh`      |
| Restauration     | `scripts/restore.sh`     |
| Mise à jour GLPI | `scripts/update_glpi.sh` |

---

## ✨ Auteur

Projet de déploiement GLPI
🔧 Réalisé dans le cadre du BTS SIO SISR
👤 Lavenir Louka — Mediaschool IRIS




