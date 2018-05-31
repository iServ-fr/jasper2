---
title: 'PHP7 : Comment l''installer sur Centos7 et nginx'
date: '2016-05-05 15:45:00'
tags:
- php
- sysadmin
navigation: True
layout: post
current: post
cover: content/images/water.jpg
navigation: True
class: post-template
author: vfleurette
---

Bonjour à tous, le tutoriel de cette semaine portera sur l'installation de **PHP7** sur **CentOS7**  avec **php-fpm**.
Avoir Nginx d'installé est une condition préalable à celui-ci, donc si vous ne l'avez pas fait, ne vous inquiétez pas, il est encore le temps, via ce tutoriel [http2](https://www.iserv.fr/ready-for-http2/).
On ne va pas seulement installer PHP, cependant pour bien faire les choses, il faut d'abord installer PHP-FPM, pour que PHP puisse fonctionner comme un processus distinct plutôt que de l'intégrer dans le processus de serveur Web. Cela a été longptemps la meilleure pratique, mais il est un peu plus difficile à mettre en place que l'ancienne.

Deuxièmement, CentOS supporte de base une version non prise en charge et obsolète de PHP. PHP 5.4 est la version qui vient avec CentOS 7 (ou plutôt avec le référentiel EPEL) et que la version n'est plus maintenue. Par conséquent nous allons installer PHP7 à partir d'un référentiel différent. Cela permettra non seulement vous donner toutes les dernières fonctionnalités, mais aussi une version qui recevra encore des correctifs et des évolutions.

**Alors, commençons!**

### Préparation de votre environnement
  
Tout d'abord, nous allons commencer par vous assurer que votre système est à jour. Cela permettra non seulement de mettre à jour tous les paquets qui peuvent avoir une mise à jour en cours, mais aussi de mettre à jour les caches du référentiel :

`sudo yum update`
 
Quand on vous demande de continuer, tapez 'y' pour assurer que tout est mis à jour correctement.
Maintenant, afin d'obtenir toute sorte de version décente de PHP (en d'autres termes: celles qui continuent de recevoir des mises à jour de sécurité), nous avons besoin d'ajouter un dépôt tiers qui a des paquets mis à jour. Il y a un très bon dev français appelé Remi qui maintient son dépôt PHP pour un certain nombre de versions. Elles sont libres et très bien documentées. Vous pouvez en savoir plus sur ces dépôts sur [son site](http://blog.famillecollet.com/).  
Pour ajouter son référentiel de PHP, exécutez la commande suivante:

`sudo yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm`
  
Cela récupère les paquets et ajoute le nouveau référentiel YUM. Il est ajouté et désactivé par defaut, nous allons donc l'activer manuellement. 
Ouvrez le fichier référentiel:

`sudo vim /etc/yum.repos.d/remi.repo`

Et localiser ces deux blocs de texte:

```ini 
[remi]
name=Remi's RPM repository for Enterprise Linux $releasever - $basearch  
#baseurl=http://rpms.remirepo.net/enterprise/$releasever/remi/$basearch/  
mirrorlist=http://rpms.remirepo.net/enterprise/$releasever/remi/mirror  
enabled=1  
gpgcheck=1  
gpgkey=http://rpms.remirepo.net/RPM-GPG-KEY-remi
[...]

[remi-php70]  
name=Remi's PHP 70 RPM repository for Enterprise Linux $releasever - $basearch  
#baseurl=http://rpms.remirepo.net/enterprise/$releasever/php70/$basearch/  
mirrorlist=http://rpms.remirepo.net/enterprise/$releasever/php70/mirror  
# WARNING: Only available for RHEL/CentOS >= 6  
enabled=0  
gpgcheck=1  
gpgkey=http://rpms.remirepo.net/RPM-GPG-KEY-remi  
```
  
J'ai coupé le bloc 'remi-php56' car nous voulons seulement PHP7. Maintenant, afin de permettre à ce référentiel, vous devez changer 'enabled = 0' en 'enabled = 1'. Cela signifie que, après le changement des blocs cela ressemblent à ceci:

```ini
[remi]  
name=Remi's RPM repository for Enterprise Linux $releasever - $basearch  
#baseurl=http://rpms.remirepo.net/enterprise/$releasever/remi/$basearch/  
mirrorlist=http://rpms.remirepo.net/enterprise/$releasever/remi/mirror  
enabled=1  
gpgcheck=1  
gpgkey=http://rpms.remirepo.net/RPM-GPG-KEY-remi

[...]

[remi-php70]  
name=Remi's PHP 70 RPM repository for Enterprise Linux $releasever - $basearch  
#baseurl=http://rpms.remirepo.net/enterprise/$releasever/php70/$basearch/  
mirrorlist=http://rpms.remirepo.net/enterprise/$releasever/php70/mirror  
# WARNING: Only available for RHEL/CentOS >= 6  
enabled=1  
gpgcheck=1  
gpgkey=http://rpms.remirepo.net/RPM-GPG-KEY-remi  
```

Enregistrez le fichier. Vous êtes maintenant prêt à installer PHP-FPM!

### Installation
  
Pour installer PHP-FPM (et non le package PHP qui tape dans Apache comme une dépendance), exécutez la commande suivante:

`sudo yum install php-fpm`

  
Il vous demande encore une fois si vous voulez continuer. Plusieurs autres paquets ont été sélectionnés ainsi que les dépendances. Tapez 'y' à nouveau pour démarrer l'installation.  
Une fois l'installation terminée, PHP-FPM aura été installé mais pas encore en cours d'exécution. Pour le démarer, tapez:

`sudo systemctl start php-fpm`

  
Pour assurer qu'il démarre automatiquement avec le serveur, exécutez la commande suivante:

`sudo systemctl enable php-fpm`

  
Maintenant, nous devons nous assurer que NGINX sait transmetre  les requetes PHP  provenant de PHP-FPM. Pour que cela fonctionne, nous devons ajouter un bloc de configuration à l'hôte par défaut. Pour des raisons indépendantes de ma compréhension cela a été mis en place un peu «différent» sur CentOS, donc si vous êtes à la recherche de logique arrêter d'essayer. Dans tous les cas, lancez un nouveau fichier:

`sudo vim /etc/nginx/default.d/php-fpm.conf`

  
Et ajouter le contenu suivant à celui ci:

```ini 
\# pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000  
 \#  
 location ~ \\.php$ {  
 root /usr/share/nginx/html;  
 fastcgi_pass 127.0.0.1:9000;  
 fastcgi_index index.php;  
 fastcgi\_param SCRIPT\_FILENAME $document\_root$fastcgi\_script_name;  
 include fastcgi_params;  
 }
```
  
Ce bloc dit NGINX de transmettre toute demande venant d'un fichier se terminant par .php à 127.0.0.1 port 9000, qui est l'endroit où PHP-FPM fonctionne. NGINX fait cela en utilisant FastCGI. Le bloc de configuration comprend la configuration par défaut, nous ne toucherons rien d'autre pour l'instant.  
Enregistrez le fichier et redémarrez NGINX:

`sudo systemctl restart nginx`

  
Vous êtes maintenant prêt à tester PHP. Nous allons le faire en affichant phpinfo sur votre serveur. **Rappelez-vous de supprimer le fichier de test après le tutoriel car il affiche des informations sensibles sur votre environnement!**  
Ouvrez un nouveau fichier:

`sudo vim /usr/share/nginx/html/info.php`

Et d'ajouter le contenu suivant à ce nouveau fichier:
  
Enregistrez le fichier.  
Si vous allez maintenant à votre localhost  ou votre IP plus "/info.php" (exemple: http://localhost/info.php) vous devriez voir une page agréable et brillante (ou bien, pourpre et laid) avec les informations sur PHP et votre serveur!  
**Si cet article vous a plus, n’hésitez pas à le partager sur votre propre mur pour qu’il soit lu par le plus grand nombre ! Merci d’avoir eu la patience de m’avoir lu jusqu’au bout !**



Image crédité à Colin Viebrock ([1]) [Public domain], <a href="https://commons.wikimedia.org/wiki/File%3APHP_Logo.png">via Wikimedia Commons</a>