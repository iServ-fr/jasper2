---
layout: post
title: Installation de SolR 6 sous CentOS
date: '2018-05-19 18:49:59'
tags:
- tuto
---

J'ai souvent utilisé le moteur d'indexation SolR (basé sur lucene) que ce soit pour mes développements ou en production. Nous allons installer la version 6 de SolR et en faire un service, pour que SolR soit plus facilement gérable en ligne de commande.

> J'ai hésité à publier cet article, car SolR en est à sa version 7 mais j'ai constaté que la version 6 intéresse et est toujours utilisée dans beaucoup de projets.

# Installation
Tout d'abord, vérifier si vous avez la version 1.8 ou + du JRE (Java Runtime Environment), avec un petit `java -version` dans votre terminal.

![javaversion](/content/images/javaversion.png)


Ensuite, vous pouvez récupérer la version de solr 6 que vous souhaitez (en remplaçant les x et y par votre version): 

```shell
wget http://archive.apache.org/dist/lucene/solr/6.x.y/solr-6.x.y.tgz
```

Après avoir récupéré votre version de solr, lancez cette commande pour récupérer le script d'installation dans le dossier courant.

```shell
tar xzf solr-6.x.y.tgz solr-x.y.0/bin/install_solr_service.sh --strip-components=2
```

Et on lance le script d'installation:
```shell
sudo bash ./install_solr_service.sh solr-6.3.0.tgz
```

Votre instance de solr est maintenant disponible à l'adresse: http://nomdedomaine:8983/solr
 
A noter qu'il peut y avoir des problèmes au niveau du firewall

```shell
sudo firewall-cmd --zone=public --add-port=8983/tcp --permanent
sudo firewall-cmd --reload
```

# Création du service
Lors de l'installation, un service solr a été crée et son script de démarrage se trouve dans le dossier /etc/init.d .
S'il n'existe pas, il faut donc créer le fichier /etc/init.d/solr avec le contenu suivant:
```shell
SOLR_INSTALL_DIR=/opt/solr
SOLR_ENV=/etc/default/solr.in.sh
RUNAS=solr
```
* SOLR_INSTALL_DIR correspond au dossier d'installation de SolR
* SOLR_ENV correspond au fichier contenant les variables d'environnements
* RUNAS correspond au nom du service
Il vous faut l'adapter à vos besoins :)

Vous pouvez maintenant gérer SolR comme n'importe quel service, en ligne de commande:
`sudo service solr start`
`sudo service solr stop`
`sudo service solr restart`

# Sécurité
###### Via htacess
Pour sécuriser votre installation de SolR, vous pouvez mettre en place un htpasswd via apache en ajoutant les lignes suivantes dans votre vhost
```shell
AuthType Basic
AuthName "Restricted Content"
AuthUserFile /etc/httpd/.htpasswd
Require valid-user
```

###### Via iptables

L'autre solution est de passer par iptables
```shell
iptables -A INPUT -p tcp -s localhost --dport 8983 -j ACCEPT
iptables -A INPUT -p tcp -s votre.adresse.ip.ici --dport 8983 -j ACCEPT
iptables -A INPUT -p tcp --dport 8983 -j DROP
```
La première commande iptables accepte toutes les connexions de localhost sur le port 8983, la seconde accepte les connexions depuis votre ip, et la dernière dit à iptables d'abandonner tout le trafic au port 8983. 
Iptables obéit aux règles de haut en bas donc, les trafics depuis localhost et depuis votre ip, sont laissés passer, le reste est refusé.
Pour enregistrer ces règles de manière permanente (afin qu'elles persistent après un redémarrage), assurez-vous de sauvegarder la configuration du pare-feu avec `sudo service iptables save`.