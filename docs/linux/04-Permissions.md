# Gérer les permissions en environnement GNU-Linux

Linux se veut être un système robuste aux virus et aux intrusions, en partie grâce aux permissions applicables sur chaque fichier ou dossier. Un utilisateur classique connecté au système ne peut avoir avoir un accès en modification qu'aux fichiers présents dans son `home`, pour le reste il doit s'identifier en tant que super-utilisateur. En effet avec Linux, chaque fichier appartient à un utilisateur et un groupe, les permissions en lecture, écriture et exécutions peuvent être paramétrées pour chacun.

## 1. Gérer les utilisateurs et les groupes

### 1.1 Ajouter/Supprimer un utilisateur
- Créer un nouvel utilisateur
  
!!! snippet
    `sudo adduser [nom]`

Lors de la création d'un nouvel utilisateur le système demande un mot de passe, ainsi que plein d'autres renseignements tels que `room` `phone number`... Il n'est pas nécessaire de remplir ces informations appuyez sur entrer pour passer dessus.

!!! info
    Lors de la création d'un nouvel utilisateur, linux crée automatiquement un groupe du même nom. 

- Se logger avec le nouvel utilisateur créé

!!! snippet
    `su [nom_utilisateur]`

- Supprimer un utilisateur

!!! snippet
    `sudo deluser [nom]`

### 1.2 Ajouter/Supprimer un groupe

- Ajouter un groupe
  
!!! snippet
    `sudo addgroup [nom]`

- Supprimer un groupe

!!! snippet
    `sudo delgroup [nom]`

### 1.3 Ajouter/Retirer un utilisateur d'un groupe

- Ajout d'un utilisateur à un groupe

!!! snippet
    `sudo adduser [utilisateur] [groupe]`

- Retrait d'un utilisateur d'un groupe

!!! snippet
    `sudo deluser [utilisateur] [groupe]`

### 1.4 Visualiser les groupes d'appartenance d'un utilisateur

!!! snippet
    `sudo groups [utilisateur]`



## 2. Voir les permissions attribuées

Pour lister les permissions des fichier ou dossiers contenus dans un répertoire, il suffit de taper la commande suivante dans votre terminal :

!!! snippet
    `ls -l`

Et pour afficher également les permissions sur les fichiers et dossiers cachés :

!!! snippet
    `ls -al`

Un exemple d'affichage des permissions du contenu du répertoire `/home/marcel/` dans une distribution ubuntu :

<script id="asciicast-S6QY2IAf9jbwXD86J8EH6BMtH" src="https://asciinema.org/a/S6QY2IAf9jbwXD86J8EH6BMtH.js" async></script>

Nous détaillons ci-dessous le contenu de la ligne du dossier `Musique` :

![](figures/Schema_permissions.png)

Une distribution Linux est organisée avec un ou plusieurs **utilisateurs** réparties dans des **groupes**. Dès qu'un nouvel utilisateur est créé il est **automatiquement placé dans un groupe du même nom**.

A chaque fichiers et dossiers sont attribués des permissions en **lecture**, **écriture** et **exécution**. Lors de l'affichage avec `ls -l` elles sont affichées de la manière suivante :

```bash
rwx # Droits en R-Lecture W-Écriture X-Exécution
r-x # Droits en R-Lecture et en X-Exécution
--x # Juste le droit en X-Exécution
```

## 3. Modifier les permissions

Pour modifier les permissions attribuées à un fichier ou un dossier il faut utiliser la commande :

!!! snippet
    `sudo chmod [options] [file or folder]`

La modification se fait en désignant l'utilisateur `u` propriétaire pour *user*, le groupe `g` propriétaire pour *group*, et le restant `a` pour *all*.

Ci dessous quelques exemples de modifications effectuées sur le fichier `foo` :

```bash
sudo chmod a+x foo #Ajout au fichier foo du droit en execution pour tous les utilisateurs.

sudo chmod g-r foo #Retrait au fichier foo du droit en lecture pour le groupe.

sudo chmod u-x foo #Retrait au fichier foo du droit d'exécution pour l'utilisateur.
```

Nous montrons ci-dessous l'exemple du paramétrage des permissions effectué sur le fichier `foo`:

<script id="asciicast-tnYC6bLJZ7TeZ7NKf3YPTIhQ7" src="https://asciinema.org/a/tnYC6bLJZ7TeZ7NKf3YPTIhQ7.js" async></script>

Remarquez qu'il nous faut dans cet exemple, trois lignes pour modifier les permissions du fichier `foo`, une autre technique nous permet de le faire d'un seul coup :

```bash
sudo chmod 637 foo #Attribution des permissions rw--wxrwx
```
Cette méthode est issue de la conversion binaire-décimal :

```
rw-|-wx|rwx ---> 110|011|111 --décimal--> 6|3|7
```

## 4. Modifier le propriétaire

La commande suivante permet de modifier le propriétaire d'un fichier ou un dossier :

!!! snippet
    sudo chown [user] [file or folder]

Ci-dessous nous donnons un exemple de modification du propriétaire du fichier `foobar` :

```bash
sudo chowm alice foobar #Changement de propriétaire du fichier foobar pour l'utilisateur alice.
```

Ci-dessous nous donnons un exemple de modification du propriétaire du dossier `Photos` :

```bash
sudo chown -R alice Photos #Changement de propriétaire du dossier Photos pour l'utilisateur alice.
```

!!! info
    L'option `-R` ajoutée à la commande `chown` est la récursivité elle permet de modifier le propriétaire sur le dossier et l'ensemble de son contenu.

Exemple de modification de propriétaire du dossier `Documents` :
<script id="asciicast-qDUgWqnLhar2101WcNfugFyH5" src="https://asciinema.org/a/qDUgWqnLhar2101WcNfugFyH5.js" async></script>

## 5. Modifier le groupe

Pour modifier le groupe d'appartenance d'un fichier ou dossier, 2 options s'offrent à nous :

* Utiliser la commande précédente de cette manière :

!!! snippet
    ```sudo chown [user]:[group] [file or folder]```

* Utiliser la commande `chgrp` :

!!! snippet
    `sudo chgrp [group] [file or folder]`


Ci-dessous un exemple de changement de groupe avec les deux commandes précédentes :
<script id="asciicast-wGuBn72Tew50ObmqLxUD25Nzj" src="https://asciinema.org/a/wGuBn72Tew50ObmqLxUD25Nzj.js" async></script>
