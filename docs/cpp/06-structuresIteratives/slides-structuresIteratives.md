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
# ▶︎ C06 - Structures itératives
>## Programmation C++
>### BTS CIEL Informatique et Réseaux
>### Lycée Louis Rascol, Albi
<br><br>
`Release : v1.0 (18.10.23)`
📧 [joris.serrand@rascol.net](mailto:joris.serrand@rascol.net)
🖥️ Site Web : [ciel-ir-rascol.github.io](https://ciel-ir-rascol.github.io/)
🐙 GitHub : [ciel-ir-rascol](https://github.com/ciel-ir-rascol)
![bg right:40% w:80%](assets/cppLogo.png)

---

<!-- paginate: true --->
<!--
header: ▶︎ C06 - Structures itératives
footer: Programmation C++ • Lycée Louis Rascol, Albi
-->

# Répéter en boucle 🔁
- C'est la 3ème structure basique en programmation :
  - Séquence, sélection et **itération**.
- On dit itération ou répétition.
- Permet la répétition d'une instruction ou d'un bloc d'instructions.
- Le nombre de répétition est défini par une condition.

---

# Types de boucles en C++
- La boucle `for`
  - Itère un nombre de fois donné
- La boucle range-based `for`
  - Permet d'itérer sur chaque élément d'une plage.
- La boucle `while`
  - Itère tant qu'une condition est vraie
  - Sort de la boucle quand la condition est fausse
  - Teste la condition à chaque début d'itération
- La boucle `do while`
  - Pareil que la `while`
  - Teste la condition à la fin de chaque itération

---

<!-- _class: lead -->
# La boucle `for`

---

# Structure d'une boucle `for`

```cpp
for(declaration et init; condition; pas de comptage)
    // Pour une seule instruction

for(declaration et init; condition; pas de comptage){
    // ...
    // Pour plusieurs instructions
    // ...
}
```

---

# Exemple avec une instruction

▶︎ Affichage de la variable de comptage
```cpp
for (int i{0}; i<5; i++)
    cout << i << endl;

/* 🖥️ SORTIE CONSOLE
0
1
2
3
4 */
```
ℹ️ Par convention le variable de comptage (souvent `i`ou `j`) est **toujours déclarée dans la boucle** `for`

![bg right:40% w:60%](assets/diagFor.svg)
    

---

# Exemple avec bloc d'instructions
▶︎ Affichage des entiers pairs entre 0 et 10
```cpp
for (int i{1}; i<=10; i++){
    if (i%2 == 0)
        cout << i << endl;
}

/* 🖥️ SORTIE CONSOLE
2
4
6
8
10 */
```
![bg right:40% w:70%](assets/diagFor2.svg)

---

# Exemple avec parcours d'un tableau
▶︎ Parcourir les 3 cases du tableau `tab`
```cpp
int tab [] {42,52,62};

for (int i{0}; i<3; i++)
    cout << tab[i] << endl;

/* 🖥️ SORTIE CONSOLE
42
52
62 */
```

---

<!-- _class: lead -->
# La boucle `for` range-based

---

# Structure d'une boucle `for` range-based
```cpp
for (declaration_element : sequence)
    // Pour une seule instruction

for (declaration_element : sequence){
    // ...
    // Pour plusieurs instructions
    // ...
}
```

---

# Exemple parcours d'un tableau
▶︎ Parcours d'un tableau d'entiers par élément avec une range-base `for`

<div class="columns">
<div>

```cpp
int tab [] {42,52,62};

for (int nombre : tab)
    cout << nombre << endl;

/* 🖥️ SORTIE CONSOLE
42
52
62 */
```
    
</div>
<div>
    
```cpp
int tab [] {42,52,62};

// Avec auto pas besoin du type !
for (auto nombre : tab)
    cout << nombre << endl;

/* 🖥️ SORTIE CONSOLE
42
52
62 */
```

</div>
</div>

---

# Exemple parcours d'un vecteur
▶︎ Parcours d'un vecteur de flottants avec une range-base `for` et calcul de la moyenne de ces éléments

<div class="columns">
<div>
    
```cpp
vector<float> temps {20.3, 12.6, 5.7, 10.1};

float temps_moyenne {0};
float temps_somme {0};

for (auto temp : temps)
    temps_somme += temp;

temps_moyenne = temps_somme / temps.size();
```

</div>
<div>

```cpp
float temps_moyenne {0};
float temps_somme {0};
int size {0};

// Ici on met le vecteur dans le for
for (auto temp : {20.3, 12.6, 5.7, 10.1}){
    temps_somme += temp;
    size ++;
}

temps_moyenne = temps_somme / size;
```

</div>
</div>

---

# Exemple parcours d'une chaîne de caractère
```cpp
for (auto c : "Banane")
    cout << c << endl;

/* 🖥️ SORTIE CONSOLE
B
a
n
a
n
e */
```

---

<!-- _class: lead -->
# La boucle `while`

---

# Structure d'une boucle `while`
```cpp
while (condition)
    // instruction

while (condition){
    // ...
    // instructions
    // ...
}
```
ℹ️ N'importe quelle structure codée avec une boucle `for` peut être codée avec une `while`

---

# Exemple simple
▶︎ Nous reprenons l'exemple précédent codé avec une boucle `for`, en utilisant cette fois une `while` :

```cpp
int i{0};

while (i < 5){
    cout << i << endl;
    i++ ; // ‼️ Attention à bien incrémenter !
}

/* 🖥️ SORTIE CONSOLE
0
1
2
3
4 */
```
![bg right:35% w:70%](assets/diagFor.svg)

---

# Exemple avec bloc d'instructions
▶︎ Idem même exemple mais avec une `while` :
```cpp
int i{1};
while (i<=10){
    if (i%2 == 0)
        cout << i << endl;
    i++;
}

/* 🖥️ SORTIE CONSOLE
2
4
6
8
10 */
```
![bg right:40% w:70%](assets/diagFor2.svg)

---

# Exemple avec parcours d'un tableau
▶︎ Toujours le même exemple que précédemment mais avec une `while` :
```cpp
int tab [] {42,52,62};
int i{0};

while (i<3){
    cout << tab[i] << endl;
    i++;
}

/* 🖥️ SORTIE CONSOLE
42
52
62 */
```

---

# Exemple validation d'une saisie
▶︎ Dans cette exemple on demande à l'utilisateur de saisir un nombre tant que la condition de saisie est fausse.

```cpp
int number{0};
cout << "Entrez un entier, plus petit que 100" << endl;
cin >> number;

while (number >= 100){
    cout << "Inférieur à 100 on a dit ! Réessaye ! " << endl;
    cin >> number;
}

cout >> "Thank you !" >> endl;
```

---

# Exemple d'utilisation d'un `flag`
▶︎ L'utilisation des flags est très courante, c'est un booléen qui permet d'arrêter le rebouclage quand il vaut `false`.
```cpp
bool flag {true};
int number {0};

    while(flag){
        cout << "Entrez un nombre entre 1 et 5 : ";
        cin >> number;
        if(number <= 1 || number >= 5)
            cout << "Entre 1 et 5 on a dit ! Réessaye !" << endl;
        else {
            cout << "Thank you !" << endl;
            flag = false;
        }
    }
```

---

<!-- _class: lead -->
# La boucle `do while`

---

# Structure d'une boucle `do while`
```cpp
do{
    //...
    // Instructions
    // ...
}while(condition);
```
ℹ️ Cette fois-ci la **condition est vérifiée en fin de boucle** et non au début comme avec la `while`

‼️ Pour ce type de boucle, peu importe le nombre d'instructions, **les accolades `{}` sont obligatoires !**

---

# Exemple validation d'une saisie
▶︎ Même exemple que précédemment mais avec une `do while`

```cpp
int number{0};

do{
    cout << "Entrez un entier, entre 1 et 5 : ";
    cin >> number;
}while(number <= 1 || number >= 5);

cout >> "Thank you !" >> endl;
```

ℹ️ La structure est plus compacte qu'avec une boucle `while`, on ne doit pas répéter le `cin` 2 fois.

![bg right:35% w:65%](assets/diagDoWhile.svg)

---

# Exemple calcul d'une aire
▶︎ Ce code calcule une aire tant que l'utilisateur répond `y` ou `Y` à la question finale.
```cpp
char choix{};

do{
    float largeur{}, hauteur{};
    cout << "Entrez largeur et hauteur :";
    cin >> largeur >> hauteur;

    cout << "l'aire est" << {largeur * hauteur} << endl;
    cout << "Voulez-vous en calculer une autre ? (Y/N) : ";
    cin >> choix;
}while (choix == 'Y' || choix == 'y');

cout << "Thank you !" << endl;
```

---

<!-- _class: lead -->
# Directives `continue` et `break`

---

# À quoi ça sert ? 🤔

- `continue`
  - Dès que le mot clé apparaît, plus aucune instruction est exécutée dans la boucle.
  - Le flux d'exécution se dirige immédiatement au début de la boucle pour l'itération suivante.
- `break`
  - Dès que le mot clé apparaît, plus aucune instruction est exécutée dans la boucle.
  - La boucle se termine immédiatement.
  - Le flux d'exécution se dirige immédiatement vers les instructions après la boucle.

---

# Exemple
▶︎ Exemple de parcours d'un vecteur `break` et `continue` sont utilisés dans un `if`
```cpp
vector<int> valeurs {1,2,-1,3,-1,-99,7,8,10};

for (auto elem : valeurs) {
    if (elem == -99)
        break;
    else if (elem == -1)
        continue;
    else
        cout << elem << endl;
}

/* 🖥️ SORTIE CONSOLE
1
2
3 */
```

---

<!-- _class: lead -->
# Boucles imbriquées

---

# Exemple parcours et affichage d'un tableau
```cpp
int tab[4][4]{
    {1,2,3},
    {10,11,12},
    {20,21,22}
};

for (int i{0}; i < 4; i++){ // Boucle des lignes
    for (int j{0}; j< 4; j++){ // Boucles des colonnes
        cout << tab[i][j] << " ";
    }
    cout << endl; // Retour à la ligne en fin de ligne du tableau
}

/* 🖥️ SORTIE CONSOLE
1 2 3
10 11 12
20 21 22 */
```