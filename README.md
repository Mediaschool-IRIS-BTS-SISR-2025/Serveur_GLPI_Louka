# 📦 Projet Serveur GLPI – Louka (BTS SISR)

Ce projet contient l’infrastructure Docker permettant de déployer **GLPI**, **MariaDB** et **phpMyAdmin** sur un serveur Linux. Il est conçu pour être facilement déployable sur n’importe quel serveur (VM locale ou serveur physique).

---

## 🌐 Services inclus

| Service        | Port Serveur (hôte) | Port Conteneur | Description |
|----------------|--------------------|----------------|-------------|
| **GLPI**       | 80                 | 80             | Interface web GLPI |
| **MariaDB**    | 3306               | 3306           | Base de données utilisée par GLPI |
| **phpMyAdmin** | 8081               | 80             | Interface web d’administration SQL |

---

## 🐳 Déploiement avec Docker

- Installer Docker et Docker Compose :  
  sudo apt update && sudo apt install -y docker.io docker-compose
  sudo systemctl enable docker --now

- Ouvrir les ports nécessaires : 80 (GLPI), 3306 (MariaDB), 8080 (phpMyAdmin)
  
- Avoir un utilisateur avec droits sudo

- Créer le fichier docker-compose.yml dans un dossier /home/USER/glpi-docker/

- Lancez les conteneurs :
  cd /home/USER/glpi-docker/
  sudo docker compose up -d

- Vérifier que tous les conteneurs sont actifs :
  sudo docker ps

- Accès aux services :
  GLPI : http://IP_SERVEUR/
  
  phpMyAdmin : http://IP_SERVEUR:8081
  
  MariaDB : localhost:3306 depuis le serveur ou via phpMyAdmin





