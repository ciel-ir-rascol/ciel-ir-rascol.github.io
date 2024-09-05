# DM de Noël : Jeu devine la capitale

## 1. Énoncé 

Nous donnons ci-dessous un fichier contenant la liste des 196 pays reconnus par l'ONU dans le monde, ce fichier en langue Anglaise est organisé de la manière suivante :

```bash
Costa Rica -- San Jose
Cote d'Ivoire -- Yamoussoukro
Croatia -- Zagreb
Cuba -- Havana
```

Chaque ligne comporte un pays suivi par sa capitale, les deux sont séparés par `--` 

A télécharger ici : [capitales.txt](https://rascolsin.fr/tsti2d/linux/ressources/capitales.txt)

```bash
wget https://rascolsin.fr/tsti2d/linux/ressources/capitales.txt
```

Le script que vous devez réaliser, tire de manière aléatoire une ligne parmi les 196, affiche à l'écran le nom du pays et demande à l'utilisateur de saisir la capitale correspondante.

L'utilisateur a le droit à 5 tentatives, si les 5 tentatives sont infructueuses le programme met fin à la partie.

## 2. Coup de pouce

Pour réaliser le script nous donnons ci-dessous quelques commandes qui peuvent vous permettre d'arriver à une solution :

### Commande `shuf`

L'utilitaire `shuf` permet de tirer de manière aléatoire une ou plusieurs lignes du fichier texte passé en paramètre :

```bash
shuf -n 1 capitales.txt
```
Cette commande va renvoyer une ligne (option `-n 1`) tirée au sort depuis le fichier `capitales.txt`

### Commande `awk`

L'utilitaire `awk` permet d'extraire une section de texte d'un fichier suivant un critère donné, l'option `-F` permet de choisir un ou plusieurs caractères de séparation.

Exemple d'utilisation pour séparer 2 éléments d'une chaîne de caractères :

```bash
couple="Romeo,Juliette"
Homme="$(echo $couple | awk -F"," '{print $1}')" 
Femme="$(echo $couple | awk -F"," '{print $2}')" 
```

Ici le caractère de séparation utilisé est `,` nous paramétrons donc `-F","`. `awk` sépare ensuite les termes, pour afficher le 1er donc `Romeo` dans notre exemple, il suffit d'ajouter `'{print $1}'`


