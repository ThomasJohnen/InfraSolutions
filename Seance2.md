# Séance 2

### exercice 1 : Déployer un site en HTML

1) Installer apache2

```bash
 apt install apache2 -y
```

- facultatif : installer Lynx et tester apache

```bash
 apt install lynx -y
```

```bash 
 lynx http://localhost
```

Normalement, le site d'appache doit être visible.

2) Une fois le dossier du site HTML transférer il faut configurer un Virtualhost dans le dossier sites-available avec le fichier.conf: 

```bash
sudo nano etc/apache2/sites-available/monsite.conf
```

Voici ce qu'il faut écrire dedans :

```bash
<VirtualHost *:80>
        ServerName monsite

        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/htdocs/monsite
        ErrorLog ${APACHE_LOG_DIR}/monsite_error.log
        CustomLog ${APACHE_LOG_DIR}/monsite_access.log combined

        <Directory /var/www/htdocs/monsite>
        Require all granted
        AllowOverride All
        </Directory>
</VirtualHost>
```

Il ne faut pas oublier que dans la balise <virtualHost> il y a *:80. Ce 80 représente le port d'écoute. 


3) Quand on a dit sur quel port on voulait écouté, si ce n'est pas le port 80, il faut vérifier dans :

```bash
/etc/apache2/ports.conf
``` 

si ce port d'écoute est bien mentionné.

4) Ensuite, bien rajouter le nom du ServerName mentionné dans le virtualHost dans le fichier Hosts à l'adresse : 

```bash
/etc/hosts
```

Voici à quoi ressemble le code : 

```bash
127.0.0.1       localhost
::1             localhost ip6-localhost ip6-loopback
ff02::1         ip6-allnodes
ff02::2         ip6-allrouters
127.0.0.1       monsite
```

Ensuite faire : 

```bash
sudo a2ensite monsite.conf
```

puis :

```bash
sudo systemctl reload apache2
```

Si l'on relance lynx, on obtient le site : 


```bash
lynx http://monsite
```


#### ET VOILA ! 
---

### exercice 1 : Déployer un site en PHP


1) Si il faut installer Apache et Lynx, se référencer à l'exo 1

2) Installer PHP, module PHP pour apache et SQL : 

```bash
sudo apt install php php-mysql libapache2-mod-php -y
```

php : c'est php.

php-mysql :  C'est le nom du package PHP pour le support de MySQL. Il s'agit d'une extension PHP qui permet à PHP d'interagir avec les bases de données MySQL.

libapache2-mod-php : C'est le nom du package qui fournit le module Apache pour PHP. Ce module permet à Apache de comprendre et d'exécuter des scripts PHP.

3) Installer MySQL

```bash
sudo apt install default-mysql-server
```


4) Injecter un fichier de création DB :

```bash
sudo mysql -u username -p < file.sql
```

ATTENTION ! Il peut être utile de créer un user sql. Pour ça :

```bash
sudo mysql -u root
```


une fois connecté il faut exécuté ces commandes SQL : 

```sql
CREATE USER 'username'@'localhost' IDENTIFIED BY 'votre_mot_de_passe';

GRANT ALL PRIVILEGES ON *.* TO 'username'@'localhost';
```

Après celà, on peut revenir au point 5


5) reload Apache

```bash
systemctl reload apache2
```









