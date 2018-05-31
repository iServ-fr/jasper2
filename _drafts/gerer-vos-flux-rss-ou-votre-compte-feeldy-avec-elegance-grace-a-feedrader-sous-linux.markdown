---
layout: post
title: feedafever
---

#### Un besoin de news fraiches

Si vous êtes en train de me lire, il y a de fortes chances que *iServ.fr* ne soit pas le seul site que vous suivez régulièrement et que faire votre veille tous les jours soit un peu le parcours du combattant. Continuez quand même à lire, la suite peut vous intéresser aussi.

Dès qu’on essaie de suivre l’actualité de plusieurs sites à la fois, on se retrouve rapidement abonné à leurs flux RSS, que ce soit via un navigateur web, un logiciel de messagerie ou un logiciel ad hoc (sur mac et iOS je recommande [reeder](http://reederapp.com) et sur android je recommande [Press](https://play.google.com/store/apps/details?id=com.twentyfivesquares.press&hl=fr)).

_Qu’est-ce qu’un flux RSS? 
C’est un fichier, mis à jour automatiquement à chaque fois que le contenu d’un site évolue, et accessible de l’extérieur, permettant donc à ces différents types de logiciels de savoir si un site a été mis à jour ou pas sans besoin de le visiter._

Si vous avez pris goût aux flux rss, vous aurez peut-être remarqué également qu’on en ajoute rapidement beaucoup, vraiment beaucoup, beaucoup trop, et à un certain moment, on en a tellement qu’on ne peut plus les lire.

> C’est là que rentre en jeu [Fever](http://feedafever.com) un logiciel payant 30€ en une fois à vie + toutes les mises à jour.

Fever ne s’installe pas comme un logiciel ordinaire sous Windows, Linux ou OS X, c’est une application web écrite en php nécessitant un serveur http avec php et une base de donéées MySQL.

Si vous ne disposez pas de votre serveur personnel hébergé quelque part, vous pouvez tout de même utiliser Fever grâce à un outil comme MAMP sur Mac ou WAMP sur PC qui permettent d’installer Apache, PHP, MySQL et les configurer simplement en quelques clics en local sur votre poste de travail.

#### Installation et configuration sur un server Centos 6/7

`mkdir /var/www/html/fever`
`cd /var/www/html/fever`
`wget http://feedafever.com/gateway/public/fever.zip`
`unzip fever.zip`

On va appliquer des nouveaux droits au dossier (à changer après l’installation, 777 c’est le mal).

`chmod 777 /var/www/html/fever`

Si vous avez deja une instance de mariadb et phpmyadmin, vous pouvez rapidement configurer un compte spécifique pour fever avec des droits dédiés à la base Fever, sinon voici comment faire pour installer et configurer [mariadb-server](https://iserv.fr/installation-du-serveur-mariadb/).

Ensuite en root :  
`mysql -u root -p`  
saisissez votre mot de passe.

On va ensuite créer une base de données avec des privilèges spécifiques à cette base (ne jamais utiliser une application avec les accès root, ceux là vous les gardez pour vous bien caché).

`create database fever; (le point virgule est important)  
grant all privileges on fever.* TO "root"@"localhost" identified by "your-password"; (changez your-password par le votre)`  
`flush privileges;  
exit;`

Pour ceux qui seraient effrayés par la ligne de commande, je recommande le logiciel [sequelpro](http://www.sequelpro.com) sous OS X (je n’ai malheureusement pas encore trouvé d’équivalent sous Fedora). Il me permet de faire rapidement toutes les commandes précédentes liées à la base de données via une belle interface graphique.

#### Création sur serveur virtuel

On commence par créer un document de configuration (j’utilise vim mais vous pouvez utiliser nano ou emacs).

`vim /etc/httpd/conf.d/fever.conf`

vous y copiez ceci :

```apacheconf
ServerName fever.yourdomain.com  
DocumentRoot /var/www/html/fever  
AllowOverride All  
Order Deny,Allow  
Allow from all  
```

et vous faites `esc` puis `:wq` pour sauvegarder et sortir de vim

toujours en root vous lancez :  
`apachectl configtest`

si la réponse est `OK` alors lancez :

`service http restart/reload`

sinon il va falloir trouver d’où vient l’erreur de votre configuration.

#### Tache cron

Un service de flux rss à jour c’est bien. Mais un service qui se met à jour tout seul toutes les 15 minutes, c’est bien mieux.

Pour cela, on va configurer un tache qui fonctionnera en background de votre système.

`crontab -e`  
et entrez la commande suivante

    */15 * * * * apache curl -L -s -k http://fever.yourdomain.com/?refresh
    

Visitez votre site web via http://fever.yourdomain.com et vous devriez voir l’interface Web pour la configuration de Fever. Entrez dans vos paramètres de base de données et cliquez sur `vérifier privilèges`:

<!-- ![checkup](https://iserv.fr/wp-content/uploads/2015/10/wpid-compatibility-fever.jpg) 
You’ll see something like this:

![boot](https://iserv.fr/wp-content/uploads/2015/10/wpid-fever-post-boot.jpg) -->

Maintenant revenez sur le site de FeedAFever pour acheter une licence, que vous pouvez entrer sur cet écran. Le processus d’installation automatisée va terminer le travail, Voila c’est tout bon.

> Enjoy !!!!!