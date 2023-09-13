---
search:
  exclude: true
marp: true
style: |
  .columns {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 1rem;
  }
---
<!-- _backgroundImage: url("assets/bgImage.jpg") -->
# ▶︎ C10 - Les pointeurs
>## Programmation C++
>### BTS CIEL 1ere année
>### Lycée Louis Rascol, Albi
<br><br>
`Release : v1.0 (03.09.23)`
📧 [joris.serrand@rascol.net](mailto:joris.serrand@rascol.net)
🐙 [Github : ciel-ir-rascol/cpp-cours ](https://github.com/ciel-ir-rascol/cpp-cours)
![bg right:45% w:400](assets/cppLogo.png)

---
<!-- paginate: true --->
<!--
header: ▶︎ C10 - Les pointeurs
footer: Programmation C++ • Lycée Louis Rascol, Albi
-->
# Qu'est ce qu'un pointeur ?
- Une **variable** dont la valeur est une **adresse**
- Qu'est ce qu'il y a à cette adresse ?
  - Une autre **variable**
  - Une **fonction**
- Si `x` est un entier contenant `10`, je peux déclarer un pointeur qui pointe sur la valeur de `x` → `10`

---

# Pourquoi utiliser des pointeurs ?
>Mais, je ne peux pas utiliser la variables ou la fonction directement ?? 🤔
> **Oui, mais pas dans toutes les situations**
- Dans les fonctions les pointeurs peuvent être utilisés pour accéder à des données définies or de la fonction.
- Les pointeurs peuvent être utilisés sur les tableaux de manière très efficiente.
- On peut allouer de la mémoire dans le tas (heap) :
  - Cette mémoire n'a même pas besoin d'un nom de variable.
  - La seule manière d'y accéder est avec un pointeur.

---

#  Déclarer des pointeurs
## Syntaxe
```cpp
type_variable *nom_pointeur;
```
## Exemple
```cpp
int *int_ptr; // Pointeur sur un entier
double *double_ptr; // Pointeur sur un double
char *char_ptr; // Pointeur sur un char
string *string_ptr; // Pointeur sur une chaîne de caractères
```
‼️ **Un pointeur prend le type de la variable sur lequel il pointe**

---
# Initialiser les pointeurs
▶︎ Un pointeur non initialisé **pointe vers des données indéterminées** en mémoire : **Il faut absolument éviter ça !**
## Syntaxe
```cpp
variable_type *nom_pointeur = nullptr; // Pointeur initialisé pointant nulle part
```
## Exemple
```cpp
int *int_ptr = nullptr; 
double *double_ptr = nullptr;
```
‼️ **Initialisez toujours vos pointeurs**

---

# Accéder à l'adresse d'une variable
- Utilisation de l'opérateur `&`
- Les variables sont stockées sous forme d'une unique adresse
```cpp
int num=10;

cout << "La valeur de num est : " << num << endl; 
//🖥️ La valeur de num est 10

cout << "La taille de num est : " << sizeof num << endl;
//🖥️ La taille de num est 4 → 4 octets

cout << "L'adresse de num est : " << &num << endl; 
//🖥️ L'adresse de num est 0x61ff1c
```
---

# Accéder à l'adresse d'un pointeur
## Exemple
```cpp
int *ptr;

cout << "La valeur de ptr est : " << ptr << endl; 
//🖥️ La valeur de num est Ox61ff60 → Données indéterminées

cout << "La taille de ptr est : " << sizeof ptr << endl;
//🖥️ La taille de ptr est 8 → 8 octets

cout << "L'adresse de ptr est : " << &ptr << endl;
//🖥️ L'adresse de ptr est 0x61ff18

ptr = nullptr; // On fait pointer ptr nulle part
cout << "La valeur de ptr est : " << ptr << endl; 
//🖥️ La valeur de ptr est 0
```

---

# Taille d'un pointeur
**⚠️ La taille d'un pointeur ≠ taille de la variable sur laquelle il pointe**
**‼️ Dans une programme tous les pointeurs on la même taille**
## Exemple
```cpp {1-2}
int *p1 = nullptr;
double *p2 = nullptr;
string *p3 = nullptr;

cout << sizeof p1 <<","<< sizeof p2 <<","<< sizeof p3;
//🖥️ 8,8,8
```
▶︎ Peut importe la taille de la variable, sur une machine moderne (x64), un **pointeur aura toujours une taille de 8 octets**.

---

# Type d'un pointeur
**‼️ Le compilateur vérifie que l'adresse stockée par un pointeur est du bon type**
## Exemple
```cpp
int score = 10;
double temp = 100.8;

int *scorePtr = nullptr;
scorePtr = &score; // 🟢 scorePtr reçoit l'adresse de score
scorePtr = &temp; // 🔴 ERREUR du compilateur
```

---

# Déréférencement de pointeurs
ℹ️ Déréférencement → Obtenir la valeur à laquelle un pointeur pointe
On peut accéder aux données à l'adresse pointée par le pointeur avec l'opérateur `*`
## Exemple
```cpp
int score = 100;
int *scorePtr = &score; //scorePtr reçoit l'adresse de score

cout << *scorePtr << endl; // 🖥️ 100

*score_prt = 200; // Changement du contenu de ptr : ptr←200
cout << *scorePtr << endl; // 🖥️ 200
cout << score << endl; // 🖥️ 200
```
‼️ **Opérateur `*` utilisé pour déclaration et init ptr et aussi déréférencement**

---

# Déréférencement de pointeurs
## Autre exemple
```cpp
double hauteTemp = 100.7;
double basseTemp = 37.4;
double *tempPtr = &hauteTemp; // tempPtr initialisé à l'adresse de hauteTemp

cout << *tempPtr << endl; // 🖥️ 100.7

tempPtr = &basseTemp; // tempPtr reçoit l'adresse de basseTemp

cout << *tempPtr << endl; // 🖥️ 37.4

```

---

# Déréférencement de pointeurs
## Un dernier exemple
```cpp
string name = "Richard";

string *stringPtr = &name; // stringPtr est initialisé à l'adresse de name

cout << *stringPtr << endl; // 🖥️ Richard

name = "Dinesh"; // On change le contenu de name : name ← "Dinesh" 

cout << *stringPtr << endl; // 🖥️ Dinesh
```
---

# Attribution de mémoire dynamique
## Pourquoi réserver de la mémoire dans le tas (heap) ?
‼️ **Le tas (heap) ≠ La pile (stack)**
`int unEntier = 22;` → 22 est stocké dans la pile !
- Nous ne savons souvent pas combien d'espace de stockage nous avons besoin jusqu'à ce que nous en ayons besoin.
- On peut allouer de l'espace de stockage pour une variable durant l'exécution
- Utile pour les tableaux qui normalement nécessitent une déclaration de la taille lors de la déclaration
- **On se sert des pointeurs pour accéder à l'espace mémoire réservé dans le tas.**

---

# Attribution de mémoire dynamique
## Utilisation de `new` pour réserver de l'espace
```cpp
int intPtr = nullptr;

intPtr = new int; // Réservation d'un entier dans le tas

cout << intPtr << endl; // 🖥️ Ox1252f21

cout << *intPtr << endl; // 🖥️ 23879977 → Données indéterminées

*intPtr = 42;

cout << *intPtr << endl; // 🖥️ 42
```

---
# Attribution de mémoire dynamique
## Libération de la mémoire réservée `delete`
```cpp
int *intPtr = nullptr;
intPtr = new int; // Réservation d'un entier dans le tas

...// On fait plein de trucs trop 😎 avec intPtr

delete intPtr; // Libération de l'espace réservé dans le tas
```
**‼️ Il est important de penser à libérer l'espace utilisé, ce n'est pas automatique**

---

# Attribution de mémoire dynamique
## Utiliser `new []` pour allouer de l'espace pour un tableau
```cpp
int *tableauPtr = nullptr;
int taille = 0;

cout << "Donnez la taille de votre tableau ?";
cin >> taille;

tableauPtr = new int[taille]; // Réservation du tableau dans le tas
```

---

# Attribution de mémoire dynamique
## Utiliser `delete []` pour libérer la mémoire réservée pour un tableau
```cpp
int *tableauPtr = nullptr;
int taille = 0;

cout << "Donnez la taille de votre tableau ?";
cin >> taille;
tableauPtr = new int[taille]; // Réservation du tableau dans le tas

... // On fait des 👍 trucs avec le tableau dans le tas

delete [] tableauPtr // Libération de l'espace mémoire dans le tas

```

---

TODO : Avant de poursuivre revenir sur les vidéos précédente et créer un projet CLion pointeur à utiliser en cours et pour le screencast.

