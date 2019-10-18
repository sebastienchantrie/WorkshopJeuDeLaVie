WorkShop Jeu de la vie !
=================

Bonjour , bienvenu sur mon workshop , ensemble nous allons apprendre a crée le jeu de la vie en javascript sans framework.


Mais qu'est ce que c'est ?
-----------------

Le jeu de la vie est un automate cellulaire imaginé par John Horton Conway en 1970 et qui est probablement le plus connu de tous les automates cellulaires. Malgré des règles très simples, le jeu de la vie est Turing-complet.

Le jeu de la vie est un jeu au sens mathématique plutôt que ludique. Bien que n'étant pas décrit par la théorie des jeux, certains le décrivent comme un « jeu à zéro joueur ».

Les règles
-----------------

Le jeu de la vie n’est pas un jeu, puisqu'il ne nécessite aucun joueur. Il s’agit d’un automate cellulaire, un modèle où chaque état conduit mécaniquement à l’état suivant à partir de règles pré-établies.

Le « jeu » se déroule sur une grille à deux dimensions, théoriquement infinie (mais de longueur et de largeur finies et plus ou moins grandes dans la pratique), dont les cases — qu’on appelle des « cellules », par analogie avec les cellules vivantes — peuvent prendre deux états distincts : « vivante » ou « morte ».

À chaque étape, l’évolution d’une cellule est entièrement déterminée par l’état de ses huit voisines de la façon suivante :
Une cellule morte possédant exactement trois voisines vivantes devient vivante (elle naît).
Une cellule vivante possédant deux ou trois voisines vivantes le reste, sinon elle meurt.

Ce que nous allons voir lors de ce workshop
-----------------

 - Tableau multi dimensionnel
 - Conception d'un  algorithme mathématique
 - Boucles et conditions
 - Manipulation du DOM
 - Passage de paramètres a des fonctions

                     

Fini le blabla , let's go !
=================

### Commencez par cloner le repo sur votre ordinateur.

A l'intérieur de celui ci , ce trouve un fichier index.html , un fichier style.css et un fichier script.js.
Ceux ci seront indispensable pour la suite , le fichier index.html contient tout les éléments avec leurs ID définie tandis que le fichier style.css contient un peu de style ( Mon jeu de la vie n'est pas responsive , mon but n'étant pas de travailler mon coté front sur ce projet, rien ne vous empêche de vous amuser a changer tout le style pour avoir un projet personnalisée).
Le fichier script.js est quant a lui presque totalement vide , c'est la que nous allons travailler.

### Regardons la structure du projet.

En ouvrant l'index.html dans votre navigateur , vous devriez tomber sur cette page
![Gameoflifeaccueil](https://image.noelshack.com/fichiers/2019/42/4/1571316171-img1.png)

Vous vous rendrez vite compte qu'en appuyant sur le bouton , il ne se passe rien , nous allons donc commencer par crée l'affichage du tableau dans lequelle ce déroulera notre jeu de la vie.

### Un peu de code ?!

Nous allons devoir crée un **tableau Multi-dimensionnel** d'une taille égale a celle proposée sur la page d'accueil , donc 32x32 , 64x64 ou 128x128.
Pour ce faire on va avoir besoin d'une variable ou stocké le resultat des input radio , cette variable nous allons la déclarée en global et sans valeurs pour le moment parce que nous devrons l'utiliser a nouveau plus tard... 

Une variable déclarée en dehors d'une fonction devient **GLOBAL** .
Une variable globale a **une portée globale** : tous les scripts et toutes les fonctions d'une page Web peuvent y accéder.
Par convention nous allons la placer tout en haut du script.
```JS
let  nbtab;
```
```JS
    btnclick.addEventListener("click", () => {
		let  tbl  =  document.createElement("table");
		let  tblBody  =  document.createElement("tbody");
		if (document.getElementById('32').checked) nbtab  =  32;
		else  if (document.getElementById('64').checked) nbtab  =  64;
		else  nbtab  =  128;
		for (let  i  =  0; i  <  nbtab; i++) {
			let  row  =  document.createElement("tr");
			for (let  j  =  0; j  <  nbtab; j++) {
			let  cell  =  document.createElement("td");
			cell.classList.add('false');
			cell.id  =  `cell-${i}-${j}`
			if (nbtab  ===  32) {
			cell.classList.add('mini');
			bodytab.classList.add('col-lg-8');
			bodytab.classList.add('littlemargin');
		}
		else  if (nbtab  ===  64) {
			cell.classList.add('middle');
			bodytab.classList.add('col-lg-6');
			bodytab.classList.add('middlemargin');
		} else {
			cell.classList.add("big");
			bodytab.classList.add('col-lg-8');
			bodytab.classList.add('bigmargin');
		}
		row.appendChild(cell);
		}
		tblBody.appendChild(row);
		let  move  =  document.getElementById('move');
		move.classList.add('move');
		tbl.appendChild(tblBody);
		bodytab.appendChild(tbl);
		tbl.setAttribute("border", "2");
		}
	});
```


Si tout ce passe bien , vous devriez maintenant pouvoir cliquer sur le bouton et voir un tableau de la taille de votre sélection.

L'affichage du tableau c'est bon , mais il ne se passe pas grand chose dans notre jeu , par défaults le tableau est generé avec toute les cellules mortes , c'est donc a vous d'ajouter des cellules vivantes avant de cliquer sur le bouton play , pour ce faire on va rajouter ce bout de code a la suite du		``row.appendChild(cell);.``
```JS
/* Fonction qui rends les cases cliquable */

	cell.addEventListener('click', (e) => {
		if (cell.classList[0] ==  "false") cell.classList.replace("false", "true");
		else  cell.classList.replace("true", "false");
})
```

Certes , il peut maintenant cliquer sur les cases une par une , mais c'est un peu long , on va ajouter une fonction qui permets de rester appuyer sur son clique gauche et pouvoir transformer l'état des cellules en passant dessus , c'est pas très agile de faire ça maintenant mais c'est une toute petite fonctionnalités , alors on va la crée maintenant. Nous allons définir une nouvelle variable globale.
```JS
let  mousedown  =  false;
```
Ensuite nous allons mettre ce bout de code juste en dessous de la fonction que nous venons de crée
```JS
document.addEventListener('mousedown', (e) => {
	bodytab.onmousedown  = () => {
	mousedown  =  true;
	console.log(mousedown);
	}
	cell.onmouseover  = () => {
		if(mousedown) {
			if (cell.classList[0] ==  "false") cell.classList.replace("false", "true");
			else  cell.classList.replace("true", "false");
		}
	}
	bodytab.onmouseup  = () => {
		mousedown  =  false;
	}
});
```
Ok , ca c'est bon !  Il y a aussi un petit bouton règles , on va donc l'activer avec une simple manipulation du DOM , juste histoire de l'avoir fait , c'est super basique.
```JS
btnrules.addEventListener('click', () => {
	rules.style.opacity  =  '1';
	rules.style.zIndex  =  '5';
})
btnback.addEventListener('click' , () => {
	rules.style.opacity  =  '0';
	rules.style.zIndex  =  '-5';
})


```

Bon , ok c'est super , l'utilisateur peut colorier des cases et lire les règles , mais ca fait toujours rien quand on appuie sur play , c'est donc le moment de passer a la logique.

### La partie Algorithme / logique

Ahh , on va enfin pouvoir rentrer dans le vif du sujet !!!! :D

Si on prends le temps de réfléchir , nous avons donc maintenant l'affichage d'un tableau avec un nombre de cases définie , chaque case correspond a un TD et possède un ID

Vu qu'on cherche a faire le jeu de la vie , il va falloir codé la logique du jeu.

On va donc faire une fonction qui crée un autre tableau multi-dimensionnel ( cette fois ci uniquement en JS , ce tableau ne sera jamais visible pour l'utilisateur) et qui stock le même nombre de case que le tableau HTML , la fonction sera appelée plus tard a l'intérieur de la fonction qui contiendra la logique mais nous devons la faire maintenant.

```JS
function  createtab(mylogictab) {
	if (document.getElementById('32').checked) nbtab  =  32;
	else  if (document.getElementById('64').checked) nbtab  =  64;
	else  nbtab  =  128;
	for (let  i  =  0; i  <  nbtab; i++) {
		let  arr  = [];
		for (let  y  =  0; y  <  nbtab ; y++) {
			arr[y] =  false;
		}
		mylogictab[i] =  arr;
	}
	return  mylogictab;
}
```
Ce tableau que nous venons de crée permettra de vérifier l'état des cases et d'y appliquer les règles et les changements d'états.


Maintenant nous allons crée la fonction qui va regarder les cellules autours de la cellules que nous aurons passer en arguments.

La logique est simple , on va crée une fonction pour éviter de répéter le même code
Cette fonction sera appelée avec différents arguments pour se promener dans notre tableau multi-dimensionnel et verifier l'état des cases aux alentours.
On peut y voir la condition ``if  (map[x][y])  return  (1)``
En gros , il va regarder la cellule , si elle est vivante , il renverra 1 , sinon , il renverra 0.
```JS
function  controlCellule(x, y) {
	if (x  <  0) x  =  map.length  -  1;
	else  if (x  >=  map.length) x  =  0;
	if (y  <  0) y  =  map[x].length  -  1;
	else  if (y  >=  map[x].length) y  =  0;
	if (map[x][y]) return (1)
	return (0);
}
```
Ensuite nous allons crée les fonctions qui appellerons la fonction controlCellule et lui passer en arguments différent paramètres comme expliqué plus haut.


```JS

function  controlTopLane(x, y) {
	let  cel  =  0;
	cel  +=  controlCellule(x  -  1, y  -  1);
	cel  +=  controlCellule(x  -  1, y);
	cel  +=  controlCellule(x  -  1, y  +  1);
	return(cel);
}

function  controlMidLane(x, y) {
	let  cel  =  0;
	cel  +=  controlCellule(x, y  -  1);
	cel  +=  controlCellule(x, y  +  1);
	return(cel);
}

function  controlBotLane(x, y) {
	let  cel  =  0;
	cel  +=  controlCellule(x  +  1, y  -  1);
	cel  +=  controlCellule(x  +  1, y);
	cel  +=  controlCellule(x  +  1, y  +  1);
	return(cel);
}
```
Si vous regardez le code vous verrez  qu'en fait , ce qui ce passe c'est que chaqu'une des trois fonctions incrémente cell de 1 vu que controlCellule retourne 1 en cas de cellule vivante.

Bon , la c'est cool , on a plein de fonction qui font des trucs mais qui sont jamais appelé et si elles etaient appelée chaqu'une d'entre elle stockerais le nombre de céllules vivante dans une variable avec un scoop local...
Mais chaque fonction retourne le nombre de cell , donc on va de nouveau devoir stocké cela quelque part... 

Nouvelle fonction !! Elle va stocké le nombre de cellule true retourné par chaque fonctions de contrôle du tableau et stocké tout ça dans la variable celresult

```JS
function  controlAround(x, y) {
	let  celresult  =  0;
	celresult  +=  controlTopLane(x, y);
	celresult  +=  controlMidLane(x, y);
	celresult  +=  controlBotLane(x, y);
	return  celresult;
}
```

Ensuite , si on réfléchis , on a donc une fonction qui prends en paramètres une cellule , des fonctions qui regarde les cellules autours de la cellules en questions et qui retourne le nombre de cellules vivante , en fait , on a presque fini , maintenant on dois juste appliquer les règles définie.

Donc , si une cellule est vivante , a la prochaine génération elle le restera si elle a 2 ou 3 voisine vivante.
Sinon elle meurt.

Si une cellule est morte , a la prochaine génération elle prendra vie si elle a exactement 3 voisine vivante.
Sinon elle reste morte.

```JS
function  lookingForChangeState(x, y, celresult) {
	if (map[x][y]) {
		if (celresult  ==  2  ||  celresult  ==  3) map2[x][y] =  true;
		else  map2[x][y] =  false;
	}
	else {
	if (celresult  ==  3) map2[x][y] =  true;
	else  map2[x][y] =  false;
	}
}
```

Bon , c'est bien beau toute la partie logique , mais c'est quand même plus cool avec un affichage , c'est donc maintenant le moment de lié notre tableau logique avec le tableau de l'affichage , celui qu'on a crée tout au début , sur le quelle l'utilisateur peut cliqué pour coché les cases true !

```JS
function  ChangeDisplay (cell) {
	for ( let  x  =  0 ; x  <  map2.length ; x++) {
		for ( let  y  =  0 ; y  <  map2.length ; y++) {
			let  cell  =  document.getElementById(`cell-${x}-${y}`)
			if (map2[x][y] ==  false  &&  cell.classList[0] ==  'true') {
				cell.classList.replace('true' ,'false');
			}
			else  if (map2[x][y] ==  true  &&  cell.classList[0] ==  'false') {
				cell.classList.replace('false' ,'true');
			}
		}
	}
}
```

Maintenant nous avons tout ce qu'il nous faut , c'est le moment d'imbriqué tout ça afin d'appliquer la logique.
On va donc attendre que l'utilisateur aie cliqué sur le bouton play pour lancer une fonction dans un setinterval afin de générer a l'infini la suite logique de génération de cellules !!

Mais avant toute choses , on va avoir besoin de définir deux nouvelles variables globales
```JS
let  mylogictab  = [];
let  map  = [];
```
```JS
btnread.addEventListener('click' , () => {
	logicgame  =  setInterval(() => {
		map  =  createtab(mylogictab);
		map2  = [];
		for ( let  x  =  0 ; x  <  map.length ; x++) {
			for ( let  y  =  0 ; y  <  map.length ; y++) {
				let  cell  =  document.getElementById(`cell-${x}-${y}`)
				if (cell.classList[0] ==  'true') map[x][y] =  true;
			}
		}
		for ( let  x  =  0 ; x  <  map.length ; x++) map2.push(map[x].slice());
let  x  =  0;
while (x  <  map.length) {
	let  y  =  0;
	while (y  <  map.length) {
		const  celresult  =  controlAround(x, y);
		lookingForChangeState(x, y, celresult);
		y++;
	}
	x++;
	}
	map  =  map2;
	ChangeDisplay();
	},50)
});
```

Normalement , vous pouvez vous arrêtez ici , votre jeu de la vie fonctionne.

Si vous voulez ajouter des fonctionnalités vous pouvez , sur mon jeu de la vie j'ai le nombre de génération qui s'affiche , le bouton pause qui marche et il n'est pas possible de rajouter des cellules lorsque le jeu est en cours.

Il est aussi possible de rajouter des presset , une génération de map aléatoire et encore tellement d'autres choses.




