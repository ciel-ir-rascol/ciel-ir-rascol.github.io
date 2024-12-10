# Réalisation de scripts Bash

## 1 - Éditer et lancer un script

Pour éditer votre script Bash dans l'environnement GNU/Linux deux options s'offrent à vous :

* Utiliser un éditeur de texte en ligne de commande tel que **nano** ou **vim**.
* Utiliser un éditeur de texte graphique comme **gedit**

Une fois votre éditeur ouvert, la première chose à écrire est :

```bash
#!/bin/bash
```

Cette ligne de code indique au terminal quel type de Shell il doit utiliser, dans notre cas nous utiliserons le Shell Bash. Si vous souhaitez avoir des informations sur les différents types de Shell, je ne peux que vous conseiller d'aller voir la page Wikipédia suivante :
[lien](https://fr.wikipedia.org/wiki/Shell_Unix)

Ensuite il faut avant tout enregistrer votre nouveau fichier de script, pour cela donnez lui l'extension `.sh`, extension utilisée pour les scripts Bash.

Pour lancer un script et observer son fonctionnement, positionnez vous avec le terminal à l'endroit où il est situé (voir commandes `cd` et `ls`), puis entrez les commandes suivantes :

```bash
$ chmod a+x nom_du_script.sh
```

Cette ligne donne le droit d'exécution de votre script à tout le monde.

```bash
$ ./nom_du_script.sh
```
Cette ligne lance votre script.

## 2 - Utilisation de variables

### 2.1 - Déclaration

Pour déclarer une variable en shell Bash il suffit rentrer son nom puis sa valeur initiale :

```bash
foo="je suis le contenu de foo"
bar=22
test=22.69
```
Ci-dessus nous avons déclaré et initialisé 3 variables : Une chaîne de caractère `foo`, un entier `bar` et un flottant `test`. Remarquez qu'il n'est pas nécessaire de déclarer le type de la variable, Bash va automatiquement le faire suivant valeur initiale choisie.

!!! warning
    Lors de la déclaration d'une variable attention à ne pas mettre d'espace entre la fin du nom et le `=`

### 2.2 - Utilisation

Pour utiliser le contenu d'une variable il faut mettre le symbole `$` devant le nom de celle-ci, on fait alors référence à sa case mémoire, son contenu.

- Faire des calculs avec les variables :
  
  Une syntaxe particulière est utilisée pour faire faire un calcul entre 2 ou plusieurs variables, exemple de script ci-dessous :
  ```bash
  #!/bin/bash
  a=10
  b=12
  c=$((a+b))
 
  # Afficher le résultat à l'écran
  echo $c
  ```
  
  1. Déclaration de 2 variables `a` et `b` initialisées respectivement à `10` et `12`
  2. Addition dans `c`
  3. Affichage du contenu de `c` à l'écran grâce à la commande `echo`

!!! warning
    Bash ne permet pas directement de faire des additions avec des nombres décimaux. Ci nécessaire installer l'application appelée `bc` permettant de gérer le calcul en nombres flottants.

<script id="asciicast-sT9oX27Ovl7qk58jKjWEN1EEe" src="https://asciinema.org/a/sT9oX27Ovl7qk58jKjWEN1EEe.js" async></script>

- Concaténer des chaînes de caractères
  
  Bash permet de concaténer rapidement le contenu de 2 variables de type chaîne de caractères, un exemple ci-dessous :

  ```bash
  #!/bin/bash
  a="J'aime "
  b="coder avec le shell Bash !" 
  c=$a$b
 
  # Afficher le résultat à l'écran
  echo $c
  ```
  1. Déclaration de 2 variables `a` et `b` initialisées respectivement à `J'aime ` et `coder avec le shell Bash`
  2. Concaténation dans `c`
  3. Affichage du contenu de `c` à l'écran grâce à la commande `echo` 
   
<script id="asciicast-3FRKfaaTT8AZEbgQVKZTGOL2D" src="https://asciinema.org/a/3FRKfaaTT8AZEbgQVKZTGOL2D.js" async></script>

## 3 - Les structures conditionnelles

### 3.1 Les opérateurs de comparaison

| Opérateur | Nom                                    |
| --------- | -------------------------------------- |
| -lt       | lower than (inférieur à)               |
| -gt       | greater than (supérieur à)             |
| -eq       | equal (égal à)                         |
| -ne       | not equal (différent de)               |
| -ge       | greater or equal (supérieur ou egal à) |
| -le       | lower or equal (inférieur ou égal à)   |

!!! info
    Ces opérateurs sont uniquement utilisables avec des nombres, pour les chaines de caractères voir ci-dessous. De plus Bash ne permet pas directement de comparer des nombres décimaux, **ces expressions fonctionnent seulement avec des entiers**.

| Opérateur | Nom        |
| --------- | ---------- |
| ==        | Égalité    |
| !=        | Différence |


### 3.1 If

La structure `if` effectue le test donné, si il est vrai, elle dirige l'exécution vers le `then`, dans le cas contraire elle continu la suite des instructions, un script exemple ci-dessous :

```bash
#!/bin/bash

# Capture des 2 nombres saisis par l'utilisateur
echo "Rentrez le premier nombre"
read a # Saisi du nombre a
echo "Rentrez le second nombre"
read b # Saisi du nombre b

# Test d'infériorité de a sur b
if [ $a -lt $b ]; then
    echo "a est inférieur à b"
fi

# Test de supériorité de a sur b
if [ $a -gt $b ]; then
    echo "a est supérieur à b"
fi

# Test d'égalité de a et b
if [ $a -eq $b ]; then
    echo "a est égal à b"
fi
```

!!! warning
    Toujours mettre un espace après le 1er `[` et avant le dernier `]` de la condition.

<script id="asciicast-3r6hSzznZj48YWfIZPOALfT3R" src="https://asciinema.org/a/3r6hSzznZj48YWfIZPOALfT3R.js" async></script>

### 3.2 If Else

Nous reprenons le script précédent en utilisant une structure `if elif` :

```bash
#!/bin/bash

# Capture des 2 nombres saisis par l'utilisateur
echo "Rentrez le premier nombre"
read a # Saisi du nombre a
echo "Rentrez le second nombre"
read b # Saisi du nombre b


if [ $a -lt $b ]; then # Test d'infériorité de a sur b
    echo "a est inférieur à b"
elif [ $a -gt $b ]; then  # Sinon test de supériorité de a sur b
    echo "a est supérieur à b"
elif [ $a -eq $b ]; then # Sinon test d'égalité de a et b
    echo "a est égal à b"
fi
```

### 3.3 Case

La structure `case` très utilisée dans les menus, permet d'orienter le programme suivant un choix de l'utilisateur :

```bash
#!/bin/bash
echo "Rentrez un nombre compris entre 1 et 4"
read nb # Saisi du nombre nb

case $nb in # Tests sur la variable nb, contenant le nombre saisi
    1) echo "Super ! Vous avez saisi 1";; # Ne pas oublier les 2 ;; sauf sur la dernière ligne
    2) echo "Formidable ! Vous avez saisi 2";;
    3) echo "Fantastique ! Vous avez saisi 3";;
    4) echo "Wahoo ! Vous avez saisi 4";;
    *) echo "Vous n'avez rien saisi de valable ! Dommage" # Cas où nb different de [1;4]
esac
```
<script id="asciicast-fAMGFUlSxYNNvZ7cfALcaO49r" src="https://asciinema.org/a/fAMGFUlSxYNNvZ7cfALcaO49r.js" async></script>

## 4 - Les boucles

### 4.1 While

La boucle `while` ou "tant que" permet de répéter un ensemble d'instructions tant que la condition donnée est vraie, exemple ci-dessous :

```bash
#!/bin/bash

i=0 # Initialisation de la variable de comptage à 0
while [ $i -lt 5 ]; do # On tourne tant que i<5
    echo "compteur = "$i # On affiche le contenu de i
    i=$(($i+1)) # On incrémente i
done 
```

<script id="asciicast-uo8m9lOLooHmdt1bQKdsnB31K" src="https://asciinema.org/a/uo8m9lOLooHmdt1bQKdsnB31K.js" async></script>

### 4.2 Until

La boucle `until` ou "jusqu'à" contrairement à la boucle `while` va s'exécuter jusqu'à ce que la condition soit vérifiée. Nous reprenons l'exemple précédent et adaptons la condition pour compter de 0 à 4 :

```bash
#!/bin/bash

i=0 # Initialisation de la variable de comptage à 0
until [ $i -gt 5 ]; do # On tourne jusqu'à ce que i>4
    echo "compteur = "$i # On affiche le contenu de i
    i=$(($i+1)) # On incrémente i
done 
```
<script id="asciicast-yvWruoqljzLb5wqysKE4U6hAY" src="https://asciinema.org/a/yvWruoqljzLb5wqysKE4U6hAY.js" async></script>

### 4.3 For

La boucle `for` est très utilisée en shell Bash pour parcourir les éléments d'une liste, d'un fichier ou encore le contenu d'un répertoire. Dans l'exemple ci-dessous nous listons tous les fichier du répertoire courant soit /home/foo/ :

```bash
#!/bin/bash

i=0 # Initialisation de la variable de comptage à 0
# On parcourt le répertoire actuel, le nom du fichier recueilli est mis dans la var nom_fichier à chaque itération 
# '*' Désigne l'ensemble des fichier du répertoire
for nom_fichier in *; do 
    echo $i". "$nom_fichier
    i=$(($i+1)) # On incrémente i
done
```

<script id="asciicast-hoBrPRCznnxjkYIG9k4oRR8J5" src="https://asciinema.org/a/hoBrPRCznnxjkYIG9k4oRR8J5.js" async></script>


## 5 - Les paramètres positionnels 

Les paramètres positionnels sont les paramètres passés en entrée d'un script quand vous appelez celui-ci dans le terminal. Par exemple lors de l'utilisation de la commande `rm` on peut passer l'option `-r` qui est un paramètre positionnel : `rm -r`

Il est facile d'utiliser ces paramètres en Bash ils sont référencés par un numéro : 1 pour le premier paramètre, 2 pour le second ...

```bash
$ mon_script param1 param2 param3
```
Pour utiliser ces paramètres dans le script :

```bash
#!/bin/bash

$1 # Utilisation du premier paramètre
$2 # Utilisation du second paramètre
$3 # Utilisation du troisième paramètre
```

!!! info
    Le paramètre positionnel `$0` est une chaîne de caractères contenant le nom du script