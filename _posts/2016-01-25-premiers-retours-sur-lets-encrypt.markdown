---
layout: post
title: Premiers retours sur Let's Encrypt
date: '2016-01-25 13:33:00'
tags:
- sysadmin
- tuto
- iserv
- opensource
---

Suite à mon précédent article : [Tuto Let’s Encrypt sur  Centos 7 avec Nginx](https://iserv.fr/tuto-lets-encrypt-sur-centos-7-avec-nginx-https-pour-tous-et-gratuit/) voici mes premiers retours sur Let's Encrypt.

J'ai réalisé cet article à la suite de mes recherches afin d'obtenir la note maximale aux tests [SSLLabs](https://www.ssllabs.com/ssltest/) ou sur [CryptCheck](https://tls.imirhil.fr/).

[Test SSLLabs de IServ.fr](https://www.ssllabs.com/ssltest/analyze.html?d=iserv.fr)

![SSL LABS TEST](/content/images/2018/02/SSLLabsiServ.png)

[Test cryptCheck de IServ.fr](https://tls.imirhil.fr/https/www.iserv.fr)

### Des paramètres par défaut insuffisants
  
Déjà, les paramètres par défaut de Let’s Encrypt ne sont pas corrects. Pourtant, tout le monde sait, en particulier dans le monde de la crypto, qu’un outil de crypto est correct quand sa configuration par défaut est correcte, la plupart des utilisateurs n’allant de toute façon jamais la modifier.

Par exemple, l’outil génère par défaut des clefs RSA de 2048 bits. Cette taille est dorénavant très insuffisante, et [déconseillée officiellement par l’ANSSI](http://www.ssi.gouv.fr/uploads/2015/01/RGS_v-2-0_B1.pdf) au profit de clefs d’au moins 3072 bits. Certes, vos machines ne réclament sûrement pas un niveau de sécurité digne d’Edward Snowden, mais il ne sert à rien de rester dans la zone rouge de la crypto surtout quand l’usage d’une clef de 4096 bits n’est absolument pas une contrainte. Le problème a été [officiellement soulevé](https://github.com/letsencrypt/letsencrypt/issues/489) à Let’s Encrypt, qui a donné [une fin de non-recevoir](https://github.com/letsencrypt/letsencrypt/issues/489#issuecomment-153757615), arguant que 2048 était la configuration par défaut et que si on voulait plus, il fallait juste changer le fichier de configuration.

De ce fait, il faut modifier la commande principale de génération du certificat :

 `./letsencrypt-auto certonly  --rsa-key-size 4096`

### Arrêt de production ou HTTPS only non supporté

Ensuite, Let’s Encrypt, par défaut encore, réclame d’arrêter le serveur nginx pour valider la détention du domaine à signer. Il embarque en effet son propre serveur web pour échanger avec leur back-office (c'est de là que vient la simplicité de let's encrypt), et il ne peut évidemment pas fonctionner si le nôtre est déjà en fonctionnement. C’est juste un comportement contraignant, personne ne souhaite arrêter sa production [tous les 90 jours](https://letsencrypt.org/2015/11/09/why-90-days.html) (c'est encore une beta donc c'est normal aussi mais ça reste pénible) pour renouveler un certificat… Encore une fois, il est possible de contourner le problème via l’utilisation de la méthode _[webroot](https://letsencrypt.readthedocs.org/en/latest/using.html#webroot) au lieu de la méthode par défaut [_standalone_](https://letsencrypt.readthedocs.org/en/latest/using.html#standalone).

### Amélioration Nginx

Pour obtenir la meilleur note (A+) il faut faire quelques ajustements dans la config du bloc SSL de nginx. Il faut limiter la liste des protocoles SSL : **TLSv1.2 TLSv1.1 TLSv1** (on dit adieux aux vieux systèmes d'exploitation qui ne gèrent pas ces protocoles à un niveau de sécurité acceptable), ainsi que les ciphers.

```ini
server {  
 listen 443 ssl spdy; # Ajoutez SPDY ou http2 si vous avez le support d'une des deux fonctionnalités  
 server_name monsite.fr www.monsite.fr;  
 root /var/www/dossier;  
 index index.html index.htm index.php;

add_header Strict-Transport-Security 'max-age=31536000'; # pour le support de HSTS (voir après la config nginx)

ssl_protocols TLSv1.2 TLSv1.1 TLSv1;  
 ssl_certificate /etc/letsencrypt/live/monsite.fr/fullchain.pem;  
 ssl\_certificate\_key /etc/letsencrypt/live/monsite.fr/privkey.pem;  
 ssl\_prefer\_server_ciphers on;  
 ssl_ciphers 'kEECDH+ECDSA+AES128 kEECDH+ECDSA+AES256 kEECDH+AES128 kEECDH+AES256 kEDH+AES128 kEDH+AES256 +SHA !aNULL !eNULL !LOW !MD5 !EXP !DSS !PSK !SRP !kECDH !CAMELLIA !RC4 !SEED';  
 ssl\_session\_cache shared:SSL:10m;  
 ssl\_session\_timeout 10m;  
 keepalive_timeout 70;

\[...\] # Reste de votre configuration (PHP, Directory, etc ...  
 }
```

[HSTS / HTTP Strict Transport Security](https://fr.wikipedia.org/wiki/HTTP_Strict_Transport_Security)

### Le cadenas est orange

![minor_chrome](/content/images/2018/02/minor_chrome.png)


### Premiers retours sur Let's Encrypt
  
Si le cadenas est orange (ou avec un warning) sur votre site, vérifiez les liens de vos images ou scripts, et utilisez le protocole `https://` ou bien utilisez `//` pour tous vos scripts et images.

Merci à [@StosseFlorian](https://twitter.com/StosseFlorian)  pour les indications et à [@blogdedada](https://twitter.com/blogdedada) :

> [@vincfleurette](https://twitter.com/vincfleurette) Tu as un guide pour sécuriser ça ici : [https://t.co/7qh067dpf6](https://t.co/7qh067dpf6) il faut juste en générer des nouveaux et les filer à nginx
> 
>   
> — Harvester (@StosseFlorian) [1 Janvier 2016](https://twitter.com/StosseFlorian/status/682980910392852485)

> [@vincfleurette](https://twitter.com/vincfleurette) Au prochaine renouvellement de clé LE, pense aussi à en demander une de 4096 bits, et à avoir des DHparams de longueur égale
> 
>   
> — Harvester (@StosseFlorian) [1 Janvier 2016](https://twitter.com/StosseFlorian/status/682981163699441665)

  

**Soyez fiers ! Vous avez réussi à installer un certificat Let’s Encrypt sur votre serveur Nginx ! Si vous avez le moindre problème, question, n’hésitez pas à lire la documentation [disponible ici](https://letsencrypt.readthedocs.org/en/latest/) ou bien d’en parler dans les commentaires ?**



*Image crédité à Fabio Lanari (Internet1.jpg by Rock1997 modified.) [<a href="http://www.gnu.org/copyleft/fdl.html">GFDL</a> ou <a href="https://creativecommons.org/licenses/by-sa/4.0-3.0-2.5-2.0-1.0">CC BY-SA 4.0-3.0-2.5-2.0-1.0</a>], <a href="https://commons.wikimedia.org/wiki/File%3AInternet2.jpg">via Wikimedia Commons</a>*