---
layout: post
title: Chrono-post &#58; du, pour gérer le space disk
date: '2018-05-19 18:49:59'
tags:
- tuto
navigation: True
current: post
cover: assets/images/2018/05/linuxls.png
navigation: True
class: post-template
author: schaptal
excerpt: La commande du (disk usage) permet d’afficher la taille d’un répertoire et de tous les sous répertoires qu’il contient, et ce de manière récursive...
---

Bonjour à tous,

Tout d'abord, un mot pour vous expliquer le terme Chrono-post (non, il ne s'agit pas d'une reconversion d'iServ dans le transport de colis, même si ça pourrait être sympa, mais trop d'infrastructure à mettre en place, de choses à prévoir, mais je digresse). Le concept est simple, il s'agit de posts qui seront concis et qui ne traiteront que d'une seule thématique.

Aujourd'hui, nous allons étudier une commande unix qui sert à la gestion d'espace sur votre disque dur (que ce soit sur votre poste ou un serveur).

## La commande _du_

La commande **du** (disk usage) permet d’afficher la taille d’un répertoire et de tous les sous répertoires qu’il contient, et ce de manière récursive.
Pas besoin d'être sur une distribution Linux, voici un petit exemple sous Mac et cela fonctionne très bien ;)

Cette commande peut être très pratique pour la gestion de serveur et la recherche des fichiers et/ou répertoires qui occupent le plus de place, afin de libérer de l'espace disque (surtout quand vous remarquez qu'une de vos partitions sur le serveur est à 100%, non c'est pas du vécu :D ).

<figure class="kg-image-card" markdown="1">![Sous mac aussi](/assets/images/2018/05/Capture-d-e-cran-2018-05-27-a--22.22.08.png)
</figure>

Deux options dont je me sers souvent:

*   -h qui correspond à human readable
*   -s qui permet de ne voir que le total du dossier qui est en argument. A noter que par défaut, il s'agit du dossier courant (taper `du` revient au même que de taper `du .`)

Pour aller plus loin, je vous invite à étudier directement le [man de la commande _du_](http://www.linux-france.org/article/man-fr/man1/du-1.html) sur le net (attention au fond turquoise) ou tout simplement à taper `du` dans votre invite de commande.


Merci d'avoir suivi ce premier chrono-post et à très bientôt pour le prochain qui portera sur la commande **df** !



Image de couverture créditée à <a href="https://en.wikipedia.org/wiki/User:Vidarlo">Vidarlo</a>, <a title="Vidarlo at the English language Wikipedia [GFDL (http://www.gnu.org/copyleft/fdl.html) or CC-BY-SA-3.0 (http://creativecommons.org/licenses/by-sa/3.0/)], via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:Xterm.png">via Wikimedia Commons</a>
