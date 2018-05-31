---
layout: post
title: Désactiver Bonjour sur Cyberduck
date: '2017-06-02 07:59:00'
tags:
- tuto
---

Si vous utilisez [Cyberduck](https://cyberduck.io/) sur le réseau local de votre société, IUT ou Université, vous ne savez peut-être pas que [Cyberduck](https://cyberduck.io/) ouvre le protocole de communication Bonjour.

> Bonjour, anciennement appelé Rendez-vous, est un logiciel créé par Apple qui met en œuvre la technologie Zeroconf de l’IETF. Il est utilisé dans Mac OS X à partir de la version 10.2, mais également dans iTunes et dans Windows.
> Le code source a été rendu disponible sous licence libre Apache 2.01 et une version binaire est disponible pour Windows.
> Zeroconf est un système de mise en réseau local automatique, il est aussi utilisé pour trouver les imprimantes et dossiers partagés, mais aussi des serveurs web et FTP, ainsi que des utilisateurs de iTunes, iPhoto et iChat.
> Rendez-vous a été renommé Bonjour en 2004 car Tibco Software avait déjà publié sur le marché un produit nommé Rendez-vous.
> Bonjour utilise le port 5353 en UDP.
> Wikipedia

Du coup, il peut-être très facile pour un curieux d'observer tous les utilisateurs utilisant ce protocole et principalement des Mac-Users. Un bon moyen aussi d'entamer une discussion avec la voisine d'à coté. Depuis que j'utilise Cyberduck, mais pour l'utilisation que j'en ai et pour respecter votre vie privée, je pense qu'il est préférable de le désactiver. Il y a une commande Terminal simple, comme tant d'autres choses le sont dans le monde Mac. Pour désactiver Bonjour, lancez Terminal et exécuter cette commande :

    defaults write ch.sudo.cyberduck rendezvous.enable false

Si vous voulez réactiver Bonjour, faites la même commande, mais changer **false** à **true**.