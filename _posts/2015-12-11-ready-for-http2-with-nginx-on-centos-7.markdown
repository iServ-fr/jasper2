---
title: Ready for HTTP2 with Nginx on Centos 7
date: '2015-12-11 16:20:00'
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

## Qu’est-ce que HTTP2 ?

HTTP2 est le nouveau protocole du web qui fait suite à la dernière mise à jour qui date de 1999 !

**Les 2 axes majeurs de HTTP/2 sont la rapidité et la sécurité de la navigation.**

Les avancées de HTTP/2 :
*   **la compression des headers des requêtes et des réponses**. Cette optimisation permet de réduire la bande passante lorsque les headers (tels que des cookies) sont similaires.
*   **le multiplexage des requêtes au serveur**. Le multiplexage consiste à faire passer de multiples informations via un seul tuyau de transmission.
*   de l’**optimisation de la négociation SSL**.

Ainsi, on économise les multiples connexions entre le client et le serveur. Les requêtes, quant à elles, sont effectuées simultanément par le navigateur. Les requêtes ne se suivent donc plus les unes derrière les autres et les plus prioritaires (telles que les CSS) ne sont plus bloquées par les moins prioritaires (telles que les images).

*   **le push des ressources du serveur au navigateur.** Désormais, le serveur pourra envoyer l’ensemble des ressources référencées dans une même page (CSS, JS…), avant même que le navigateur n’ait analysé celle-ci.
  

## Comment démarrer la transition vers HTTP/2 ?

HTTP/2 va être déployé sur la majorité des navigateurs. A l’heure actuelle HTTP/2 est déjà supporté par les navigateurs à hauteur de 70% de part de marchés.

**Ainsi il est possible de profiter dès aujourd’hui des optimisations HTTP/2  pour que vos pages HTTP/HTTPS se chargent plus rapidement.**

Pour cela, aucune modification sur le code de la page n’est nécessaire.

### Redirection SSL / TLS

Si votre web-app est déjà chiffré avec SSL / TLS , Ce serait  serait un bon moment pour franchir le pas ([iServ est deja en https](https://www.iserv.fr/2015/01/11/iserv-en-ssl/)). Chiffrer votre application vous protège contre l'espionnage et les attaques man-in-the-middle . Certains moteurs de recherche , même récompensent les sites cryptés avec une note amélioration dans les résultats de recherche. Le bloc Nginx de configuration suivant redirige toutes les requêtes HTTP vers sa variante HTTPS

```ini
     server {  
         listen 80;  
         location / {  
             return 301 https://$host$request_uri;  
         }  
     }  
```

### Activation HTTP / 2

Pour activer le protocole HTTP/2 support, il suffit d'ajouter le paramètre HTTP2 à toutes les déclarations "Listen 443" .

Inclure aussi les paramètres SSL, nécessaires car les navigateurs ne supportent pas HTTP/2 sans chiffrement.
  
```ini
     server {  
         listen 443 ssl http2 default_server;  
         ssl_certificate    server.crt;  
         ssl\_certificate\_key server.key;  
         ...  
     }  
```

## Et vous, êtes-vous prêt pour HTTP/2 ?
  
Petite particularité, sous Centos le paquet **nginx** dans les dépôts était en version **1.6.3** ce qui provoque des erreurs après un passage de "_nginx -t_" donc, avant de recharger nginx et risquer de planter le serveur web, j'ai cherché une solution pour obtenir une version nativement compatible avec http/2 et *stable*.

Pour configurer le nouveau dépôt, il faut se créer un fichier /etc/yum.repos.d/nginx.repo avec votre éditeur code préféré (VIM) et ajouter les lignes suivantes :

```ini  
name=nginx repo  
baseurl=http://nginx.org/packages/mainline/centos/7/$basearch/  
gpgcheck=0  
enabled=1
```
  

Une fois enregistré, vous lancez "yum update" et vous devriez avoir une mise à jour 1.9.X de nginx.
Il ne vous reste plus qu'à vérifier que votre configuration est OK et redémarrer nginx via "systemctl restart nginx.service".

Vous pouvez à présent tester votre site sur [cette page](https://tools.keycdn.com/http2-test) et contempler que votre site fonctionne bien avec ce nouveau protocole.