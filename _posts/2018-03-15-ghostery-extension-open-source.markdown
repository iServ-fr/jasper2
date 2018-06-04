---
layout: post
title: Ghostery, l'extension anti-tracking passe à l'open source
date: '2018-03-15 19:45:10'
tags:
- decouverte
- opensource
navigation: True
current: post
cover: assets/images/2018/03/ghostery-1.jpeg
unsplash: false
navigation: True
class: post-template
author: schaptal
---

Ghostery, une extension pour navigateur web qui empêche le tracking de votre navigation sur le web, a ouvert son code source.

De nombreuses pages web font appel à de nombreux éléments externes. La plupart du temps, ils servent à suivre l’utilisateur, permettant de savoir au propriétaire du site d'où ils viennent et où vont les internautes transitant par ses pages.

Ce plugin est disponible pour Firefox, Edge, Chrome, Opera et [Cliqz](https://cliqz.com/fr/) (il s'agit de l'entreprise qui a racheté le plugin il y a un peu plus d'un an, ça serait dommage de ne pas mettre l'extension à l'interieur, pour en savoir plus, c'est par [ici](https://www.lemondeinformatique.fr/actualites/lire-cliqz-rachete-l-extension-anti-tracking-ghostery-67381.html)).


### L'historique

Avant le rachat par Cliqz, Ghostery avait en effet un modèle économique particulier: l’extension collectait des données de navigation, plus particulièrement les données relatives aux outils de tracking rencontrés par l’utilisateur, afin de les vendre par la suite aux éditeurs de site web.

En clair, le but était de recueillir les données des utilisateurs, les anonymiser et les mettre en vente. Couplé à une extension propriétaire, ce modèle économique n’était pas vraiment de nature à inspirer confiance aux utilisateurs.

Un manque de transparence donnait l'impression que Ghostery jouait un double rôle en promettant la confidentialité des utilisateurs tout en vendant des données à des sociétés de publicité en même temps.


### Du passé faisons table en marbre (Karadoc de Vannes)

<blockquote class="twitter-tweet" data-lang="fr"><p lang="en" dir="ltr">We’re excited to announce that we’re now officially <a href="https://twitter.com/hashtag/OpenSource?src=hash&amp;ref_src=twsrc%5Etfw">#OpenSource</a>. This change demonstrates Ghostery’s commitment to transparency and creating the best tools for our users. <a href="https://t.co/g3zDhfcP0Q">https://t.co/g3zDhfcP0Q</a> <a href="https://twitter.com/hashtag/GhostyGoesOpen?src=hash&amp;ref_src=twsrc%5Etfw">#GhostyGoesOpen</a> <a href="https://twitter.com/hashtag/ghostery?src=hash&amp;ref_src=twsrc%5Etfw">#ghostery</a> <a href="https://twitter.com/hashtag/security?src=hash&amp;ref_src=twsrc%5Etfw">#security</a> <a href="https://twitter.com/hashtag/privacy?src=hash&amp;ref_src=twsrc%5Etfw">#privacy</a> <a href="https://twitter.com/hashtag/adblocker?src=hash&amp;ref_src=twsrc%5Etfw">#adblocker</a> <a href="https://twitter.com/hashtag/antitracking?src=hash&amp;ref_src=twsrc%5Etfw">#antitracking</a> <a href="https://twitter.com/hashtag/ai?src=hash&amp;ref_src=twsrc%5Etfw">#ai</a> <a href="https://t.co/G4IvLbgh2E">pic.twitter.com/G4IvLbgh2E</a></p>&mdash; Ghostery (@Ghostery) <a href="https://twitter.com/Ghostery/status/971776824228433921?ref_src=twsrc%5Etfw">8 mars 2018</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

<br>

> Notre objectif est la transparence. Un code source ouvert permet au public de voir comment fonctionne Ghostery et quels types de données sont transmis, une fonctionnalité alignée sur les valeurs incarnées par nos produits eux-mêmes - transparence, perspicacité et contrôle. Au-delà, ce projet apporte une opportunité inestimable à nous et à nos utilisateurs en invitant la communauté numérique à contribuer à notre code, à nous aider à nous améliorer et à nous rejoindre dans nos efforts pour rendre Internet plus propre, plus rapide et plus sûr (extrait du communiqué de Ghostery disponible [ici](https://www.ghostery.com/fr/blog/product-releases/ghostery-goes-open-source/))

Le but de cette ouverture est donc double:
* D'une part, l'objectif est de permettre aux utilisateurs de voir comment fonctionne Ghostery et quels types de données il recueille. Cette transparence est essentielle pour effacer les anciennes controverses qui ont pu exister avec l'ancien propriétaire de Ghostery.
* D'autre part, l'objectif est de donner la possibilité aux utilisateurs/developpeurs de faire des contributions à son code source. Cela permet de renforcer la communauté autour de son produit.

Vous pouvez faire un tour sur le [github de Ghostery](https://github.com/ghostery/ghostery-extension). Il convient de noter que Ghostery a publié le code pour ses extensions de navigateur uniquement et non pour les applications mobiles.


En tous cas, il s'agit là d'un beau projet qui nous permettra d'avoir accès aux sites web plus rapidement et de préserver, en plus de nos données personnelles, nos batteries. 
En effet, moins de trackers, moins de données à charger, moins de conso :)


Et en prime, un exemple d'utilisation de ghostery sur iserv


![ghosterySansRessourcesExterne](/assets/images/2018/03/ghosterySansRessourcesExterne.png)

*Sans contenu externe*


![ghosteryAvecRessourcesExterne](/assets/images/2018/03/ghosteryAvecRessourcesExterne.jpg)

*Avec du contenu externe* :) 
