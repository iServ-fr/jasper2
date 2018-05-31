---
title: JSON Resume ou comment résumer sa vie en Json
date: '2018-02-25 13:40:33'
tags:
- decouverte
- opensource
navigation: True
current: post
cover: content/images/water.jpg
navigation: True
class: post-template
author: schaptal
---

Vous voulez faire un CV sans avoir à utiliser word ou un autre logiciel de traitement de texte ? Vous voulez pouvoir réutiliser vos informations sur un autre cv sans avoir à tout recommencer ? Alors JSON Resume va vous  intéresser.

Il s'agit d'une initiative pour normer le formatage d'un cv. Le principe, remplir un fichier au format json (d'où le nom JSON Resume) avec vos informations et ce en respectant un [schéma](https://jsonresume.org/schema/) JSON.

Le projet est open source et accessible [ici](https://jsonresume.org/).
La construction du CV se fait en deux temps:
* les données que l'on mettra à l'intérieur
* l'allure qu'aura le CV, ou autrement dit le thème

Cela permet de penser son cv comme certains projets web ou logiciels. Le thème est le frontend de votre projet alors que vos données sont stockées dans votre JSON.

Vous pouvez également construire ce dernier avec vos propres données et choisir votre theme via l'adresse http://registry.jsonresume.org/

Si vous souhaitez être plus autonome, sachez qu'il existe aussi [resume-cli](https://github.com/jsonresume/resume-cli) qui permet de générer le cv en ligne de commande. 

> Warning: pour les prochaines étapes, il vaut mieux maitriser un minimum la ligne de commande et l'édition de fichier json.

Il s'agit d'un packet nodejs qui s'installe comme suit:
`sudo npm install -g resume-cli`

Vous pouvez créer un nouveau cv via la commande:
`resume init`

```ini 
This utility will generate a resume.json file in your current working directory.
Fill out your name and email to get started, or leave the fields blank.
All fields are optional.
Press ^C at any time to quit.
name: Le nom qui sera en entête de votre cv par exemple Richard Hendricks
email: votre mail qui sera inscrit sur votre cv par exemple richard.hendricks@mail.net
  
Your resume.json has been created!
To generate a formatted .html .md .txt or .pdf resume from your resume.json
type: `resume export [someFileName]` including file extension eg: `resume export myresume.html`
You can optionally specify an available theme for html and pdf resumes using the --theme flag.
Example: `resume export myresume.pdf --theme flat`
Or simply type: `resume export` and follow the prompts.
```

Voici le json de base qui est généré (dont j'ai enlevé quelques lignes pour le rendre plus lisible)

![resumeJson](/content/images/2018/02/resumeJson.png)

Il vous suffit de le modifier avec votre éditeur de texte préféré et le tour est joué, le contenu de votre cv est prêt :)

Pour les thèmes, il suffit de les installer en ligne de commande également.
Par exemple, pour le thème stackoverflow:
`npm install jsonresume-theme-stackoverflow`

Pour aller plus loin, vous pouvez reprendre le principe à votre compte.
Vous pouvez garder le json avec vos données et développer votre propre moteur de rendu dans le langage qui vous convient.

De plus, vos expériences vont s'enrichir tout au long de votre carrière, vos hobbies peuvent changer, etc. 
Le fichier json sera donc amené **à évoluer**. Rien ne vous empêche, alors, de le versionner (sous git par exemple). Le format étant toujours le même votre moteur de rendu ne changera pas (ou alors très peu).
Et puis, cela vous permettra de regarder avec nostalgie l'historique de votre fichier dans quelques années...