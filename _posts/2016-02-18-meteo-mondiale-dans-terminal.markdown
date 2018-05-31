---
layout: post
title: Météo mondiale dans votre terminal \ Tuto pour Linux/Mac
date: '2016-02-18 14:40:00'
tags:
- decouverte
---

## Les prévisions météo s’affichent aussi dans le terminal

Pourquoi s’embarrasser d’une application dédiée, pourquoi même s’embêter à ouvrir un onglet dans un navigateur web pour obtenir la météo ? 
Alors que l’on pourrait avoir les prévisions à trois jours pour n’importe quelle ville, directement dans le terminal !

Vous voulez la meme chose .... Alors voici comment faire :-)

Déjà, avant de commencer, on va regarder si vous avez ce qu'il faut :

*   l'environnement Go ?  (voir ci dessous)
*   utf-8 terminal avec  256 couleurs (de base c'est bon sinon petite recherche google )
*   une clé d'API worldweatheronline.com  (voir ci dessous)
  

Déjà pour commencer, il faut installer le langage GO si vous ne l'avez pas deja fait.

## L'environnement GO

Pour Centos/Fedora 20

`yum install -y go`

Pour Mac OS X
 
\#Créer les répertoires  
`mkdir $HOME/Go`
`mkdir -p $HOME/Go/src/github.com/user`

\#Configurer le PATH  
`export GOPATH=$HOME/Go`
`export GOROOT=/usr/local/opt/go/libexec` 
`export PATH=$PATH:$GOPATH/bin`
`export PATH=$PATH:$GOROOT/bin`

\#Installer Go  
`brew install go`

On va maintenant configurer GO dans le PATH  
 
`export GOPATH=$HOME/go`
`export PATH=$PATH:$GOROOT/bin:$GOPATH/bin`
  
Maintenant on peut installer WEGO

## WEGO

* Pour installer le binaire Wego dans votre $GOPATH

`go get github.com/schachmat/wego`

1.  Exécutez Wego une fois. Vous obtiendrez un message d'erreur, vous demandant d’éditer le fichier de configuration.
2.  Si vous ne possédez pas encore la clé API nécessaire, vous pouvez [vous inscrire ici](https://developer.worldweatheronline.com/auth/register) avec votre compte github.com. Votre compte github.com a besoin d'une adresse e-mail du public, mais vous pouvez en choisir un faux.
3.  Copiez votre clé API dans le fichier _.wegorc_ dans votre dossier $HOME, changer la ville à votre guise, et choisissez si vous voulez utiliser des unités métriques ou impériales. Enregistrez le fichier.
4.  Exécutez **Wego** une fois de plus et vous devriez obtenir les prévisions météo pour les 2 jours actuels et à venir.  
Si vous êtes en visite à Marseille ce week-end, il suffit d'exécuter **Wego 4 Marseille** ou **Wego Marseille 4** (l'ordre des arguments ne fait aucune différence) pour obtenir les prévisions pour aujourd'hui et les 3 prochains jours.

Et voila ce que ça donne :

![météo wego_montpellier_guake](/content/images/2018/02/wego-e1455811038826.png)
