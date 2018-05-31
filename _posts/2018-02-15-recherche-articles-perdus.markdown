---
title: A la recherche des articles perdus - Ghost
date: '2018-02-15 10:31:00'
tags:
- iserv
- cms
navigation: True
layout: post
current: post
cover: content/images/water.jpg
navigation: True
class: post-template
author: schaptal
---

Bonjour à tous, 
aujourd'hui, on parle de notre site iServ, et notre cms [Ghost](https://ghost.org/fr/), mais avec une approche différente de celle de Vincent dans son article [Bonjour Ghost](https://iserv.fr/bonjour-ghost/).

Pour ceux qui ne connaissent pas Ghost:
> *Ghost est un moteur de blog libre et open source écrit en JavaScript et distribué sous licence MIT. Ghost est conçu pour simplifier le processus de publication en ligne par des blogueurs.* (source [Wikipedia](https://fr.wikipedia.org/wiki/Ghost_(moteur_de_blog)))

Beaucoup de choses ont été écrites sur Ghost. Sur son financement, sa techno, le fait qu'il soit libre et oui, il y aurait beaucoup à dire (et beaucoup a déjà été dit).
Cependant, je vais me concentrer sur l'aspect CMS de Ghost (ce qui est sa fonction première).

Et je vais pour cela je vais m'appuyer sur un cas concret, celui de la ... **récupération des anciens articles Jekyll du site iServ**.

A noter que j'aurais pu utiliser des scripts pour le faire automatiquement comme par exemple, en m'appuyant sur ce repo [github](https://github.com/domchristie/turndown) ou en installant la bibliothèque [to-markdown](https://www.npmjs.com/package/to-markdown).

Je ne l'ai pas fait pour deux raisons:
1. Mon but était d'utiliser ghost sans faire appel à des compétences trop "techniques"
2. Je n'aurais pas relu tous les articles **en détail** et ça aurait été dommage
(En vrai, c'était pour supprimer des typos et corriger des fautes :) ).

Donc, j'ai pu récupérer les anciens articles de Jekyll en HTML via le dépot git de l'ancien site iServ en Jekyll [ici](https://github.com/vincfleurette/iServ) (versionner c'est le bien).
J'ai reconstruit les articles un par un et j'ai utilisé https://domchristie.github.io/turndown/ pour passer du HTML au [Markdown](https://fr.wikipedia.org/wiki/Markdown). Cet outil est une instance du projet github mentionné plus haut.

Mais bon, là n'est pas l'essentiel. Le but est de voir **comment on peut se servir de Ghost sans avoir beaucoup de compétences techniques**.

Après avoir récupéré et reformaté quelques articles, je peux en arriver à la conclusion que Ghost est minimaliste.
**Et c'est bien**. 
L'administration de Ghost est claire, simple d'utilisation.
Contrairement à un wordpress assez lourd et où l'on peut se perdre, Ghost se concentre sur le texte et sur la mise en page des articles. **Point**.
D'ailleurs, lors de la rédaction, le fait de pouvoir avoir la source d'un coté et le résultat de l'autre est d'une grande aide.

![Screen and split](/content/images/2018/02/VueDivise.png)

Le système de tag est suffisant pour structurer son blog (bizarrement j'ai plus l'impression d'avoir à faire à des catégories qu'à des tags mais bon).
De plus, le fait de pouvoir rajouter un petit texte descriptif ainsi qu'une image en entête (comme pour un article) est largement suffisant pour faire d'un tag une page à part entière.

Enfin, pour ceux qui veulent optimiser le SEO (search engine optimisation) de leurs articles, vous pouvez mettre le title ainsi que la meta description pour la page de votre article. L'affichage de la preview du résultat dans les moteurs de recherche est un gros plus.

<img alt="descriptiondifferente" src="/content/images/2018/02/descriptMoteurRecherche-1.png" style="max-width: 40% !important; height: auto;margin-top:0;"/>

Pour conclure, reprenons la deuxième partie de la définition wikipédia de Ghost:
> *Ghost est conçu pour simplifier le processus de publication en ligne par des blogueurs.*

C'est exactement ça.
Pour un rédacteur, Ghost ne necessite pas un niveau technique et la courbe d'apprentissage est très courte (contrairement à un Wordpress).
La seule compétence vraiment utile est la maitrise du [Markdown](https://fr.wikipedia.org/wiki/Markdown). Mais, même si l'on peut trouver de la documentation un peu partout sur le net et notamment sur [GitHub](https://help.github.com/articles/basic-writing-and-formatting-syntax/), Ghost y a également pensé et a mis dans sa barre de tache un petit :<img alt="petiteaide" src="/content/images/2018/02/Capture-d-e-cran-2018-02-15-a--10.21.38.png" style="width: 40px !important; height: auto;margin:0;display:inline;"/>

Cette petite icône vous ouvrira une popup avec un récapitulatif et un lien vers la documentation complète.
Enfin, à noter que si vous voyez une limitation en markdown, Ghost prend aussi en compte le HTML :)

Have Fun 



Image crédité à https://ghost.org (https://ghost.org/about/logos) [Public domain], via Wikimedia Commons