---
title: Tuto Comment installer PHP 7 OS X El Capitan
featured: true
date: '2016-01-18 08:57:00'
tags:
- php
- tuto
navigation: True
layout: post
current: post
cover: https://images.unsplash.com/photo-1488590528505-98d2b5aba04b?ixlib=rb-0.3.5&q=80&fm=jpg&crop=entropy&cs=tinysrgb&w=1080&fit=max&s=278085b2f7e71c40d0bd45a0e1fc06df
unsplash: true
navigation: True
class: post-template
author: vfleurette
---


Dans ce court tutoriel, vous apprendrez comment installer la dernière version de PHP7 sur OS X en utilisant homebrew et comment le configurer dans le serveur Apache.
Vous pourriez vous demander en premier lieu, pourquoi se donner la peine de l’installer.

![Tuto Comment installer PHP 7](https://i.giphy.com/OY4dDgEBdTjy0.gif) 

La principale motivation pour moi a été un coup de pouce de la performance. Il est probable qu’il ne tourne toujours pas plus vite que les versions précédentes de PHP fonctionnant sur Facebook HHVM. Néanmoins, il y a une amélioration **significative** des performances sans HHVM (qui mange beaucoup de RAM).

# Tuto Comment installer PHP 7
 
### Comment l’installer?

Ce tutoriel est pour OS X, mais certaines procédures peuvent être appliquées pour certaines versions de linux centos/debian (notamment pour la configuration d’Apache)

D’abord, si vous ne l'avez pas déjà, récupérer Homebrew.
Homebrew est un gestionnaire de paquets pour OS X. Pour les instructions d’[installation Ici](https://brew.sh/).

### Installer PHP 7 via Homebew

Exécutez les commandes suivantes dans votre console:

    $ brew tap homebrew/dupes
    $ brew tap homebrew/versions
    $ brew tap homebrew/homebrew-php
    
    //Installation

    $ brew install php70

    //Si vous avez installé des versions antérieures avec homebrew
    //vous avez besoin de supprimer le lien

    $ brew unlink php56

### Configurer Apache

Ouvrez le fichier de configuration d’Apache par défaut avec votre éditeur de texte favori.

    //Ouvrir avec vim ou tout autre éditeur de texte
    $ sudo vim /etc/apache2/httpd.conf

    //Si vous ne voulez pas utiliser la console uniquement, vous pouvez ouvrir le dossier dans le Finder

    $ open /etc/apache2/
    //Rechercher php5_module (qui devrait être près de la ligne 171) et modifier le httpd.conf comme ceci:

    #Commenter le module PHP5
    #LoadModule php5_module libexec/apache2/libphp5.so

    #activer le module PHP 7
    LoadModule php7_module /usr/local/opt/php70/libexec/apache2/libphp7.so
    SetHandler application/x-httpd-php


### Redémarer apache

Exécutez cette commande pour redémarrer le serveur Apache d’OS X par défaut:

    $ sudo apachectl restart

Si vous rencontrez des erreurs ou si vous voulez tester votre fichier httpd.conf, exécutez ‘apachectl’ dans le terminal.

Sinon c'est lundi..., on annonce de la neige sur Montpellier

![Tuto Comment installer PHP 7](https://i.giphy.com/NhcmPmXRUUbAY.gif) 

et c'est l'heure du petit dej...

