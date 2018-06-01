---
title: 'Decentraleyes : vitesse et vie privée'
date: '2016-05-02 16:27:00'
navigation: True
layout: post
current: post
cover: assets/images/2018/02/decentralize-1.png
navigation: True
class: post-template
author: vfleurette
---

## Decentraleyes : vitesse et vie privée une extension pour firefox


Si vous utilisez Firefox et que vous n'avez pas encore installé [decentraleyes](https://addons.mozilla.org/fr/firefox/addon/decentraleyes/), je vous encourage vivement à le faire. Vous pouvez en apprendre beaucoup sur un site lorsque vous surveillez ses appels aux ressources externes: vous pouvez voir les connexions vers des sites tiers, annonces, web analytics scripts et bien plus.

Dans le développement web, une plus ou moins bonne pratique consiste à utiliser les bibliothèques ou les frameworks JavaScript populaires comme jQuery, bootstrap. Les sites peuvent hébergé localement les fichiers de ces derniers, ou utiliser des versions hébergées par des CDN (content delivery network) comme ceux de Google, Microsoft ou Cloudflare.

Ces ressources sont souvent essentielles pour le bon fonctionnement d'un site, et en les bloquant, elles peuvent tout simplement bloquer la bonne exécution du site.

Il y a deux préoccupations que les internautes peuvent avoir en ce qui concerne l'utilisation de ces réseaux de diffusion de contenu: la vie privée et la vitesse.

La vitesse est plus facile à expliquer. Alors qu'il est souvent plus rapide d'utiliser un CDN pour les ressources hébergée localement plutôt que son propre serveur du site lui-même, cela signifie de maintenir une connexion avec le CDN en priorité. Ce site supporte également le protocole http2 ce qui vous permet en utilisant les dernieres versions, de charger les ressources de iserv en parallèle et non les unes à la suite des autres, [pour en savoir plus sur http2](https://iserv.fr/ready-for-http2-with-nginx-on-centos-7/).

Pour la confidentialité, cela vient des multiples appels aux cdn's qui peuvent déposer des cookies sur votre système. Ils peuvent également enregistrer votre activité sur Internet puisque vous vous connectez à eux en utilisant un navigateur web, et obtiennent des informations sur les connexions telles que votre système d'exploitation, le navigateur Web que vous utilisez, votre adresse IP ou votre emplacement dans le monde.

![decentralize](/assets/images/2018/02/decentralize.png)

[Decentraleyes](https://addons.mozilla.org/fr/firefox/addon/decentraleyes/) pour Firefox se préoccupe de ces deux aspects en même temps, au moins pour les CDNs.

Ainsi, au lieu d'aller chercher un jQuery.js chez MaxCDN, un SWFObject chez Cloudflare ou une font chez Google, votre Firefox ira piocher tout ça en local, sans appeler une seule fois les CDN en question. Decentraleyes est une bonne extension qui introduit quelque chose qui n'existe nulle part ailleurs. Même si ce n’est pas 100% étanche, ça limitera quand même un peu vos échanges réseaux avec les principaux CDN du marché.

Source: [ghacks](http://www.ghacks.net/2015/11/23/decentraleyes-for-firefox-loads-cdn-resources-locally/) et [korben](http://korben.info/decentraleyes-bloquer-appels-aux-cdn-casser-sites-web.html)