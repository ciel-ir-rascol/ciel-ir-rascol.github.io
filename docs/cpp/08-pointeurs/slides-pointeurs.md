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
# ▶︎ C10 - Les pointeurs
>## Programmation C++
>### BTS CIEL Informatique et Réseaux
>### Lycée Louis Rascol, Albi
<br><br>
`Release : v1.0 (03.09.23)`
📧 [joris.serrand@rascol.net](mailto:joris.serrand@rascol.net)
🐙 [Github : ciel-ir-rascol/cpp-cours ](https://github.com/ciel-ir-rascol/cpp-cours)
![bg right:40% w:80%](assets/cppLogo.png)

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
>Mais, je ne peux pas utiliser la variable ou la fonction directement ?? 🤔
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

# Relation entre les pointeurs et les tableaux (Arrays)

- La valeur du nom d'un tableau correspond à l'adresse du premier élément dans le tableau
- La valeur d'un pointeur est une adresse
- Si un pointeur pointe sur la même case mémoire q'un élément d'un tableau alors on peut utiliser les 2 de manière interchangeable
```cpp
int notes[] {10,12,18}
cout << notes << endl; // 🖥️ 0x61ff10 -> Adresse 1ere case tableau
cout << *notes << endl; // 🖥️ 10 -> Contenu 1ere case tableau

int *notesPtr {notes}; // Pointeur pointant sur 1ere case tableau
cout << notesPtr << endl; // 🖥️ 0x61ff10 -> Adresse 1ere case tableau
cout << *notesPtr << endl; // 🖥️ 10 -> Contenu 1ere case tableau
```

---

# Relation entre les pointeurs et les tableaux (Arrays)
## Accéder aux cases d'un tableau, notation `[]`

```cpp
int notes[] {10,12,18}
int *notesPtr {notes}; // Pointeur pointant sur 1ere case tableau

cout << notesPtr[0] << endl; // 🖥️ 10 -> Contenu 1ere case tableau
cout << notesPtr[1] << endl; // 🖥️ 12 -> Contenu 2ème case tableau
cout << notesPtr[2] << endl; // 🖥️ 18 -> Contenu 3ème case tableau
```

---

# Relation entre les pointeurs et les tableaux (Arrays)
## Accéder aux cases d'un tableau, `*pointeur` déréférencement
```cpp
cout << notesPtr << endl; // 🖥️ 0x61ff10 -> Adresse 1ere case tableau
cout << (notesPtr + 1) << endl; // 🖥️ 0x61ff14 -> Adresse 2ème case tableau
cout << (notesPtr + 2) << endl; // 🖥️ 0x61ff18 -> Adresse 3ème case tableau

cout << *notesPtr << endl; // 🖥️ 10 -> Contenu 1ere case tableau
cout << *(notesPtr + 1) << endl; // 🖥️ 12 -> Contenu 2ème case tableau
cout << *(notesPtr + 2) << endl; // 🖥️ 18 -> Contenu 3ème case tableau
```

---

# Opérations mathématiques
## Incrémenter et décrémenter
```cpp
int tabEntiers[] {10,20,30};
int *ptrOnTab {tabEntiers};

cout << *ptrOnTab++ << endl;
//🖥️ 20 -> Contenu de la case mémoire du 2nd élément
cout << *ptrOnTab++ << endl;
//🖥️ 30 -> Contenu de la case mémoire du 3ème élément
cout << *ptrOnTab-- << endl;
//🖥️ 20 -> Contenu de la case mémoire du 2nd élément
cout << *ptrOnTab-- << endl;
//🖥️ 10 -> Contenu de la case mémoire du 1er élément
```

---

<!-- _class: lead -->
# Attribution de mémoire dynamique
# *Heap*

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
int *intPtr = nullptr;

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
## Utiliser `new type[]` pour allouer de l'espace pour un tableau
```cpp
int *tableauPtr = nullptr;
int taille = 0;

cout << "Donnez la taille de votre tableau ?";
cin >> taille;

tableauPtr = new int[taille]; // Réservation du tableau dans le tas
```

---

# Attribution de mémoire dynamique
## Utiliser `delete [] nom` pour libérer la mémoire réservée pour un tableau
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

<!-- _class: lead -->
# Fonctions et pointeurs

---
# Fonctions et pointeurs
## Passage par référence avec des pointeurs en paramètres
```cpp
void multiplierPar2(int *intPtr){
  // On multiplie le contenu de la case mémoire pointée par intPtr, par 2
  *intPtr = *intPtr * 2; 
}

int main(){
  int valeur {10};

  cout << valeur << endl; // 🖥️ 10
  
  multiplierPar2(&valeur); // On met en argument l'adresse de valeur
  
  cout << valeur << endl; // 🖥️ 20
}
```

---

# Fonctions et pointeurs
## Retourner un pointeur depuis une fonction
- Les fonctions peuvent aussi retourner des pointeurs :
```cpp
type *fonction();
```
- Les fonctions peuvent retourner des pointeurs :
  - Dans de la mémoire dynamique (heap) allouée depuis la fonction
  - Dans des données passées par paramètre
- ⚠️ **Ne jamais retourner un pointeur dans une variable locale à la fonction**

---

# Fonctions et pointeurs
## Exemple de retour par pointeur
▶︎ **Fonction `lePlusGrand`**
```cpp
int *lePlusGrand(int *ptrEntier1, int *ptrEntier2){
  if(*ptrEntier1 > *ptrEntier2)
    return ptrEntier1;
  else
    return ptrEntier2;
}
```

---

# Fonctions et pointeurs
## Exemple de retour par pointeur
▶︎ **Fonction principale**
```cpp
int main(){
  int a {100};
  int b {200};
  
  int *rslt{nullptr}; // On déclare un pointeur null sur un entier
  
  rslt = lePlusGrand(&a,&b); // La fonction retourne l'adresse du rslt
  cout << *rslt << endl; // 🖥️ 200
  
  return 0;
}
```

---

# Fonctions et pointeurs
## Exemple de retour d'adresse mémoire depuis le heap
▶︎ **Fonction `creerTableau`**
```cpp
int *creerTableau(int nbCases, int valeurInit){
  int *ptrTableau {nullptr};

  nouveauStockage = new int[nbCases]; // Réservation de nbCases dans le heap
  for(int i=0; i<nbCases; i++)
    *(ptrTableau + i) = valeurInit;

  return ptrTableau;
}
```

---

# Fonctions et pointeurs
## Exemple de retour d'adresse mémoire depuis le heap
**▶︎ Fonction principale**

```cpp
int main(){
  int *monTableau {nullptr};
  // Création d'un tableau dans le heap de 100 cases initialisées à 20
  monTableau = creerTableau(100,20)
  
  // On fait plein de choses avec ce beau tableau 😎

  delete [] monTableau; // ‼️ Indispensable !
  
  return 0;
}
```

---

# Fonctions et pointeurs
 ☠️ **À ne pas faire !**
```cpp
int *cEstPasBien(){
  int taille{};
  ...
  return &taille; // 🤯 taille est détruit en sortant de la fonction !!!
}

int *jeNeferaiJamaisCa(){
  int taille{};
  int ptrTaille{&taille};
  ...
  return ptrTaille; // 🤯 taille est détruit en sortant de la fonction !!!
}
```
**‼️ L'emplacement mémoire des variables locales est détruit en sortant des fonctions.**
