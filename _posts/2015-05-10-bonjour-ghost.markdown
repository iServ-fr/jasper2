---
title: Bonjour Ghost
date: '2015-05-10 10:13:00'
tags:
- sysadmin
- iserv
- cms
navigation: True
layout: post
current: post
cover: assets/images/2018/02/ghost-logo-4.png
unsplash: false
navigation: True
class: post-template
author: vfleurette
---

Pour motoriser ce site, j’ai décidé d’abandonner Jekyll, qui pourtant, m’a rendu un grand service. Jekyll, c’est un véritable bonheur à utiliser, je l’ai découvert grâce à la *[sheevaboite](https://www.sheevaboite.fr/)*, un très bon site sur l’auto hebergement.

Je me tourne donc vers Ghost dans sa version la plus simple. J’ai suivi ce **[tuto](http://soyuka.me/installer-ghost-sur-un-vps-pm2-apache/)**, mais l’objectif final est d’utiliser [Docker](https://www.docker.com/). J’ai eu la chance dans le cadre de mon travail d’assister à l'[OVH World tour 2015](http://www.ovh.com/fr/events/RS030415-ovh-world-tour-Montpellier) à Montpellier et j’ai découvert Docker, runabove, Object Storage (j’y reviendrai dans un prochain article).

L’une des sessions techniques portait sur Docker. Le conférencier [@gierschv](https://twitter.com/gierschv) a fait une démonstration de ghost + mariadb chacun dans son container. Ce type de solution m’intéresse afin de pouvoir proposer des solutions industrielles de déploiements d’applications Web.


Image crédité à https://ghost.org (https://ghost.org/about/logos) [Public domain], <a href="https://commons.wikimedia.org/wiki/File%3AGhost-Logo.svg">via Wikimedia Commons</a>