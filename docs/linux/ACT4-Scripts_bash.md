# Activité : Écrire des scripts Bash

## Exercice 1 : Tables de multiplication 

Créez un script Bash affichant la table de multiplication d'un nombre entier rentré par l'utilisateur.

Le comportement devra être le suivant :

<script id="asciicast-9hzruFZDTLheuZa1tRcxUBcEv" src="https://asciinema.org/a/9hzruFZDTLheuZa1tRcxUBcEv.js" async></script>

!!! question
    - Écrivez le script Bash en utilisant l'éditeur de votre choix.
    - Vérifiez le fonctionnement en lançant le script et en le testant
    - Appelez l'enseignant pour vérifier

## Exercice 2 : Jeu deviner un nombre

Créez un jeu dans lequel l'ordinateur tire un nombre entre 2 valeurs données en paramètres d'entrée, puis propose à l'utilisateur de deviner ce nombre en 5 essais.
Si il n'y parvient pas mettez fin au script.

Le comportement devra être le suivant :

<script id="asciicast-rj5cb2f32ZQaPpUsFZXUqSvUf" src="https://asciinema.org/a/rj5cb2f32ZQaPpUsFZXUqSvUf.js" async></script>

??? note "Tirer un nombre aléatoire en Bash"
    Pour créer un nombre aléatoire en Bash, il faut utiliser la fonction `$RANDOM` qui donne en retour un entier signé, soit un nombre entre 0 et 32767.

    Pour borner ce nombre aléatoire entre 2 valeurs : [a;b] il faut utiliser la fonction modulo noté `%` En Bash renvoyant le reste d'une division Euclidienne. En effet, le reste d'une division de x par y est toujours compris entre 0 et y (exclu)


## Exercice 3 : Script de backup

Nous souhaitons réaliser un script de backup fonctionnant à l'aide de l'utilitaire `rsync`, la sauvegarde sera incrémentale avec mémorisation des fichiers supprimés. Nous donnons les étapes suivantes :

### 1. Sauvegarde locale

Dans un premier temps sauvegarder `Documents` dans `Backup` localement en utilisant l'arborescence suivante :

```bash
/home
|--Documents
|----Fichier1
|----Fichier2
|----Fichier3
|
|--Backup
|----Courant
|----Trash
```

* `Documents` est le dossier dont le contenu est à sauvegarder
* `Backup` est le dossier contenant la sauvegarde
    * `Courant` est le clone de `Documents`
    * `Trash` est une mémoire de tous les fichiers supprimés


Les options de l'utilitaire `rsync` à utiliser pour réaliser cette partie sont :

* `-a` Option d'archivage, active la récursivité et permet de conserver les permissions
* `-u` Option update, la synchronisation se produit seulement quand les fichiers de la sauvegarde sont plus anciens que les fichiers sauvegardés
* `--delete` Option suppression, quand les fichiers sont supprimés sur la source, ils sont également supprimés sur la sauvegarde
* `--backup` Option sauvegarde, les fichiers supprimés sont conservés
* `--backup-dir=[chemin dossier trash]` Fonctionne avec l'option précédente permet d'indiquer le chemin du dossier de sauvegarde
* `--stats` Avec cette option rsync renvoi les statistiques à la fin de la réalisation de la sauvegarde


### 2. Envoi de mail

Nous souhaitons envoyer à l'utilisateur le résultat du déroulement de la sauvegarde, pour cela nous pouvons utiliser l'utilitaire `ssmtp` permettant d'envoyer des mails en ligne de commande. Cet utilitaire permet d'utiliser le service classique d'envoi de mail smtp fourni par votre fournisseur de mail, dans notre cas Gmail.

Le site [pihomeserver](https://www.pihomeserver.fr/2015/08/13/envoyer-un-email-depuis-votre-raspberry-pi/) donne une explication très détaillée sur l'utilisation de `ssmtp` pour envoyer un mail.

### 3. Sauvegarde à distance

Nous souhaitons à présent réaliser les sauvegardes non plus sur site mais à distance, pour cela paramétrez votre répertoire de destination pour utiliser `rsync` avec ssh.

Exemple de variable contenant le répertoire de destination paramétré pour une sauvegarde avec ssh :

```bash
REPERTOIRE_DESTINATION="foo@192.168.1.2:/home/foo/Backup/Courant"
```