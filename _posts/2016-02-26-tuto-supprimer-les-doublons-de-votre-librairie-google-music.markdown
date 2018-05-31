---
title: "[Tuto] Supprimer les doublons de votre librairie Google Music"
date: '2016-02-26 15:15:00'
tags:
- tuto
navigation: True
layout: post
current: post
cover: assets/images/water.jpg
navigation: True
class: post-template
author: vfleurette
---

J'aime bien Google Music, c'est l'un des seuls services google que j'utilise avec Gmaps. J'ai utilisé leur outil pour transférer ma bibliothèque iTunes (Oui iTunes marche plutôt bien sur Mac.. pas sous windows). Google Music a un double intérêt. Je peux avoir ma musique partout sans avoir mon propre ordi et également de sauvegarde en plus de la  time machine. Cependant, je n'aime pas le Google Music Uploader : il n'est pas assez intelligent pour reconnaître quand une chanson de votre bibliothèque est déjà dans le nuage, donc si jamais vous devez reconfirer l'outil, vous aurez des centaines ou même des milliers de chansons en double. Et jusqu'à ce qu'un ingénieur de Google décide de fixer le problème, vous êtes coincé avec une bibliothèque en désordre et une expérience utilisateur dégradée.

### Conditions préalables

Ce guide est destiné à Mac OS X ou Centos. Pour suivre celui-ci, vous aurez besoin de:

1.  Un système d'exploitation Mac ou Centos
2.  Une bonne connexion Wi-Fi ou Ethernet.
3.  Un terminal
4.  Une bibliothèque Google Music.
5.  Python 2.7.10 (Python 3.5 ne fonctionnera pas avec ce script).
6.  Les outils en ligne de commande OS X / Xcode.
7.  [gmusicapi](https://unofficial-google-music-api.readthedocs.org/en/latest/) non - officiel .
8.  Si vous utilisez l' authentification à deux facteurs sur votre compte Google, vous aurez également besoin d'un [mot de passe spécifique à l'application](https://security.google.com/settings/security/apppasswords) à utiliser exclusivement avec le gmusicapi.
  

### Sous Mac uniquement

En premier lieu, installez les outils de ligne de commande OS X / Xcode

Nous avons besoin d'installer les outils de ligne de commande Xcode. Ouvrez une fenêtre de terminal et exécutez

`xcode-select --install`

et suivez les instructions à l'écran pour terminer l'installation.

### Sous Centos 5/6/7

`yum install -y python-pip`

### Installer gmusicapi

pip rend l'installation de paquets Python facile. Dans Terminal,

`pip install gmusicapi`

### Télécharger [deletegmusicdupes.py](https://gist.githubusercontent.com/sebvance/060da84f55b13837b310/raw/a6c6bf367f8fd092f7b0e76a65ee1a17b93db20b/DeleteGmusicDupes.py)

Enregistrez-le quelque part. Ceci est le script qui va identifier vos doublons, et proposer de les supprimer. Vous pouvez consulter le [code source ici](https://gist.github.com/sebvance/060da84f55b13837b310) .

### Exécuter deletegmusicdupes.py

Dans Terminal, accédez au dossier où vous avez enregistré DeleteGmusicDupes.py. Ensuite, exécutez:

`python deletegmusicdupes.py`

Lorsque vous êtes invité à saisir votre "Nom d'utilisateur", utilisez votre adresse e-mail Google. Lorsque vous êtes invité à entrer votre mot de passe, indiquez votre mot de passe spécifique à l'application. Une fois connecté, le script vous affichera une liste des doublons dans votre compte - il peut y en avoir des centaines. Il vous demandera si vous voulez supprimer les doublons. Eh bien, oui, à ce stade, vous le faites probablement.

L'API ne peut retourner tous les résultats à la fois, donc si vous avez une grande bibliothèque, vous aurez besoin pour exécuter le script plusieurs fois. Exécutez à nouveau le script (vous serez invité à vous connecter à chaque fois) jusqu'à ce que le script signale "pas de doublons trouvés»

### Actualiser Google Music

Vous avez terminé! Merci d'avoir consulté cet article et à bientôt.