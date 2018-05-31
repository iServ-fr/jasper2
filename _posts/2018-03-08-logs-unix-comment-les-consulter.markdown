---
layout: post
title: 'Logs sous unix: comment les consulter ?'
date: '2018-03-08 13:27:16'
tags:
- sysadmin
- tuto
navigation: True
current: post
cover: content/images/water.jpg
navigation: True
class: post-template
author: schaptal
---

Il est probable que dans votre vie d'informaticien, vous devrez étudier des fichiers de logs, qu'ils viennent du système ou de vos applications. 
Après tout, ils sont là pour une raison très importante ... pour vous aider à résoudre un problème. 
En fait, chaque administrateur (ou développeur aussi ^^) chevronné vous demandera immédiatement en cas de problème: "*y a marqué quoi dans les logs ?*".

Il existe des logs pour tout: des logs system, pour le kernel, pour Apache, pour MySQL, etc. Pour chaque logiciel, application, service, il y a un fichier de log.

#### Où trouver ces fichiers de logs ?
Les logs system et les logs des services (apache, mariadb, ...) sont dans le dossier /var/log sous unix. Les logs des applications se trouvent à des dossiers différents/personnalisés et cela dépend des applications elles-mêmes.

Nous allons voir maintenant comment visualiser les logs.
> La suite de cet article sera concentré sur différentes manières d'afficher des logs sous linux (ou MacOS). Bien entendu, il ne s'agit pas d'une liste exhaustive. Il y a beaucoup de manières différentes de les visualiser. Je vais vous montrer les principaux que j'ai rencontré au cours de mes périgrinations.

## grep
Il s'agit d'une commande pour faire une recherche. En effet, il est possible de ne pas savoir exactement dans quel fichier se trouve l'information qui nous interresse. La plupart du temps, les developpeurs mettent certains mots clés pour spécifier une erreur. On pourra s'en servir pour trouver notre information (en se servant par exemple d'un code d'indentification pour une erreur).
> Trouver dans quels fichiers de logs se trouve le code "errlog404" (avec les options -r  pour récursive, -i  pour insensible à la "casse", -l  pour n'avoir que les noms des fichiers)

`grep -r -i -l 'errlog404' /var/log/`

## tail -f ou tailf

tail est une commande qui permet d'afficher les dernières lignes de texte d'un fichier.
L'option -f permet à un fichier d'être surveillé. Au lieu d'afficher les dernières lignes et de quitter, tail affiche les dernières lignes et surveille le fichier. Quand des nouvelles lignes sont ajoutées au fichier par un autre processus, tail met à jour l'affichage. C'est particulièrement utile pour surveiller des fichiers de logs. 

L'option -n permet d'afficher les n dernières lignes
`tail -n 20 'monfichierdelog'`

Bien entendu, on peut combiner plusieurs options:
`tail -f -n 100 'heureusementilyadeslogs'`
ou
`tailf -n 100 'heureusementilyadeslogs'`
(si tailf est installé)

## less

Si on reprend la définition de [wikipedia](https://fr.wikipedia.org/wiki/Less_(Unix)):

> less est une commande Unix permettant de visualiser un fichier texte page par page (sans le modifier). Sa fonction est similaire à la commande more, mais permet en plus de revenir en arrière ou de rechercher une chaîne. Contrairement à vi (qui permet aussi de visualiser des fichiers), **less n'a pas besoin de charger entièrement le fichier en mémoire et s'ouvre donc très rapidement même pour consulter de gros fichiers.**

C'est un sacré avantage pour des fichiers de logs qui peuvent être conséquent (plusieurs Go ou +)  :)

De plus, l'option +F de less est vraiment utile:
`less +F /var/log/messages`

Vous allez pouvoir voir en temps réel le fichier (comme pour tail -f).
Par contre, en faisant un ctrl+c, vous allez pouvoir naviguer dans le fichier. Pour revenir à la vue en temps réel, vous n'avez qu'à refaire maj + f (pour faire un F majuscule).

### Inconvénient par rapport à tail -f:
less ne permet de suivre qu'un fichier en temps réel à la fois, contrairement à tail -f qui permet l'affichage de plusieurs fichiers en même temps et qui spécifie à quel fichier appartient les lignes nouvellement apparues.