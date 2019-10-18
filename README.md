WorkShop Jeu de la vie !
=================

Bonjour , bienvenu sur mon workshop , ensemble nous allons apprendre a crée le jeu de la vie en javascript sans framework.


Mais qu'est ce que c'est ?
-----------------

Le jeu de la vie est un automate cellulaire imaginé par John Horton Conway en 1970 et qui est probablement le plus connu de tous les automates cellulaires. Malgré des règles très simples, le jeu de la vie est Turing-complet.

Le jeu de la vie est un jeu au sens mathématique plutôt que ludique. Bien que n'étant pas décrit par la théorie des jeux, certains le décrivent comme un « jeu à zéro joueur ».

Les régles
-----------------

Le jeu de la vie n’est pas un jeu, puisqu'il ne nécessite aucun joueur. Il s’agit d’un automate cellulaire, un modèle où chaque état conduit mécaniquement à l’état suivant à partir de règles pré-établies.

Le « jeu » se déroule sur une grille à deux dimensions, théoriquement infinie (mais de longueur et de largeur finies et plus ou moins grandes dans la pratique), dont les cases — qu’on appelle des « cellules », par analogie avec les cellules vivantes — peuvent prendre deux états distincts : « vivante » ou « morte ».

À chaque étape, l’évolution d’une cellule est entièrement déterminée par l’état de ses huit voisines de la façon suivante :
Une cellule morte possédant exactement trois voisines vivantes devient vivante (elle naît).
Une cellule vivante possédant deux ou trois voisines vivantes le reste, sinon elle meurt.

Ce que nous allons voir lors de ce workshop
-----------------

Tableau multi dimensionnel               
Manipulation du DOM                           
Boucle et conditions                               
Conception d'un algorithme mathématique                             

Fini le blabla , let's go !
=================

### Commencez par cloner le repo sur votre ordinateur.

A l'intérieur de celui ci , ce trouve un fichier index.html , un fichier style.css et un fichier JS , vide bien evidement :)
Ceux ci seront indispensable pour la suite , le fichier index.html contient tout les elements avec leurs ID définie tandis que le fichier CSS contient un peu de style ( Mon jeu de la vie n'est pas responsive , mon but n'étant pas de travailler mon coté front sur ce projet, rien ne vous empeche de vous amuser a changer tout le style pour avoir un projet personnalisée).

### Regardons la structure du projet.

En ouvrant l'index.html dans votre navigateur , vous devriez tomber sur cette page.



