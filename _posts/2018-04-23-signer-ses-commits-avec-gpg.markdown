---
layout: post
title: Signer ses commits avec GPG
date: '2018-04-23 17:00:00'
tags:
- tuto
- decouverte
- securite
navigation: True
current: post
cover: assets/images/water.jpg
navigation: True
class: post-template
author: schaptal
---

Ajourd'hui, un article sur git et les commits (encore ?!).
Oui, encore. Mais là, c'est pour avoir une jolie, une jolie, ...
Mais une jolie signature voyons.

Imaginez (oui, je sais ce n'est pas facile, surtout si vous lisez cet article de bon matin), vous flanez sur github, vous tombez sur un projet qui vous interesse, vous regardez les commits et sur l'un d'entre eux, vous voyez ça:

![verifiedcommit](/assets/images/2018/04/verifiedcommit.png)

Alors là deux réactions possibles:

![meh](/assets/images/2018/04/meh.jpeg)

ou si vous êtes comme moi
![gloriousImg](/assets/images/2018/04/gloriousImg.jpeg)

Si vous êtes dans la première réaction et bien comment dire, hmm, je ne pense pas que le reste de l'article va vous intérresser (et surtout, vous n'avez pas vraiment lu le titre de l'article non ... allez je suis sympa, voila un lien vers [les joies du code](https://lesjoiesducode.fr), c'est cadeau et ça fait toujours plaisir).
Pour les autres, c'est parti ;)


### Installation de gpg

Tapez
```console
gpg --help
```

Si vous avez l'aide qui s'affiche, cela veut dire que vous avez gpg d'installer, vous pouvez sauter l'étape d'installation.


Sinon
###### Sous mac:
```console
brew install gpg
```

###### Sous fedora:
```console
dnf install gnupg2
```
Pour en savoir plus:
https://doc.fedora-fr.org/wiki/GnuPG_:_Signature_et_Chiffrement

###### Sous ubuntu/Debian:
```console
apt-get install gnupg2
```
Pour en savoir plus:
https://doc.ubuntu-fr.org/gnupg


### Création de la clé GPG

```console
gpg --gen-key
```

Rentrez un nom et une adresse mail
Vous allez devoir rentrer votre passphrase (faites en sorte qu'elle soit un minimum robuste quand même, c'est un peu votre rempart pour votre identité).

Il vous reste à ajouter dans la configuration de git votre clé et le fait que vous voulez pouvoir signer vos commits.

```console
git config --global user.signingKey <COLLER_VOTRE_CLE_ICI>
git config --global commit.gpgsign true
```

Dans la plupart des cas, il suffit de faire

```console
git commit -a -S -m 'commit signé'
```


et tada, ça marche et tout va bien.


### Les difficultés rencontrées

Tout d'abord, je tiens à préciser que je suis sous MacOS et que mes tests ont été effectués dans le but d'avoir un commit signé sur un projet github.

Bon, comment vous dire que ... non, ça ne suffit pas m ... morbleu, voila (oui, j'ose le dire).

Lors de mes premières tentatives, j'ai fait face à:

```console
error: gpg failed to sign the data 
fatal: failed to write commit object
```


La solution que j'ai pu trouver:

Une librairie à installer
```console
brew install pinentry-mac
```

truc un peu spécial, il faut au minimum de redémarrer la console pour que cela fonctionne (moi j'ai carrement redémarrer ma machine, au cas où).
Et cela fonctionne.

Si vous voulez travailler avec github, il ne faut pas oublier d'ajouter votre clé GPG dans la configuration de votre compte Github.
Un lien qui m'a vraiment aidé pour le faire.
https://help.github.com/articles/telling-git-about-your-gpg-key/

> <i class="em em-bulb"></i>Dernière remarque: ce qui est rare est d'autant plus précieux. N'allez pas signer tous vos commits à tort et à travers, cela rendrait votre signature moins pertinente <i class="em em-smile"></i>
« *Signer chaque commit est totalement stupide. Cela veut juste dire que vous l'automatisez, la signature a donc bien moins de valeur* » dans [un message en 2009](http://git.661346.n2.nabble.com/GPG-signing-for-git-commit-td2582986.html#a2583316) de [Linus Torvalds](https://fr.wikipedia.org/wiki/Linus_Torvalds).


##### Bibliographie
Github: https://help.github.com/articles/generating-a-new-gpg-key/ , 
https://help.github.com/articles/signing-commits-with-gpg/
Stackoverflow: https://stackoverflow.com/questions/39494631/gpg-failed-to-sign-the-data-fatal-failed-to-write-commit-object-git-2-10-0
Git: https://git-scm.com/book/fr/v2/Utilitaires-Git-Signer-votre-travail
NextImpact: https://www.nextinpact.com/news/99365-github-affiche-maintenant-signature-gpg-commits-et-etiquettes.htm
Un lien vers le projet github crée pour cet article:
https://github.com/chapseb/postGPG
et pour voir le "fameux" commit signé c'est par [ici](https://github.com/chapseb/postGPG/commits/master).

Pour aller plus loin sur GPG: https://ungeek.fr/gpg-et-le-chiffrement-pour-tous/

