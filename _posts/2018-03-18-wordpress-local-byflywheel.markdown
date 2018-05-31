---
layout: post
title: 'Travailler en local avec Wordpress:  Local by Flywheel'
date: '2018-03-18 21:33:36'
tags:
- decouverte
- cms
navigation: True
current: post
cover: content/images/water.jpg
navigation: True
class: post-template
author: schaptal
---


Pour ceux qui ont déjà eu à travailler en local avec wordpress, vous savez qu'il faut installer MAMP (ou WAMP, ou LAMP, suivant le système d'exploitation) et que ce n'est pas toujours facile. Aujourd'hui, je vais vous faire découvrir une alternative simple pour faire du wordpress en local. Je vais vous parler de Local by Flywheel. 

Local By Flywheel permet grâce à des machines virtuelles, de déployer de multiples instances de WordPress, avec si vous le désirez un certificat SSL et un accès SSH, le tout en quelques clics.

## Installation

Commençons par le téléchargement du logiciel dont vous aurez besoin; rendez-vous sur le site de [Flywheel](https://local.getflywheel.com) et lancez le téléchargement en cliquant sur le bouton Download.

Avant de pouvoir lancer le téléchargement vous allez avoir le choix entre la version d’installation, Mac ou Windows.

Ensuite, il vous faudra renseigner un formulaire avec plein d'informations. Cependant, une adresse mail suffit pour le valider :) 

Le logiciel est gratuit et le fichier d’installation pèse 475 Mo.


Ensuite, lancer l’installeur et suivez la procédure d’installation.

<img src="/content/images/2018/03/install_localbyflywheel.png" style="width:50%;"/>

Ici Flywheel va installer tous les éléments techniques et fichiers nécessaire au bon fonctionnement de votre site (serveur local, fichier wordpress, base de données…) 


## Créer son site

Sur l’écran d’accueil, ajoutez un site.

1. Le nom de votre site internet: Choisissez ce que vous voulez 😉(j'ai mis iserv, mais sachez que celui-ci ne tourne pas sous wordpress 😊)
2. Local site/path : l’endroit/dossier où sera stocké votre site sur votre disque dur

<img src="/content/images/2018/03/Capture-d-e-cran-2018-03-18-a--13.50.00.png" style="width:90%;"/>

Lors de la mise en place d’une instance, vous pouvez avoir  un environnement de base ou vous pouvez choisir votre version de PHP, de MySQL et le serveur qui le fera tourner (Nginx ou Apache).

<img src="/content/images/2018/03/Capture-d-e-cran-2018-03-18-a--10.38.42.png" style="width:90%;"/>
<i>environnement de base</i>

<img src="/content/images/2018/03/Capture-d-e-cran-2018-03-18-a--10.38.49.png" style="width:90%;"/>
<i>environnement custom</i>
<br>

Pour terminer votre installation, il ne vous reste plus que 3 champs à renseigner:

**WordPress Username** : Identifiant de connexion à votre administration
**WordPress Password** : Mot de Passe pour accéder à votre administration
**WordPress Email** : Votre adresse email

<img src="/content/images/2018/03/Capture-d-e-cran-2018-03-18-a--10.39.23.png" style="width:90%;"/>

En Option : S’agit-il d’un multisite ? Non par défaut, interessant si vous voulez créer un réseau de sites wordpress

C’est bon, le nouveau site est créé !


#### Recréer votre site

Si vous avez déjà une instance de wordpress, pour la recréer, il vous suffira: 
* d'importer un backup de votre base de données (via l'onglet Database et le bouton Adminer)
* de copier votre thème et vos plugins dans le dossier de votre Wordpress, dans respectivement app/public/wp-content/themes et app/public/wp-content/plugins

