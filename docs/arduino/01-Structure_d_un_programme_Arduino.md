# Structure d'un programme Arduino

Un programme Arduino est toujours structuré de la même manière : Une partie initialisations et déclarations de variables, une partie setup() et une partie loop()

## 1. Le cartouche

Tout programme doit contenir un cartouche, il permet d'informer le lecteur sur :

* Le nom du programme
* Le rôle du programme, décrit en quelques mots.
* Son auteur et éventuellement comment communiquer avec lui (mail)
* La version du code en commençant par V0.0 et sa date
* Éventuellement une licence si le code est publié sur internet
* Le logiciel permettant sa compilation (dans notre cas l'IDE Arduino)

Voici un exemple de cartouche pour un programme Arduino avec licence GNU V3.0, que vous pouvez utiliser pour vos propres codes :

```c++
/**************************************************************************************************
Nom ......... : Projet_Alarme_Emission_433.ino
Role ........ : Transmet en 433MHz grâce à la bibliothèque VirtualWire une chaîne de
                caractère sur la pin 12 de l'Arduino Mega 2560
                * Dans le cas normal envoi :"Repos_capteur_ILS"
                * Dans le cas d'un front montant sur CapteurPin envoi : "Alerte_capteur_ILS"
Auteur ...... : J.Serrand
Mail ........ : joris.serrand@rascol.net
Version ..... : V0.0 du 17/02/16
Licence ..... : Copyright (C) 2016  Joris SERRAND

                This program is free software: you can redistribute it and/or modify
                it under the terms of the GNU General Public License as published by
                the Free Software Foundation, either version 3 of the License, or
                (at your option) any later version.

                This program is distributed in the hope that it will be useful,
                but WITHOUT ANY WARRANTY; without even the implied warranty of
                MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
                GNU General Public License for more details.

                You should have received a copy of the GNU General Public License
                along with this program.  If not, see <http://www.gnu.org/licenses/>

Compilation . : Avec l'IDE Arduino
****************************************************************************************************/
```

## 2. Initialisations et déclarations de variables ou constantes

C'est dans cette partie que nous faisons les ajouts de bibliothèques nécessaires à l'exécution de notre code, ainsi que les déclarations et initialisations de variables et constantes. Même si le c++ autorise les déclarations n'importe où dans le programme, il est vivement conseillé de toutes les regrouper dans cette partie.

Voici un exemple de d'ajout de bibliothèques et de déclarations :

```c++
//Ajout de bibliothèques
#include <Wire.h> //Insertion de la bibliothèque pour les fonctions I2C

//Déclarations de constantes
#define bp 10 //Déclaration d'une constante appelée bp de valeur 10
const float pi(3.14); //Déclaration d'une constante de type float et de nom "pi" initialisée à 3.14

//Déclaration de variables
int cpt(0); //Déclaration d'un entier de nom "cpt" initialisé à 0
float vitesse(10.5); //Déclaration d'un flottant de nom "vitesse" initialisé à 10.5
```


## 3. Le paramétrage du programme setup()


La partie ``void setup()`` renferme le paramétrage nécessaire au fonctionnement du programme, on peut par exemple y trouver :

* Le ``pinMode()``, permettant de dire si une pin numérique est utilisée en entrée ou en sortie.
* Le ``Serial.begin()``, permettant de paramétrer la vitesse de transfert de l'UART.
* ...

!!! warning
    Ne pas commencer à écrire votre code dans cette partie, ``setup()`` ne doit contenir que le paramétrage et ne s'exécute qu'une seule fois lors du lancement du programme.

Voici un exemple de ``setup()`` :

```c++
void setup()
{
  Wire.begin();//Initialisation de la liaison I2C
  lcd.init(); //Initialisation du LCD
  pinMode(4, INPUT); //Paramétrage de la pin numérique 4 en entrée
  Serial.begin(9600); //Paramétrage de la vitesse du port série
}
```


## 4. Le programme principal loop()


La partie ``void loop()`` est le programme principal de votre code Arduino. Comme son nom l'indique écrire dans cette partie revient à écrire dans une boucle ``while(1)``, le programme est rebouclé sans fin.

Exemple de programme principal faisant clignoter la led 13 (led présente sur le circuit imprimé d'une carte Arduino UNO) :

```c++
void loop()
{
  digitalWrite(13, HIGH);   // Met la pin 13 au niveau haut, ce qui a pour effet d'allumer la led
  delay(1000);              // Attend une seconde
  digitalWrite(13, LOW);    // Met la pin 13 au niveau bas, ce qui a pour effet d'éteindre la led
  delay(1000);              // Attend une seconde
}
```
