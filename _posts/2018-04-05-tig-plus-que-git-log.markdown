---
layout: post
title: Tig, ta nouvelle interface git en ligne de commande
date: '2018-04-05 20:02:00'
tags:
- decouverte
---

Vous avez votre projet sous git, vous avez peu à peu construit votre projet, au fur et à mesure des commits ou alors vous avez récupéré un projet git existant sur une plateforme, ouverte ou non, comme github, gitlab, bitbucket, etc.
Mais pour voir quoi et surtout comment développer, il faut étudier ce qui a été fait auparavant. Et pour cela, il faut se plonger dans ... l'historique.

Lors de mes premiers projets git, j'utilisais le fameux:

```console
git log
```

Avec comme résultat:
<img src="/content/images/2018/03/gitlog.jpg" style="width:80%;" />

C'est pas mal, c'est utile, mais bon ...
c'est moche et on n'a pas tant d'informations que ça et coté interaction ... meh.

Et là, on m'a fait découvrir [Tig](https://github.com/jonas/tig)

![happiness](/content/images/2018/04/happiness.jpg)

Tig, c'est une interface en mode texte pour git basée sur ncurses (comme [Htop](https://iserv.fr/htop/)).
L'utilisation la plus simple est de simplement taper tig dans votre console, lorsque vous êtes dans un projet git.

![tigFirst](/content/images/2018/03/tigFirst.jpg)

L'affichage par défaut lors du lancement de tig est l'affichage de l'historique. Il s'agit essentiellement d'un journal git, avec un peu d'ASCII-art pour représenter l'historique (vous pouvez masquer l'arborescence avec G). Sans aucun argument, il affiche la branche en cours.

En appuyant sur `Entrée` sur un commit, vous ouvrez ce commit dans une vue diff.

## Comment on l'installe ?

#### Pour Debian et Ubuntu:
```console
apt-get install tig
```

#### Pour CentOS et Fedora:

```console
yum install tig
dnf install tig [On Fedora 22+ releases]
```

#### Pour MacOS
```console
brew install tig
```

#### Pour Windows
Pour utiliser tig sur windows, vous aurez besoin de cygwin, ainsi que les packages nécessaires à la compilation de tig (git, gcc-core, make, libiconv-devel et libncurses-devel).

## Ses différentes vues

#### Tree
De la vue principale, vous pouvez aller dans la vue Tree afin de parcourir l’arborescence du projet en utilisant la touche `t`. De plus, si vous selectionnez un fichier, appuyez sur `entrée`, vous verrez sur la fenêtre de droite le contenu du fichier.

![tigtree](/content/images/2018/03/tigtree.jpg)

#### Status
Cette vue permet de visualiser le statut des branches de développements. Pour l'exemple, j'ai modifié le fichier Changelog et créé le fichier `unfichiercree`.

<img src="/content/images/2018/03/tigstatus.jpg" style="width:60%;" />


#### Blame

Vous voulez savoir qui a foiré votre beau code ou a introduit ce vilain bug ?
Dès que vous êtes positionné sur un fichier, vous pouvez appuyer sur b et le git blame du fichier sélectionné apparaît. Vous pouvez faire aussi `tig blame monfichier` en ligne de commande pour accéder directement au blame du fichier.

![gitblame2](/content/images/2018/03/gitblame2.jpg)

Il suffit ensuite de sélectionner une ligne et appuyez sur Entrée, et il vous montrera le dernier commit qui a touché cette ligne.

<img src="/content/images/2018/04/gitblame.jpg">
<em>Quand je découvre que c'est moi qui ait introduit le bug <i class="em em-smile"></i></em>


#### <i class="em em-bulb"></i> Le saviez-vous ?
* Tig s’utilise un peu comme Vim, (oui, j'aime Vim).
Par exemple pour les recherches, il suffit de taper `/` et de taper son expression. Si plusieurs sont trouvés, il suffit de taper `n` pour aller à la prochaine occurence.
* En utilisant la commande `git log | tig` vous avez un affichage ressemblant furieusement au `git log` classique avec en plus une meilleur colorimétrie et un meilleur défilement avec un gros plus, le détail du commit ou votre est placé
* Vous pouvez exécuter tig des 2 façons suivantes depuis le répertoire d’un projet, soit en l’associant avec une commande Git (par exemple git log | tig ou git blame Changelog), soit directement(celle que l'on a vu dans la plupart de nos exemple).

## Raccourcis clavier:
<br>

###### Changement de vue

| Raccourci | Description                          |
| --------- |:-----------------------------------: |
|     m     | vue standard                         |
|     s     | vue statut comme le git status       |
|     t     | montre la vue arborescente du projet |
|     g     | chercher une expression (Grep)       |
|     l     | montre la vue log                    |
|     d     | montre le diff du commit             |
|     h     | affiche l'aide                       |

###### Fenêtre principale

| Raccourci | Description                          |
| --------- |:-----------------------------------: |
|     D     | Change l'affichage de la date        |
|     A     | Change l'affichage de l'auteur       |
|     X     | voir les identifiants des commits    |
|     C     | Cherry pick un commit                |
|     ,     | Va au commit parent                  |

###### Dans toutes les vues

| Raccourcis | Description                          |
| ---------- |:-----------------------------------: |
| k          | Monte d'une ligne                    |
| j          | Descendre d'une ligne                |
| K          | Commit suivant                       |
| J          | Commit précédent                     |
| q          | Quitte la vue actuelle               |


###### D'autres informations:
* Vous pouvez trouver d'autres raccourcis clavier sur : https://devhints.io/tig
* Où trouver le « man » de Tig ? https://jonas.github.io/tig/doc/tig.1.html
* Où trouver le manuel d’utilisation ? http://jonas.nitro.dk/tig/manual.html



