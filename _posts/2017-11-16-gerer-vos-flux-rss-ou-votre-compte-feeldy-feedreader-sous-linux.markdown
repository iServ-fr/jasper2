---
title: Gérer vos Flux RSS ou votre Compte Feeldy, Feedreader sous Linux
featured: true
date: '2017-11-16 10:08:19'
tags:
- tuto
- decouverte
navigation: True
layout: post
current: post
cover: assets/images/water.jpg
navigation: True
class: post-template
author: vfleurette
---

Une de mes applications préférées sous Mac est Reeder. Jusqu'à présent je n'avais pas encore trouvé d’équivalent sous Linux avec une interface sexy et qui se synchronise avec un service RSS auto-hébergé ou non. Et puis j'ai découvert FeedReader. Si vous êtes un fan de la lecture des blogs et un grand consommateur de flux RSS, alors FeedReader est une très belle application pour organiser et gérer hors de votre fil de news. Il est compatible avec :

* Feedbin
* feedly
* FreshRSS
* InoReader
* Local RSS
* OwnCloud
* The Old Reader
* Tiny Tiny RSS

![Screenshot2](/assets/images/2017/11/Screenshot2.png)
Pour l'installer c'est très facile avec le terminal. Copiez et collez chaque ligne dans un terminal selon votre environnement et "Entrée" ...

***Ubuntu / Debian / Elementary OS / et autres dérivés de Debian***

    sudo add-apt-repository ppa:eviltwin1/feedreader-stable

    sudo apt-get update && sudo apt-get install feedreader

***Fedora***

    sudo dnf install feedreader

***Arch-Linux***

    yaourt -S feedreader

***Solus***

    sudo eopkg install feedreader

Ma seule réserve est qu'il ne s'agit pas d'un vrai gestionnaire de RSS mais plutôt d'un client RSS. Vous devrez créer un compte externe sur l'un des services RSS Web (généralement gratuits) comme InoReader, Feedly ou Tiny Tiny RSS. La beauté du service est que vos flux de blog seront tous synchronisés. FeedReader a quelques fonctionnalités intéressantes telles que le partage d'un article avec Pocket (récemment racheté par Mozilla), ainsi que les notifications de bureau pour les nouveaux articles, des raccourcis clavier, et les tags. Comme on le voit dans mon image FeedReader ci-dessus, nous avons la liste de nos blogs souscrits dans une zone sur le côté gauche. Si vous lisez beaucoup de blogs, vous pouvez les regrouper en catégories: blogs Linux, blogs Mac, les blogs Auto, quelques soient vos désirs.