Serveur GLPI – Louka (BTS SISR 2025)
Présentation

Ce dépôt contient toutes les instructions pour installer et configurer GLPI sur un serveur physique Debian/Ubuntu.
Le serveur inclut Apache, MariaDB, PHP avec toutes les extensions nécessaires, ainsi que l’option d’installer l’agent GLPI.

Ports nécessaires
Service	Port	Description
GLPI	80	Interface web GLPI accessible via http://IP_DU_SERVEUR/glpi
MariaDB	3306	Base de données GLPI
phpMyAdmin	8080	Interface web pour gérer la base de données (optionnel)
SSH	22	Accès distant sécurisé au serveur
Installation de GLPI sur le serveur physique
1️⃣ Mettre à jour le système
sudo apt update && sudo apt upgrade -y

2️⃣ Installer le serveur LAMP (Apache + MariaDB + PHP)
sudo apt install -y apache2 mariadb-server mariadb-client \
php php-mysql php-gd php-curl php-intl php-xml php-mbstring \
php-ldap php-zip php-bcmath php-opcache php-cli wget

3️⃣ Configurer MariaDB pour GLPI
sudo mysql


Dans MariaDB :

CREATE DATABASE glpidb CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
CREATE USER 'glpiuser'@'localhost' IDENTIFIED BY 'MotDePasseSecurise';
GRANT ALL PRIVILEGES ON glpidb.* TO 'glpiuser'@'localhost';
FLUSH PRIVILEGES;
EXIT;

4️⃣ Télécharger et installer GLPI
cd /tmp
wget https://github.com/glpi-project/glpi/releases/latest/download/glpi.tgz
tar -xvzf glpi.tgz
sudo mv glpi /var/www/html/
sudo chown -R www-data:www-data /var/www/html/glpi
sudo chmod -R 755 /var/www/html/glpi

5️⃣ Configurer Apache pour GLPI

Créer le fichier /etc/apache2/sites-available/glpi.conf :

<VirtualHost *:80>
    DocumentRoot /var/www/html/glpi
    <Directory /var/www/html/glpi>
        AllowOverride All
        Require all granted
    </Directory>
    ErrorLog ${APACHE_LOG_DIR}/glpi_error.log
    CustomLog ${APACHE_LOG_DIR}/glpi_access.log combined
</VirtualHost>


Activer le site et le module rewrite :

sudo a2ensite glpi.conf
sudo a2enmod rewrite
sudo systemctl restart apache2

6️⃣ Vérifier Apache
sudo ss -tuln | grep :80
curl http://localhost/glpi

7️⃣ (Optionnel) Installer l’agent GLPI sur le serveur
wget -O- https://github.com/glpi-project/glpi-agent/releases/latest/download/glpi-agent_linux_installer.sh | sudo bash
sudo glpi-agent --debug --force

Accès à GLPI

Depuis le serveur : http://localhost/glpi

Depuis un autre poste du réseau : http://IP_DU_SERVEUR/glpi

💡 Assurez-vous que le port 80 est ouvert dans le firewall si nécessaire.

Sécurisation et bonnes pratiques

Pour sécuriser le dossier racine d’Apache, vous pouvez placer GLPI dans /var/www/html/glpi/public et ajuster le DocumentRoot.

Sauvegardez régulièrement la base de données et le dossier /var/www/html/glpi/files.

Changez les mots de passe par défaut de MariaDB et GLPI.

Maintenance

Redémarrer Apache :

sudo systemctl restart apache2


Redémarrer MariaDB :

sudo systemctl restart mariadb


Vérifier les logs Apache :

sudo tail -f /var/log/apache2/error.log


Vérifier les logs GLPI :

sudo tail -f /var/www/html/glpi/files/_log/php-errors.log

Auteur

Projet réalisé par Louka, BTS SISR – 2025.
