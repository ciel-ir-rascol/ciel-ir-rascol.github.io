---
search:
    exclude: true
marp: true
style: |
    .columns {
        display: grid;
        grid-template-columns: repeat(2, minmax(0, 1fr));
        gap: 1rem;
    },
    section.lead h1 {
    text-align: center;
    font-size: 250%
    }

---
<!-- _backgroundImage: url("assets/bgImage.jpg") -->
# ▶︎ C07 - Fonctions
>## Programmation C++
>### BTS CIEL Informatique et Réseaux
>### Lycée Louis Rascol, Albi
<br><br>
`Release : v1.0 (10.12.24)`
📧 [joris.serrand@rascol.net](mailto:joris.serrand@rascol.net)
🖥️ Site Web : [ciel-ir-rascol.github.io](https://ciel-ir-rascol.github.io/)
🐙 GitHub : [ciel-ir-rascol](https://github.com/ciel-ir-rascol)
![bg right:40% w:80%](assets/cppLogo.png)

---
<!-- paginate: true --->
<!--
header: ▶︎ C07 - Fonctions
footer: Programmation C++ • Lycée Louis Rascol, Albi
-->

<!-- _class: lead -->

# Introduction

___

# Qu'est ce qu'une fonction ?
## Fonctions C++
- Issues de la STL *Standard Template Libraries*
- Issues d'autres librairies ajoutées manuellement
- Vos propres fonctions

## Modularité d'un programme
- Séparer le code dans des unités logiques compartimentées
- Ces unités peuvent être réutilisées 
___

# Exemple : Calcul d'une puissance
```cpp
int main()
{
    int nb{0},puiss{0}, rslt{1};
    cout << "Donnez le nombre suivi de la puissance :";
    cin >> nb >> puiss;

    for(int i{0};i<puiss;i++)
        rslt*=nb;

    cout << nb << "^" << puiss << "=" << rslt;
}
```
___

# Exemple : Calcul d'une puissance, `math.h` library
```cpp
#include <math.h> // Bibliothèque math.h pour utiliser la fonction pow()

int main()
{
    int nb{0},puiss{0}, rslt{1};
    cout << "Donnez le nombre suivi de la puissance :";
    cin >> nb >> puiss;

    rslt=pow(nb,puiss); // Utilisation de la fonction pow()

    cout << nb << "^" << puiss << "=" << rslt;
}
```
___

# Exemple : Calcul d'une puissance, fonction perso
```cpp
// Création de la fonction puissance
int puissance(int a, int b)
{
    int c{1};
    for(int i{0};i<b;i++)
        c*=a;
    return c;
}

int main()
{
    int nb{0},puiss{0}, rslt{1};
    cout << "Donnez le nombre suivi de la puissance :";
    cin >> nb >> puiss;
    rslt=puissance(nb,puiss); // Appel de la fonction puissance
    cout << nb << "^" << puiss << "=" << rslt;
}
```
___

<!-- _class: lead -->

# Variables Locales <br> vs <br>Variables Globales

___

# Variable locale vs Variable globale
## Variable globale
- Déclarée en dehors de toute fonction (y compris la fonction `main()`)
- Accessible n'importe où dans le fichier
- ⚠️ **Peut être dangereux car pas de cloisonnement**
- Les fonctions faisant référence à des variables globales sont difficilement exportables. 

___

# Exemple : Utilisation d'une variable globale
```cpp
#include <iostream>
using namespace std;

int nb{0},puiss{0}, rslt{1}; // Déclaration des variables globales

void puissance()
{
    for(int i{0};i<puiss;i++)
        rslt*=nb;
}
int main()
{
    cout << "Donnez le nombre suivi de la puissance :";
    cin >> nb >> puiss;
    puissance();
    cout << nb << "^" << puiss << "=" << rslt;
}
```

___

# Variable locale vs Variable globale
## Variable locale
- Déclarée dans une fonction
- **A une existence seulement dans la fonction où elle a été déclarée**
- Cloisonnement des données entre les fonctions
- Facilite l'export et la réutilisation des fonctions créées.

___

# Exemple : Variable locale
```cpp
int puissance(int a, int b) // a, b et c sont locales
// ⚠️ a, b et c n'existent que dans puissance()
{
    int c{1};
    for(int i{0};i<b;i++)
        c*=a;
    return c;
}
int main()
{
    int nb{0},puiss{0}, rslt{1}; // nb, puiss, rslt sont locales
    // ⚠️ nb, puiss et rslt n'existent que dans main()
    cout << "Donnez le nombre suivi de la puissance :";
    cin >> nb >> puiss;
    rslt=puissance(nb,puiss); // Appel de la fonction puissance
    cout << nb << "^" << puiss << "=" << rslt;
}
```
___

<!-- _class: lead -->

# Déclaration d'une fonction

___

# Prototype d'une fonction
- Avec valeur de retour
```cpp
type_valeur_retour nom_fonction (parametres){
    
    // Contenu_fonction

    return valeur_a_retourner;
}
```

- Fonction sans valeur de retour (aussi appelé *procédure*)
```cpp
void nom_fonction (parametres){
    
   // Contenu_fonction

}
```

___

# Exemple de déclaration de fonction

- Avec valeur de retour
```cpp
int addition(int a, int b){
    return a+b;
}
```
- Sans valeur de retour
```cpp
void coucou(string nom){
    cout << "Coucou " << nom << " !" << endl;
}
```
___

<!-- _class: lead -->

# Appel d'une fonction

___

# Appel d'une fonction
- Sans valeur de retour
```cpp
nom_fonction(arguments);
nom_fonction(); // Pour une fonction sans argument
```
- Avec valeur de retour
```cpp
// Stockage de la valeur renvoyée par la fonction dans la variable var
var = nom_fonction(arguments);
// Affichage de la valeur renvoyée par la fonction
cout << nom_fonction(arguments);
```
⚠️ Dans le premier cas `var` **doit être du même type** que la valeur de retour de la fonction

___

# Exemple : Appel d'une fonction sans valeur de retour

```cpp
// Déclaration de la fonction
void coucou(string nom){
    cout << "Coucou " << nom << " !" << endl;
}

int main(){
    string nomUtilisateur;
    cout << "Rentrez votre nom :" << endl;
    getline(cin,nomUtilisateur); 

    coucou(nomUtilisateur); // Appel de la fonction

    return 0;
}
```
___

# Exemple : Appel d'une fonction avec valeur de retour
```cpp
// Déclaration de la fonction
int addition(int a, int b){
    return a+b;
}

int main(){
    int a{0}, b{0}, rslt{0};
    cout << "Rentrez 2 entiers : ";
    cin >> a >> b;

    rslt=addition(a,b);
    cout << rslt << endl;

    return 0;
}
```
___

<!-- _class: lead -->

# Retour de valeur par référence

___

# Retour de valeur par référence
- Dans une fonction possibilité de retourner qu'une seule valeur avec `return`
- Pour retourner plusieurs valeurs : 
  - Passage par références
  - Passage par pointeurs (cours suivant...)
- Passage par référence : Modification directe des variables passées par argument.

___

# Déclaration d'une fonction avec retour par référence
```cpp
void nom_fonction(type &var){
    // Contenu de la fonction
}
```

- L'opérateur `&` permet d'**obtenir l'adresse de la case mémoire** de la variable passée en argument.
- La fonction **agira directement sur le contenu** de cette case mémoire.

___

# Exemple retour par référence
```cpp
void addition(int a, int b, int &result) { // result est passé par référence
    result = a + b;
}

int main() {
    int x = 5, y = 10, sum = 0;
    addition(x, y, sum);
    // Aprés l'appel de la fonction le résultat est dans result
    cout << "La somme est : " << sum << endl;
    return 0;
}
```

___
<!-- _class: lead -->
# Surcharge de fonctions
# *Overloaded Functions*

___

# Overloaded Functions
- On peut avoir des fonctions qui peuvent avoir différents paramètres et toujours le même nom.
- Un type de polymorphisme :
  - Le même nom de fonction peut être utilisé avec des différents types de données pour exécuter quelque chose de similaire.
- Le compilateur doit être capable de faire la distinction entre les fonctions à utiliser, suivant la liste des paramètres et les arguments fournis.

___

# Exemple : Overloaded Functions

```cpp
int add_numbers(int a, int b){ // Fonction 1
    return a+b;
}
double add_numbers(double a, double b){ // Fonction 2
    return a+b;
} 

int main(){
    cout << add_numbers(10,20) << endl; // Appel de la fonction 1 car ENTIERS
    cout << add_numbers(10.0,20.0) << endl; // Appel de la fonction 2 car DÉCIMAUX
}
```





<!-- Mettre une partie retour par argument ->