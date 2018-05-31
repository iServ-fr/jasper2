---
layout: post
title: 'Introduction à Docker: première approche'
date: '2018-03-22 11:00:00'
tags:
- sysadmin
- decouverte
---

Bonjour à tous, aujourd'hui nous parlons d'une technologie en vogue, Docker. Que vous soyez développeurs, administrateurs systèmes ou DSI, vous avez certainement entendu parler de Docker. C'est une technologie qui nous interesse et que nous allons étudier un plus intensemment ces prochaines semaines. C'est pour ça que nous en parlons aujourd'hui :)

Docker est une technologie de container qui s’appuie sur 2 grands principes :
* Une image correspond à un instantanée d’une machine (unix/linux) qui a été définie dans un fichier Dockerfile.
* Le container est une instance d’une image qui fait tourner un process de manière complètement isolée des autres au sein d’une machine (physique ou virtuelle) équipée du daemon docker.

Il s'agit de la solution de containerisation la plus utilisée au monde. La première version est sortie en mars 2013 et a rapidement suscité beaucoup d’intérêt. Avec de nombreuses contributions sur Github, la version 1.0 est sortie en 2014 et a provoqué quelques bouleversements. Même si on ne considère que seul 10% des entreprises utilisent Docker en production, 30% sont actuellement en test avec l’outil (chiffres qui ont du évoluer, ces derniers datant de mi-20017)

Les services Cloud comme AWS ou Azure acceptent de plus en plus les conteneurs Docker. Ainsi, plus besoin de lancer un nouveau service EC2 pour déployer votre application ce qui permet de gagner en ressources et en disponibilité.

#### DÉMARRER AVEC DOCKER
Si vous souhaitez vous aussi vous lancer sur Docker, rendez-vous sur le site officiel où un tutoriel vous expliquera les principes de l’outil et ses avantages : https://docs.docker.com/get-started/

Après, comme dis au début de cet article, nous n'avons pas encore une grosse expertise là dessus.
Nous écrirons surement un nouvel article dans quelques semaines oû nous résumerons les cas que nous avons pu rencontrer et les enseignements que nous avons pu en tirer. 
Donc pour résumer, même si Docker est la technologie en vogue et que tout le monde s'arrache, si on trouve que c'est nul, on ne se gènera pas pour le dire :)


Liens utiles:
https://www.journaldunet.com/solutions/cloud-computing/1146290-docker-la-technologie-qui-revolutionne-le-cloud/
https://pro-domo.ddns.net/blog/docker-youre-doing-it-wrong.html
https://code.tutsplus.com/fr/tutorials/docker-from-the-ground-up-understanding-images--cms-28165

