---
title: Tuto Let's Encrypt sur Centos 7 avec Nginx, Https pour tous et gratuit !
date: '2015-12-31 13:04:00'
tags:
- sysadmin
- tuto
- opensource
navigation: True
layout: post
current: post
cover: content/images/water.jpg
navigation: True
class: post-template
author: vfleurette
---

Voici un tuto pour Let's Encrypt qui est actuellement en version bêta publique et vous pouvez obtenir des certificats SSL valides et vérifiés pour vos domaines, gratuitement pour une durée de vie. Je sais que, même si je n'y ai pas cru la première fois, c'est vrai. C'est gratuit et libre.

## Qu'est ce que Let's Encrypt ?

Let's Encrypt est une autorité de certification lancée le 3 décembre 2015 (Bêta Version Publique). Cette autorité fournit des certificats gratuits X.509 pour le protocole cryptographique TLS au moyen d'un processus automatisé destiné à se passer du processus complexe actuel impliquant la création manuelle, la validation, la signature, l'installation et le renouvellement des certificats pour la sécurisation des sites internet.

**Dans cet article, je vais vous montrer comment mettre en place un certificat SSL à partir de Let's Encrypt pour votre domaine.** **Les instructions mentionnées dans ce post sont pour Centos 7.**  

> Let's Encrypt est encore en version bêta. Ne pas essayer ceci sur un serveur de production. Il pourrait casser quelque chose (il n'a rien cassé dans mon serveur). Donc, essayez ceci sur un serveur de test avec un environnement similaire à votre production et une fois que vous avez fait en sorte que tout fonctionne comme prévu, vous pouvez l'appliquer.

### Comment faire pour installer et configuration Let's Encrypt sur CentOS 7


\# Install git  
 `yum install git`

\# Install EPEL repo if not present  
 `yum install epel-release`

\# Installer les dépendances  
 `yum install gcc libffi-devel python-devel openssl-devel`

\# Now let us clone the github repository of Let's encrypt  
 `cd /root/`
 `git clone https://github.com/letsencrypt/letsencrypt`


Vous pouvez récupérer la dernière version du dépôt officiel sur votre serveur. Les fichiers se trouvent dans "/root/letsencrypt".

Il faut arrêter nginx avant de faire la manipulation mais au pire le script vous le signalera !

`systemctl stop nginx`

 \# cd to the letsencrypt directory  
 `cd letsencrypt`
 `./letsencrypt-auto`

  
Cela va prendre quelques minutes. Le script va installer tous les modules nécessaires.

Au moment de l'écriture, le programme d'installation automatique letsencrypt ne fait pas encore automatiquement le café/job sur CentOS 7. Vous obtiendrez probablement l'alerte suivante si l'installateur n'a pas pu configurer tout automatiquement. Si tout à fonctionné normalement, le client letsencrypt prendra soin du reste. Vous ne devez pas faire les étapes ci-dessous manuellement. Ce qui suit est pour la configuration manuelle.

> No installers are available on your OS yet; try running "letsencrypt-auto certonly" to get a cert you can install manually 
  
Ceci est 100% normal, et nous pouvons récupérer le certificat manuellement et il fonctionne très bien.

 `./letsencrypt-auto certonly`
  
Il vous demander le ou les nom(s) de domaine pour générer le certificat SSL. Donnez votre nom de domaine. Dans mon cas, j'ai entré "www.iserv.fr iserv.fr" comme noms de domaine. Après cela, vous obtiendrez un message comme ci-dessous :  

> Congratulations! Your certificate and chain have been saved at
> /etc/letsencrypt/live/<your-domain>/fullchain.pem. Your cert will
> expire on 2016-03-30. To obtain a new version of the certificate in
> the future, simply run Let's Encrypt again.
 
C'est tout. Vous avez récupéré le certificat SSL requis et la clé pour votre domaine. Tout ce que nous avons à faire est de tout mettre en place dans nginx.

Et maintenant on restart nginx

`systemctl start nginx`
 
Les répertoires _/etc/letsencrypt/archive_ et _/etc/letsencrypt/keys_ contiennent tous les certificats, y compris les précédents. Et "/etc/letsencrypt/live/" contient des liens symboliques vers les derniers certificats.

## Configuration des certificats SSL avec Nginx

Voici la méthode pour rediriger de manière permanente (en 301) tout le trafic arrivant sur le HTTP vers du HTTPS pour apporter confort, sécurité et volupté à vos visiteurs.

Ouvrez votre nginx.conf (qui se trouve surement dans un répertoire comme /etc/nginx/)

`nano nginx.conf`

Et faites en sorte d'y placer la ligne de reécriture "return 301 https://$server\_name$request\_uri;", dans la section réservée à la config HTTP. Les autres sections sont dédiées au HTTPS et à la config SSL.

```ini
 \# le serveur http sur le port 80  
 server {  
 listen 1.2.3.4:80 default;  
 server_name example.com www.example.com;  
 
 \# Redirige le HTTP vers le HTTPS ##  
 return 301 https://$server\_name$request\_uri;  
 }

\## Le serveur https sur le port 443. N'oubliez pas vote config SSL###  
 server {  
 access\_log logs/example.com/ssl\_access.log main;  
 error\_log logs/example.com/ssl\_error.log;  
 index index.html;  
 root /usr/local/nginx/html;

\## Début de la config SSL ##  
 listen 443 ssl;  
 server_name example.com www.example.com;  
 fastcgi_param HTTPS on;

\### config SSL - A vous de jouer ###  
 ssl_certificate /etc/letsencrypt/live/www.example.com/fullchain.pem;  
 ssl\_certificate\_key /etc/letsencrypt/live/www.example.com/privatekey.pem;  
 ssl_protocols SSLv3 TLSv1 TLSv1.1 TLSv1.2;  
 ssl_ciphers RC4:HIGH:!aNULL:!MD5;  
 ssl\_prefer\_server_ciphers on;  
 keepalive_timeout 70;  
 ssl\_session\_cache shared:SSL:10m;  
 ssl\_session\_timeout 10m;

\## PROXY  
 location / {  
 add_header Front-End-Https on;  
 add_header Cache-Control "public, must-revalidate";  
 add_header Strict-Transport-Security "max-age=2592000; includeSubdomains";  
 proxy_pass http://exampleproxy;  
 proxy\_next\_upstream error timeout invalid\_header http\_500 http\_502 http\_503;  
 proxy\_set\_header Host $host;  
 proxy\_set\_header X-Real-IP $remote_addr;  
 proxy\_set\_header X-Forwarded-For $proxy\_add\_x\_forwarded\_for;  
 }  
 }
```
  
Et voilà... Le tour est joué.  
Sauvegardez le fichier et relancez nginx

`nginx -s reload`
 
Pour vérifier que tout fonctionne correctement, allez faire un tour sur la version HTTP de votre site. Si vous êtes rebasculé automatiquement sur la version en HTTPS c'est que tout ce petit monde fonctionne bien.