---
title: Installation du serveur MariaDB
date: '2015-07-14 11:28:00'
tags:
- sysadmin
- tuto
navigation: True
layout: post
current: post
cover: content/images/water.jpg
navigation: True
class: post-template
author: vfleurette
---

#### Tuto MariaDB : Installation du serveur MariaDB via la commande suivante

```shell 
yum install mariadb mariadb-server
```

Sur CentOS, le démon mysqld n’est pas configuré pour se lancer au démarrage de la machine. Nous allons le configurer pour qu’il se lance à chaque démarrage via la commande suivante :

```shell 
systemctl enable mariadb.service
```

Afin de pouvoir lancer l’outil de configuration MariaDB, nous allons lancer le service via la commande :

```shell 
systemctl start mariadb.service
```

Maintenant nous pouvons lancer l’outil de configuration MariaDB pour configurer le mot de passe de root (« mariadb » par exemple), supprimer les utilisateurs anonymes, supprimer les bases de tests et désactiver la possibilité pour root de se connecter à distance via la commande :

```shell 
/usr/bin/mysql_secure_installation
Enter current password for root (enter for none) : Taper sur la touche Entrer
Set root password? [Y/n] Taper sur la touche Entrer
Remove anonymous users? [Y/n] Taper sur la touche Entrer
Disallow root login remotely? [Y/n] Taper sur la touche Entrer
Remove test database and access to it? [Y/n] Taper sur la touche Entrer
Reload privilege tables now? [Y/n] Taper sur la touche Entrer
```

#### Installation des librairies php5-mysql via la commande suivante
```shell 
yum install php-mysql
```

On doit maintenant activer le support de MariaDB dans PHP via la commande suivante :

```shell 
systemctl restart httpd
```



<br><br>
*Image crédité à Mike Zinner of [mariadb.org] [<a href="https://creativecommons.org/licenses/by-sa/3.0">CC BY-SA 3.0</a> or <a href="http://www.gnu.org/copyleft/fdl.html">GFDL</a>], <a href="https://commons.wikimedia.org/wiki/File%3AMariadb-seal-browntext.svg">via Wikimedia Commons</a>*
