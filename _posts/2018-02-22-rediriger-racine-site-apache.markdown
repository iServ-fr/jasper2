---
title: Rediriger uniquement la racine de son site sous Apache
date: '2018-02-22 16:17:23'
tags:
- sysadmin
- apache
navigation: True
layout: post
current: post
cover: assets/images/2018/02/http.jpg
unsplash: false
navigation: True
class: post-template
author: schaptal
---

Il est parfois necessaire de faire des redirections pour ses sites web. Il y  quelques cas communs comme le changement d'url d'une page d'un de vos sites ou un changement de nom de domaine. Mais comment rediriger seulement la racine de son site web ?

Le répertoire root ne contient pas forcément des ressources de première importance pour l'utilisateur. Il est également possible de vouloir que la racine de son site renvoie sur une page spécifique d'un autre site (cette page servirait à la fois de page d'accueil et de tutoriel qui aurait été faite par un autre organisme).

Si la cible est sur le même serveur vous pouvez faire comme suit:
```apache
RewriteEngine on
RewriteRule   "^/$"  "/monnouvelaccueil/"
```

Par contre, si vous voulez rediriger vers une url particulière:
```apache
RedirectMatch "^/$" "http://example.com/letutoquitexpliquetout"
```

A noter que la règle ne s'applique qu'à la racine grâce à l'expression régulière "^/$" (qui correspond au chemin "/").


Sources: 
https://httpd.apache.org/docs/2.4/fr/mod/mod_alias.html
https://www.devside.net/wamp-server/how-to-redirect-root-url-to-another-sub-directory-or-url