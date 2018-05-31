---
layout: post
title: WordPress utilise les polices systeme et c'est une bonne chose
date: '2017-11-16 10:24:27'
tags:
- cms
---

WordPress 4.6 a été mis à disposition cette semaine. Cette mise à jour est relativement petite mais apporte tout de même son lot de correctifs avec un bonus. En effet, l’administration de votre Wordpress utilise à présent la [police de caractère principale de votre OS](https://make.wordpress.org/core/2016/07/07/native-fonts-in-4-6/). Cela n'implique pas un gros changement mais vous noterez peut-être une différence malgré tout et c'est visuellement plus confortable. La police utilisée précédemment dans l’administration était Open Sans.

> L’aspect changera sur un ordinateur sous Windows ou sous Linux, puisque la police du système n’est pas la même. Sur les appareils Apple, c’est San Francisco, une nouvelle police conçue par l’entreprise, qui est utilisée. Sur Android, ce sera Roboto, sur Windows Segoe UI, etc.

La police système, une opportunité pour améliorer la vitesse de chargement de votre site.

En effet, l'avantage de ce changement est à chercher du côté de la vitesse d'affichage. En général, pour le développement web, les polices sont systématiquement chargées depuis un serveur tiers et cela affecte plus ou moins (selon le nombre et le type de police) le temps de chargement du site web. Avec cette mise à jour, on gagne quelques millisecondes, la police étant déjà présente sur l’appareil utilisé, cela fait ça de moins à télécharger.

Le bonus, c'est que cette optimisation peut également être utilisée pour votre thème ou tout autre site web. Si vous voulez l’utiliser dans un thème, c’est très simple ! Voici la ligne de CSS à ajouter sur les éléments que vous voulez afficher avec ces polices :

```css
font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen-Sans, Ubuntu, Cantarell, "Helvetica Neue", sans-serif;
```

Mais, car il y a **toujours** un **MAIS**

Si tout le monde commence à n'utiliser que des polices systèmes alors tous  les sites vont commencer à se ressembler. Nous aurons tous l'impression de consulter les mêmes pages.
Ce n'est pas la meilleure solution, et je compte vraiment sur les développeurs pour pousser un nouveau standard.
On pourrait vérifier l’existence d'une police, par exemple "Gill Sans", et l'utiliser depuis le système. 
Si elle n'existe pas, on utilise la police système ou carrément aller chercher la police manquante sur un serveur tiers, la mettre en cache (un cache de plus) et ainsi se constituer un belle galerie de polices prêtes à charger.

article inspiré par : [mestrucspour.wordpress.com](https://mestrucspour.wordpress.com/2016/08/18/wordpress-46-police-systeme/)