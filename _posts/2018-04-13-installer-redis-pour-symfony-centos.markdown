---
layout: post
title: Installer redis pour votre projet Symfony sur CentOS 7
date: '2018-04-13 17:00:00'
tags:
- php
- tuto
navigation: True
current: post
cover: content/images/water.jpg
navigation: True
class: post-template
author: schaptal
---

Comme beaucoup, vous avez du déjà voir passer le mot "redis", au moins dans des articles ou dans des réunions avec des adminsys. Redis est un système de gestion de base de données clef-valeur scalable, très hautes performances, écrit en C ANSI et distribué sous licence BSD.

Sa vitesse et sa facilité d'utilisation en font l'une des solutions les plus populaires de système de cache pour toutes les applications qui nécessitent de bonnes performances et notamment les applications web qui ont besoin d'afficher des pages très rapidement.

En plus, si vous voulez l'intégrer à votre projet Symfony, ce n'est pas très compliqué :)

![allonsy](/content/images/2018/04/allonsy.gif)

### Installation de redis sur le serveur CentOS 7


###### Ajoutez le repo EPEL et faites un yum update pour confirmer votre modification:

```console
sudo yum install epel-release
sudo yum update
```

###### Installez Redis:
```console
sudo yum install redis
```

###### Démarrer Redis
```console
sudo systemctl start redis
```

###### Facultatif : 
Pour démarrer automatiquement Redis au démarrage du serveur (ça peut éviter les mauvaises suprises lors de reboot)
```console
sudo systemctl enable redis
```

###### Vous pouvez faire un test via cette commande: 
```console
redis-cli ping
````

###### Si redis est en cours d'exécution, il vous répondra
```
PONG
```

Remarque: si vous souhaitez faire un cluster redis, je vous conseille le tuto de [data-essential](https://www.data-essential.com/setup-a-secured-redis-cluster-on-centos7/) ou de [digital ocean](https://www.digitalocean.com/community/tutorials/how-to-configure-a-redis-cluster-on-centos-7) qui sont très bien fait.

Maintenant que redis est installé sur le serveur, occupons nous du projet Symfony.

### Installation de SncRedisBundle

Il existe deux versions du bundle, l’une utilisant une extension PHP qu’il vous faudra installer sur votre système d’exploitation, l’autre qui utilise la librairie Phredis (et qui ne nécessite pas l’installation de l’extension).
C'est de la version Phredis dont il s'agit ici.

Allez dans le dossier de votre projet symfony avec ```cd```.
Une fois dans votre projet, vous pouvez installer le bundle avec Composer:
```console
composer require snc/redis-bundle predis/predis
````

Ensuite, modifiez le fichier app/AppKernel.php (avec votre éditeur de texte préféré) et ajoutez le nouveau bundle :)
```php
    $bundles = array(
        // ...
        new Snc\RedisBundle\SncRedisBundle(),
        // ...
    );
```
    
### Configuration de SncRedisBundle
Pour stocker vos sessions dans Redis, il vous suffit d’ajouter la configuration ci-dessous:

dans votre fichier config.yml: 
```yaml
snc_redis:
    clients:
        default:
            type: predis
            alias: default
            dsn: redis://localhost
    session:
        client: default
        prefix: session
```
Vous pouvez configurer beaucoup d'éléments et faire face à de nombreux cas d'utilisation. Pour cela, direction le [README](https://github.com/snc/SncRedisBundle/blob/master/Resources/doc/index.md).

Et voila, vous avez votre nouveau système de cache, et ça c'est beau.

![youareawesome](/content/images/2018/04/youareawesome.jpg)