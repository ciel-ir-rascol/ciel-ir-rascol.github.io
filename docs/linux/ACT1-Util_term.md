# ACT01 : Utiliser le terminal

Le but de cette activité est une initiation à l'utilisation de la ligne de commande sous Linux. Nous souhaitons pour cette séance nous focaliser sur l'utilisation de Linux à l'aide de la console, inventée dans les années 70, quand l'interface graphique n'existait pas encore.<br/>Aujourd'hui la console est appréciée pour son gain de temps (commandes intuitives courtes et abrégées), et sa très faible consommation de ressources graphiques. Savoir utiliser la console nous permet de comprendre comment le système fonctionne, loin d'être un outil tombé en désuétude le terminal est encore aujourd'hui l'ultime moyen d'arriver à ses fins et quelle qu'elles soient, sur un système GNU/Linux.

## 1 - Ouverture du terminal

Cette activité se déroulera sur une distribution GNU/Linux, en l’occurrence Debian, installée sur tous les postes des salles D116 et D117.

1. Démarrez l'ordinateur
2. Log-in
3. Grâce au lanceur démarrez un terminal :
![](figures/screen_choix_term.png)
1. Félicitations ! Vous êtes devant un invite de commande aussi appelé *prompt*
![](figures/termPrompt.png)

## 2 - Déplacement dans l'arborescence

### a - Commandes ```ls```, ```ls -a``` , ```cd``` et ```pwd```:

* Utilisez la commande ```pwd``` pour visualiser le chemin de votre emplacement actuel.
* Déplacez-vous sur la racine du système soit l'emplacement ```/``` à l'aide de ```cd```
* Une fois fait utilisez la commande ```ls``` pour afficher l'ensemble des fichiers et dossiers composant le répertoire actuel. Retrouvez l'arborescence évoquée précédemment.
* Rajoutez à ```ls``` l'option ```-a``` soit ```ls -a``` Que remarquez vous ? Que signifie le point devant certains fichiers ?

### b - Utilisation de ```nano``` l'éditeur de texte :

* Déplacez vous à l'aide de ```cd``` dans le répertoire ```/home/admin-cielir/Documents```
* Créez à l'aide de l'éditeur ```nano``` un nouveau document appelé : ```Activité_Linux```
* Écrivez dans le document le texte suivant : ```Linux c'est vraiment génial !```
* Quittez ```nano``` en enregistrant votre fichier quand il vous le demande.
* Visualisez à l'aide de ```ls``` si le fichier à bien été créé et ré-ouvrez le avec ```nano``` pour revoir votre création.
* Rajoutez ```ça c'est sûr !``` à la suite de votre texte.
* Quittez à nouveau ```nano``` en enregistrant une dernière fois.

### c - Utilisation de ```mv```, ```cp```, ```rm``` et ```mkdir```

* Vous souhaitez créer un nouveau répertoire où mettre le fichier que vous venez de créer, utilisez la commande ```mkdir``` pour créer un répertoire s'appelant « ```Cours_Linux``` » toujours dans ```/home/admin-cielir/Documents```
* Déplacez le fichier « ```Activité_Linux``` » dans ce nouveau dossier à l'aide de la commande ```mv```, vérifiez que le dé-
placement a bien été effectué
* Vous vous êtes trompés de nom et souhaitez renommez le fichier ```Activité_Linux``` en ```Premier_cours_Linux``` utilisez pour cela à nouveau la commande ```mv```, vérifiez que le changement a bien été effectué.
* Créez une copie de ce même fichier sur le bureau à l'aide de la commande ```cp```, vérifiez si la copie est présente sur le bureau.
* Vous réalisez que vous n'avez finalement pas besoin de la copie sur le bureau et souhaitez la supprimer grâce à la commande ```rm```
* Vous souhaitez également supprimer le dossier « Premier_cours_Linux » qui finalement ne vous sert pas à grand chose. Rajoutez pour cela l'option ```-r``` à ```rm```.
