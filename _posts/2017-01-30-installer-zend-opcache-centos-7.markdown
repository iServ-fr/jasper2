---
title: Installer Zend OPcache sur CentOS 7
date: '2017-01-30 11:04:00'
tags:
- php
- sysadmin
- tuto
navigation: True
layout: post
current: post
cover: https://images.unsplash.com/photo-1488590528505-98d2b5aba04b?ixlib=rb-0.3.5&q=80&fm=jpg&crop=entropy&cs=tinysrgb&w=1080&fit=max&ixid=eyJhcHBfaWQiOjExNzczfQ&s=6bfea06674b33a2332da1b315b31e16b
navigation: True
class: post-template
author: vfleurette
---

Zend OPcache accélère l'exécution de code PHP. Comment?
Nous savons que PHP est un langage interprété où les instructions sont écrites dans un script et a besoin d'un processus pour l'analyser/interpréter et l'exécuter. 
Zend OPcache supprime l'etape d'interpretation en compilant le script directement exécuté par la machine cible qui rend l'exécution de votre application PHP plus rapide. 
Cet article montre comment installer et configurer Zend OPcache sur CentOS 7.

Les procédures suivantes sont testées sur ce [serveur](https://www.iserv.fr) exécutant Centos 7.

1. Installez le PHP Zend OPcache:
`yum install php-pecl-zendopcache` 
   
2. Configurer Zend OPcache pour votre application PHP. Modifier opcache.ini:
`vi /etc/php.d/opcache.ini`   
    
... Et changer ce qui suit à:
```ini
opcache.revalidate_freq=0 
opcache.validate_timestamps=0  
opcache.max_accelerated_files=20000  
opcache.memory_consumption=128  
opcache.interned_strings_buffer=16  
opcache.fast_shutdown=1   
```

Commentez la ligne "opcache.validate_timestamps = 0" dans votre environnement de développement.
Pour obtenir les "opcache.max\_accelerated\_files" vous pouvez utiliser ceci: 
`find . -type f -print | grep php | wc -l`       

3. Si vous ne souhaitez pas appliquer Zend OPcache à votre site de développement, vous pouvez ajouter son chemin à opcache-default.blacklist:
`vim /etc/php.d/opcache-default.blacklist`

4.  Redémarrez votre Nginx /Apache:
`systemctl restart nginx / httpd`  

5.  Et si vous utilisez php-fpm :
`systemctl restart php-fpm`
