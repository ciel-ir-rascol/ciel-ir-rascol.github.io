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
# ▶︎ C05 - Structures sélectives
>## Programmation C++
>### BTS CIEL Informatique et Réseaux
>### Lycée Louis Rascol, Albi
<br><br>
`Release : v1.0 (11.10.23)`
📧 [joris.serrand@rascol.net](mailto:joris.serrand@rascol.net)
🖥️ Site Web : [ciel-ir-rascol.github.io](https://ciel-ir-rascol.github.io/)
🐙 GitHub : [ciel-ir-rascol](https://github.com/ciel-ir-rascol)
![bg right:40% w:80%](assets/cppLogo.png)

---
<!-- paginate: true --->
<!--
header: ▶︎ C05 - Structures sélectives
footer: Programmation C++ • Lycée Louis Rascol, Albi
-->

# Contrôler le flux d'exécution du programme

## Séquentiellement (Ce qu'on faisait jusqu'à présent)
- On ordonne de manière séquentielle les instructions, elles sont lues de haut en bas.
## Sélectivement (Avec des `if()`, des `switch() case`)
- Le programme prend une décision suite à une condition donnée, il choisit une voie ou une autre.
## Itérativement (Avec des boucles `while()`, `for()`)
- Le programme répète en boucle une suite d'instruction tant qu'une condition est vraie.


---

<!-- _class: lead -->
# Opérateurs Relationnels
# et 
# Logiques

---

# Opérateurs relationnels
L'écriture d'une condition nécessite souvent l'utilisation d'opérateurs pour tester l'égalité, l'infériorité, la différence ...


<div class="columns">
<div>
  
| Test | Opérateur |
|:---:|:---:|
| Égalité | `==`|
| Différence | `!=`|
| Infériorité | `<`|
| Supériorité | `>`|
| Infériorité ou Égalité | `<=`|
| Supériorité ou Égalité | `>=`|

</div>
<div>

‼️ **Ne confondez pas l'opérateur d'affection `=` et l'opérateur relationnel d'égalité `==`**

Exemple : 

```cpp
// Je teste si tutu est égal à 42
if (tutu == 42) 

// Je mets la valeur 42 dans tutu
tutu = 42;
```

</div>
</div>

---

# Opérateurs logiques
Pour *connecter* plusieurs conditions et former une condition complexe, on utilise des opérateurs logiques :
  
<div class="columns">
<div>

| Connexion logique | Opérateur |
|:---:|:---:| 
| not (inverse) | `!`|
| and (ET logique) | `&&` |
| or (OU logique) | `\|\|` |
    
</div>
<div>

  ℹ️ La barre verticale du OU logique `|` se trouve avec la combinaison `Alt Gr` + `6` sur un clavier Windows
  
  ℹ️ Le joli nom du symbole `&` est **esperluette** en français et **ampersand** en anglais.

</div>
</div>

---

<!-- _class: lead -->
# Structure sélective
# `if() else`

---

# Structure `if()`
```cpp
if(condition){
    // Instructions réalisées si condition VRAIE
    // instruction 1
    // instruction 2
}
// On saute la structure si condition FAUSSE
```
▶︎ Pour **une seule instruction** à exécuter les `{}` ne sont pas obligatoires :
```cpp
if(condition)
    // Instruction réalisée si condition VRAIE

// On saute la structure si condition FAUSSE
```
---

# Structure `if()`
▶︎ **Exemples**

```cpp
if (toto>=2 && toto<=5) 
    cout << "toto est compris entre 2 et 5" << endl;

if (toto!=20)
    cout << "toto est différent de 20" << endl;

if (!monBooleen)
    cout << "monBooleen est égal à false" << endl;
```

---

# Structure `if() else`
```cpp
if (condition){
    // Instructions à réaliser si condition est vraie
}
else {
    // Instructions à réaliser si condition est fausse
}
```
▶︎ Pour **une seule instruction** à exécuter les `{}` ne sont pas obligatoires :
```cpp
if(condition)
    // Instruction réalisée si condition VRAIE
else
    // Instruction à réaliser si condition est fausse
```

---

# Structure `if() else`
▶︎ **Exemples**
```cpp
if (toto%2==0) 
    cout << "toto est pair !" << endl;
else
    cout << "toto est impair !" << endl;


if (num >= 0)
    cout << "Num est positif" << endl;
else
    cout << "Num est négatif" << endl;
```

---

# Structures `if() else` imbriquées
La structure `if() else` peut s'imbriquer à l'infini :
```cpp
if(condition1){
    if(condition2){
        // Instructions si condition1 VRAIE et condition2 VRAIE
    }
    else {
        // Instructions si condition1 VRAIE et condition2 FAUSSE
    }
}
else{
        // Instructions si condition1 FAUSSE
}
```

---

# Structures `if() else` imbriquées
▶︎ Exemple, les trois états de l'eau :
```cpp
if (eau >= 100)
    cout << "C'est gazeux !" << endl;
else{
    if (eau > 0)
        cout << "C'est liquide !" << endl;
    else
        cout << "C'est solide !" << endl;
}
```

---

# Imbrication avec `else if()`
▶︎ Pour plus de compacité on peut utiliser `else if()` pour imbriquer :
```cpp
if (eau >= 100)
    cout << "C'est gazeux !" << endl;
else if (eau > 0)
    cout << "C'est liquide !" << endl;
else
    cout << "C'est solide !" << endl;

```

---

<!-- _class: lead -->
# Structure sélective
# `switch() case`

---

# Squelette de la structure

```cpp
switch(variableEntiere){
    case valeur1_variableEntiere : 
        // Instructions à réaliser
        break;
    case valeur2_variableEntiere : 
        // Instructions à réaliser
        break;
    default:
        // Instructions à réaliser si on ne rentre pas dans les
        // 2 cas précédents
}
```
‼️ **N'oubliez pas le `break` à la fin de chaque `case` sinon C++ exécutera toute les `case` suivants !**

---

# Exemple d'utilisation
<div class="columns">
<div>
▶︎ Affichage du menu principal du programme :

```cpp
int choix {0};

cout << "*** Menu Principal ***" << endl;
cout << " 1. Afficher Hello !" << endl;
cout << " 2. Afficher  I'm hungry !" << endl;
cout << " 3. Afficher  I'm thirsty !" << endl;

cin >> choix;
```

</div>
<div>

▶︎ Structure `switch() case` en fonction de la valeur de l'entier `choix` :

```cpp
switch(choix){
    case 1 : 
        cout << "Hello you !" << endl;
        break;
    case 2 : 
        cout << "I'm hungry !" << endl;
        break;
    case 3 :
        cout << "I'm thirsty !" << endl;
        break;
    default:
        cout << "CHOIX INCORRECT !" << endl;
}
```
</div>
</div>