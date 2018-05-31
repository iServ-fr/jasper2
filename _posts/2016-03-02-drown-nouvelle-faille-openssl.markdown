---
title: DROWN, une nouvelle faille pour OpenSSL
date: '2016-03-02 17:12:00'
tags:
- sysadmin
navigation: True
layout: post
current: post
cover: content/images/water.jpg
navigation: True
class: post-template
author: vfleurette
---

### Résumé

DROWN est le nom qui a été attribué par la communauté à la vulnérabilité CVE-2016-0800 publiée le 01/03/2016.  
Cette vulnérabilité affecte le protocole SSLv2, déployé en Février 1995 et déprécié dès 1996.

La faille DROWN permet à un pirate de récupérer le contenu d'une communication en théorie sécurisée, contenant par exemple un identifiant, un mot de passe, ou une session.

La gravité de cette faille doit néanmoins être remise dans son contexte, et n'a d'impact que sur des configurations anciennes.

### Qui est une cible potentielle ?

Tout système utilisant SSLv2 ou utilisant une clé privée partagée avec un système utilisant SSLv2.  
Ainsi, si vous utilisez le même certificat sur plusieurs serveurs et que l'un d'entre eux accepte encore SSLv2, tous ces serveurs sont vulnérables.

**Les chercheurs ayant découvert la faille ont scanné une grande partie de l'Internet et ont publié leurs résultats sur [le site suivant](https://test.drownattack.com/).**

Pour plus de détail, je vous invite à consulter [la page française mise en place pour l'occasion](https://www.drown.fr/).

> iServ.fr n'est pas vunérable mais j'en ai profité pour mettre à jour ma version d'openSSL, je présente la marche à suivre dans un nouveau tuto qui sera disponible ce soir.

### Petit rappel sur le contexte :

SSL a été inventé pour sécuriser la communication entre un client et un serveur, ou entre votre navigateur et un site Internet. Cette technologie est à la base d'un grand nombre d'échanges dans le web mondial.  
Ainsi, une faille affectant ce protocole peut avoir des effets dévastateurs pour un grand nombre d'internautes, en révélant le contenu de communications supposées sécurisées.

La version 2 de SSL a été la première à être utilisée dans le monde, mais a rapidement fait l'objet de critiques en matière de sécurité informatique, poussant la communauté à travailler sur une nouvelle version nommée SSLv3.  
SSLv2 est ainsi reconnu comme un protocole faible, et se retrouve donc désactivé par défaut dans la plupart des outils du marché.

Cependant, de nombreux serveurs et logiciels utilisent encore SSLv2 et la découverte de cette nouvelle faille devrait donc pousser leurs propriétaires à appliquer les recommandations ci-dessous le plus rapidement possible afin de protéger leurs services et leurs utilisateurs.