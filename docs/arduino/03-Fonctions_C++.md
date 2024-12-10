# Les fonctions de base du langage C/C++

Le langage C/C++ utilisé pour la programmation des microcontrôleurs Atmel est le langage choisi par Arduino pour la
programmation de ses cartes électroniques. Dans ce cours nous donnons les principaux mots-clés du langage permettant de
reproduire les structures de bases vues en algorithmique : structures linéaires, alternatives et répétitives.

## 1. Les opérateurs de comparaison

Le tableau suivant liste les opérateurs utilisés en C/C++ pour définir des conditions :

| Opérateurs |                   |
|:-----------|:------------------|
| ```==```   | Egalité           |
| ```!=```   | Différence        |
| ```<```    | Inférieur         |
| ```>```    | Supérieur         |
| ```<=```   | Inférieur ou égal |
| ```>=```   | Supérieur ou égal |

!!! warning
L'erreur classique est de confondre le **```=```** et le **```==```**, notez que le premier est pour l'affectation
d'une valeur à une variable et le second pour la comparaison. De plus le langage C/C++ n'autorise pas l'encadrement
de variables entre deux valeurs dans une condition tel que : **```5<toto<10```**, pour écrire une telle condition
il suffit d'utiliser l'opérateur logique **```&&```**.

## 2. Les opérateurs logiques

Le tableau suivant liste les opérateurs logiques utilisés en C/C++ pour définir des conditions :

| Opérateurs |   |
|:------------- |:---------------|
| ```&&```      | Et logique |
|  &#124; &#124;     | Ou logique        |
| ```!``` | Non      |

!!! warning
Faire attention à ne pas confondre le **```&&```** et le **```&```** ou le **```||```** et le **```|```**. Dans le cas
du double symbole l'utilisation est pour une condition, dans le cas du symbole seul l'utilisation est un pour une
opération logique bit à bit.

## 3. Les conditions

### 3.1 Si Alors : ```if() ```

La condition **Si Alors** permet de réaliser une ou plusieurs actions si seulement la condition énoncée est vrai, si ce
n'est pas le cas le programme saute la condition et poursuit son exécution. La structure de cette condition est donnée
ci-dessous :

![](figures/if.svg)

!!! warning
Le langage C/C++ utilise l'accolade ouverte **```{```** pour indiquer l'entrée dans une fonction et l'accolade
fermée **```}```** pour en sortir, afin de na pas oublier cette particularité propre à ce langage il est **vivement
conseillé de bien indenter son code** pour en améliorer la lisibilité.

Nous donnons ci-dessous un code exemple utilisant cette fonction.

```c++
int a = 0; //Déclaration d'un entier "a", initialisé à 0

if(a<10) //Condition pour entrer dans le si : "a" doit être strictement inférieur à 10
{
	a=a+1; // Si "a" est inférieur à 10 alors on rajoute 1 à "a".
}

```

### 3.2 Si Alors Sinon : ```if() else```

La condition **Si Alors Sinon** permet de réaliser une ou plusieurs actions si seulement la condition énoncée est vrai,
si ce n'est pas le cas le programme aiguille l'exécution vers le Sinon. La structure de cette condition est donnée
ci-dessous :

![](figures/if_else.svg)

Nous donnons ci-dessous un code exemple utilisant cette fonction.

```c++
int a = 0; //Déclaration d'un entier "a", initialisé à 0

if(a<10) //Condition pour entrer dans le si : "a" doit être strictement inférieur à 10
{
	a=a+1; // Si "a" est inférieur à 10 alors on rajoute 1 à "a"
}
else
{
	a=a-1; // Sinon on enlève 1 à "a"
}

```

### 3.3 Le choix multiple : ```switch() case```

Le choix multiple permet pour une variable de notre choix, d'aiguiller le programme suivant la valeur que cette variable
va prendre. La structure de cette condition est donnée ci-dessous :

![](figures/switch-case.svg)

Nous donnons ci-dessous un code exemple utilisant cette fonction.

```c++
int var_choix = 0; //Déclaration d'un entier "var_choix", initialisé à 0

switch(var_choix) //Mise en place d'un choix multiple pour la variable var_choix
{
	case 1: //Actions à exécuter dans le cas où var_choix = 1
			 break; //Indication de fin d'instructions pour ce case

	case 2: //Actions à exécuter dans le cas où var_choix = 2
	 		 break; //Indication de fin d'instructions pour ce case

	default: //Actions à exécuter dans le cas où var_choix est différent de tous les cases précédents
	 		 break; //Indication de fin d'instructions pour ce case
}

```

## 4. Les boucles

### 4.1 Tant que : ```while()```

La boucle **Tant que** permet de répéter une suite d'instructions tant que le condition énoncée au début est vraie. La
structure de cette boucle est donnée ci-dessous.

![](figures/while.svg)

Nous donnons ci-dessous un code exemple utilisant cette fonction.

```c++
while(1) //Permet de réaliser une boucle infinie équivaut à écrire while(1=1)
{
	//Suite d'instructions à réaliser dans la boucle
}

```

### 4.2 Faire Tant que : ```do while()```

La boucle **Faire Tant que** permet de répéter une suite d'instructions tant que le condition énoncée à la fin est
vraie, **la suite d'instructions sera réalisée au moins une fois car le test de la condition ne se fait qu'à la fin**.
La structure de cette boucle est donnée ci-dessous.

![](figures/do_while.svg)

Nous donnons ci-dessous un code exemple utilisant cette fonction.

```c++
do
{
	//Suite d'instructions à réaliser dans la boucle
}while(1); //Permet de réaliser une boucle infinie équivaut à écrire while(1=1)
```

### 4.3 Pour : ```for()```

La boucle **Pour** permet de répéter une suite d'instructions selon une évolution définie au début. La structure de
cette boucle est donnée ci-dessous.

![](figures/for.svg)

Paramétrage de la boucle ```for```:

* Initialisation de la variable de comptage : Exceptionnellement et **que** dans ce cas bien précis nous autorisons la
  déclaration de variable au cours du programme. La variable de comptage ici ```cpt``` est la variable qui
  s'incrémentera ou se décrémentera **à chaque passage dans la boucle** suivant le pas de comptage choisi, celle-ci est
  ici initialisée à 0.

* Condition de comptage : Nous définissons ici la condition d'exécution de la boucle, dans notre cas nous tournerons
  dans le boucle tant que la variable de comptage ```cpt``` est inférieure à 10.

* Pas de comptage : Ici nous définissons l'évolution de la variable de comptage ```cpt``` lors de chaque passage dans la
  boucle. Dans notre cas nous incrémentons de 1 à chaque passage dans la boucle, ```cpt++``` revient à
  coder ```cpt=cpt+1```. Nous aurions pu également décrémenter de 1 : ```cpt--```, ou bien choisir un pas différent de
  1 : ```cpt=cpt+3```.

Nous donnons ci-dessous un code exemple utilisant cette fonction.

```c++
for(int cpt=0;cpt<10;cpt++) //Boucle en initialisant cpt à 0 tant que cpt<10 et incrémente de 1 à chaque passage
{
	//Suite d'instructions à réaliser dans la boucle
}
```
