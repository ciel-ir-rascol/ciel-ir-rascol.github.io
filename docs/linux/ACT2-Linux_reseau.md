# ACT02 : Linux et le réseau

## 1 - Création d'un nouvel utilisateur

Vous allez créer sur le système un utilisateur avec les droits administrateur, le nom d'utilisateur `username` devra suivre le schéma suivant :
```text
Nom : Bombadil
Prénom : Tom

--> username : TBOMBADIL
```
**Bien entendu, remplacez `Bombadil` et `Tom` par vos propres nom et prénom !**

Pour cela il s'agit d'utiliser la commande : `adduser`, qui va créer un nouvel utilisateur avec possibilité de lui assigner un mot de passe, nom, prénom, adresse... Le site Ubuntu France, donne une explication complète de l'utilisation de cette commande allez y jeter un coup d'œil : [Ubuntu France tutoriel adduser](https://doc.ubuntu-fr.org/adduser)

![](figures/sandwich.png)

<sup>
<a href="https://xkcd.com/149/">"Sandwich"</a>, by <a href="https://xkcd.com">XKCD</a>
used under <a href="https://creativecommons.org/licenses/by-nc/2.5/">CC BY-NC 2.5</a>
</sup>

L'utilisateur créé ne dispose des privilèges root (super utilisateur, le `sudo`), il faut donc l'ajouter à la liste des `sudoers`, pour se faire suivez l'explication donnée par le site : [Ubuntu France tutoriel sudoers](https://doc.ubuntu-fr.org/sudoers)

!!! question
    1. Utilisez la commande `adduser` pour créer un nouvel utilisateur de votre choix, définissez également un mot de passe.

    2. Rajoutez une ligne au fichier `/etc/sudoers` pour autoriser l'accès au privilèges super utilisateur à votre nouvel utilisateur : `Nom_utilisateur ALL=(ALL:ALL) ALL`

    3. Identifiez vous avec le nouvel utilisateur créé avec `su nom_nouvel_utilisateur`

## 2 - Le gestionnaire de paquets

Les applications d'un système GNU/Linux sont gérées par un gestionnaire de paquet (**apt** pour Debian et donc Ubuntu, **yum** pour Fedora et **pacman** pour Archlinux) pour installer une application, nous ne procédons pas comme sur Windows où il s'agit la plupart du temps d'aller récupérer le fichier d'installation sur le site du fabricant, ou sur un site généraliste à la merci des virus et programmes publicitaires... 

Sur GNU Linux les applications sont dans des bases de données appelées **repositories**, chaque application est ainsi constamment maintenue à jour, vous êtes donc certains d'installer la dernière version et ce de manière fiable. Un gros avantage : la mise en jour de l'ensemble des applications du système se fait d'un seul coup, grâce au gestionnaire de paquets.

Avant d'installer quoi que ce soit sur la distribution **il faut toujours mettre à jour les repositories et ensuite mettre à jour le système**. Pour ce faire nous utilisons la commande `apt update` puis `apt upgrade`

!!! question
    1. Utilisez la commande `apt update` **en mode super utilisateur** pour mettre à jour les bases de données.

    2. Utilisez la commande `apt upgrade` **en mode super utilisateur** pour mettre à jour le système.

## 3 - La configuration réseau sous Linux

La commande `ip a` permet de visualiser la configuration réseau de l'ordinateur, grâce à elle nous pouvons obtenir des informations sur l'adresse IP, l'adresse MAC ou encore l'interface réseau utilisée.

!!! question
    1. Utilisez la commande `ip a` pour obtenir le nom de l'interface réseau utilisé

    2. Utilisez la même commande pour obtenir votre adresse IP

A présent nous souhaitons modifier l'adresse IP de l'interface réseau utilisé, pour ce faire nous utiliserons la commande `ifconfig eth0 nouvelle-adresse`, **la nouvelle adresse devra correspondre au numéro de l'ordinateur**.

Dans la section CIEL-IR l'adressage IP est configuré de cette manière :

**192.168.A.B**

* **A** : Salle (si salle D116 : 116)
* **B** : Poste (si poste D116-03 : 3)

!!! question
    1. Changez l'adresse IP de votre machine, pour ce faire vous vous aiderez du tutoriel suivant : [How to Set Up a Static IP Address on Debian 12 Linux](https://itslinuxfoss.com/set-up-static-ip-address-debian-12-linux/#2)
    
    **🚨 Vous utiliserez obligatoirement la méthode 2 : Set Up a Static IP Address on Debian 12 Using the Network Manager**

## 4 - Les transferts réseaux

### a - Commande ``ping``

Avant de transférer un document ou de se connecter à un ordinateur distant, il faut vérifier si celui-ci est présent sur le réseau. La commande `ping` en utilisant une requête [ICMP](https://fr.wikipedia.org/wiki/Internet_Control_Message_Protocol), le protocole va envoyer un paquet sur la cible, si la cible est accessible elle va répondre à la requête en envoyant un paquet à l'émetteur.

!!! question
    1. Utiliser la commande ``ping`` pour vérifier l'accessibilité du site web de votre choix. Relevez le temps aller-retour (round trip time).

    2. Utilisez la même commande sur l'adresse IP de votre voisin de TP. Relevez le temps aller-retour.

### b - Prendre la main à distance avec ssh

Le protocole ssh permet de se connecter de manière sécurisée (transferts cryptés) à un ordinateur linux distant. Pour vous connecter à votre machine à distance vous devez installer un serveur ssh, le client installé d'office permet juste de se connecter à partir de votre machine à une autre.

* Installez le paquet ``openssh-server``

La connexion à ordinateur distant se fait en utilisant la commande :

``ssh nom_utilisateur_cible@adresse_ip_cible``

!!! question
    3. Connectez-vous en ssh à l'ordinateur de votre voisin de TP

    4. Créez sur son bureau un fichier ``robot.bak`` avec nano du contenu de votre choix.

    5. Demandez à votre voisin si le fichier est bien sur son bureau.
