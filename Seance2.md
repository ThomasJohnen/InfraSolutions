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


ET VOILà ! 