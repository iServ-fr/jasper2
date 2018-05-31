---
title: Twitter en ligne de commande sous Linux
date: '2016-05-25 11:13:00'
tags:
- sysadmin
- decouverte
navigation: True
layout: post
current: post
cover: assets/images/water.jpg
navigation: True
class: post-template
author: vfleurette
---

Avec cet article, je vais vous montrer comment accéder à Twitter en ligne de commande. Il ne manque pas de clients Twitter disponibles, différents en termes de fonctionnalités etc. Si vous êtes un de ces fous de ligne de commande, il y en a un un pour vous aussi.

Un outil simple, qu'on appelle via la commande "t", est un client Twitter en ligne de commande écrit en Ruby. En dépit de son interface utilisateur dépouillé, Twitter CLI dispose de fonctionnalités très puissantes telles que la recherche plus profonde dans la timeline, etc. En plus de cela, vous pouvez capter sa sortie formatée vers toutes sortes d'autres outils CLI, de sorte que ses cas d'utilisation possibles sont pratiquement illimitées.

Dans ce tutoriel, je vais montrer comment accéder à Twitter à partir de la ligne de commande en utilisant Twitter CLI. L'installation sera accompagnées d'exemples d'utilisation de base.

### **Installer Twitter en ligne de commande sur Linux**

  
Pour installer Twitter CLI sur Debian, Ubuntu ou Linux Mint:

`sudo apt-get install ruby-dev`
`sudo gem install t`

  
Pour installer Twitter CLI sur CentOS, Fedora ou RHEL:

`sudo yum install ruby-devel`
`sudo gem install t`

### **Configurer votre compte Twitter en ligne de commande**

  
La première étape consiste à créer une application Twitter. Rien de monstrueux, rassurez-vous. Il s'agit d'un simple formulaire à remplir.

Allez sur https://dev.twitter.com/apps/new (connectez vous à Twitter si nécessaire). Vous verrez un formulaire où vous pouvez remplir des informations sur votre application. Il suffit de remplir trois champs: nom, description, et le site Web. Le nom de votre application doit être unique pour tous les utilisateurs de Twitter, et ne peut pas contenir le mot "twitter".

Le site peut être n'importe quoi (par exemple, iserv.fr :-p ).

Vous pouvez laisser vide le callbackURL. Cliquez sur la case à cocher pour accepter les conditions générales d'utilisation (que vous connaissez par coeur n'est-ce pas ;-p ) au bas de la page, et cliquez sur le bouton "Créer votre application Twitter".

Une fois que votre application est créée avec succès, vous verrez une page où vous pouvez gérer vos paramètres de l'application, comme illustré ci-dessous. Allez à l'onglet "Paramètres". Sous "Type de demande", changez "Access" pour "lire, écrire et messages directs", et enregistrer les changements.

Recharger la page pour vous assurer que votre modification a été correctement enregistrée.

La prochaine étape est d'autoriser votre application à accéder à votre compte Twitter. Pour cela, exécutez la commande suivante:

`t authorize`
  
Vous serez invité à appuyer sur _\[Entrée\]_. Si vous le faites, il fera apparaître une fenêtre de navigateur Web qui vous dirigera vers https://dev.twitter.com/apps (connectez vous à Twitter si nécessaire), où vous pourrez voir l'application que vous avez créé plus tôt.

Cliquez sur votre application. Ensuite, allez à l'onglet "Détails" dans la page de l'application. Sous "Paramètres OAuth", vous trouverez la consumer key  et la clef secrète.

Entrez la clé secrète dans le même terminal où vous exécutez **t**.

Vous serez alors invité à appuyer sur _\[Entrée\]_ pour aller à la page Twitter de l'autorisation de l'application. Presser _\[Entrée\]_ fera apparaître une autre fenêtre de navigateur.

Autorisez votre application en entrant votre login/mot de passe cliquez sur le bouton "Autoriser l'application".

A la fin de l'autorisation de l'application, vous obtiendrez un code PIN. Entrez ce numéro de code PIN dans le terminal qui vous y invite.

Vous devriez voir un message "Authorization successful", vous êtes prêt à utiliser Twitter CLI.

Les informations d'accès au compte sera stocké dans ~ / .trc comme un texte brut. Donc, assurez-vous que ce fichier soit lisible à vous seulement, parce que celui qui a une copie de ce fichier peut accéder à votre compte Twitter.

### Accédez à votre compte Twitter en ligne de commande

  
Pour vérifier que votre compte Twitter est accessible à partir de la CLI, exécutez la commande ci-dessous :

`t account`

  
Pour commencer à consulter votre timeline Twitter en temps réel:

`t stream timeline`

![timeline twitter](/content/images/2018/02/11378568535_4ea0bf8785_o.png)
Pour plus d'exemples d'utilisation complexes, reportez-vous à la [documentation officielle](https://github.com/sferik/t/blob/master/README.md).