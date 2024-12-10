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
# ▶︎ C12 - Constructeurs et Destructeurs
>## Programmation C++
>### BTS CIEL Informatique et Réseaux
>### Lycée Louis Rascol, Albi
<br><br>
`Release : v1.0 (12.10.23)`
📧 [joris.serrand@rascol.net](mailto:joris.serrand@rascol.net)
🖥️ Site Web : [ciel-ir-rascol.github.io](https://ciel-ir-rascol.github.io/)
🐙 GitHub : [ciel-ir-rascol](https://github.com/ciel-ir-rascol)
![bg right:40% w:80%](assets/cppLogo.png)

---
<!-- paginate: true --->
<!--
header: ▶︎ C12 - Constructeurs et Destructeurs
footer: Programmation C++ • Lycée Louis Rascol, Albi
-->

<!-- _class: lead -->
# Déclarer des constructeurs et destructeurs

---

# Qu'est ce que c'est un constructeur ? 🤔
- Ce sont des méthodes de la classe sans type de `return` spécifié (pas de `void` non plus)
- Utilisés essentiellement pour l'**initialisation des attributs de la classe**.
- Ils ont le **même nom que la classe**
- Ils peuvent être overloadés
- Si aucun constructeur n'est prévu, C++ fourni **automatiquement un constructeur vide** pour la classe.

---

# Déclaration d'un constructeur

▶︎ Exemple classe `Personnage` 🧙
```cpp
class Personnage{
private :
    string nom;
    int vie;
    int attaque;
    int defense;
public :
    // Overloaded Constructors
    // Le constructeur par défaut
    Personnage(); 
    // Un constructeur pour initialiser l'attribut nom
    Personnage(string nomVal); 
    // Un constructeur pour initialiser tous les attributs
    Personnage(string nomVal, int vieVal, int attaqueVal, int defenseVal); 
};
```

---

# Qu'est ce que c'est un destructeur ? 🤔
- C'est une **méthode de la classe sans type de `return` et sans paramètres**.
- Il a le **même nom que le classe** précédé d'un `~` 
- Il est **appelé automatiquement quand un objet est détruit**
- Uniquement **1 destructeur par classe**, pas d'overload
- Utilisé essentiellement pour **libérer la mémoire et les autres ressources**
- **Appelé automatiquement** quand un objet local est *out of scope* (càd or du couple `{}` dans lequel il a été créé) ou qu'on détruit un pointeur sur un objet `delete`
- Si aucun destructeur n'est prévu, C++ fourni automatiquement un destructeur vide pour la classe.

---

# Déclaration d'un destructeur

▶︎ Exemple classe `Personnage` 🧙
```cpp
class Personnage{
private :
    string nom;
    int vie;
    int attaque;
    int defense;
public :
    // Les constructeurs
    Personnage();
    Personnage(string nomVal); 
    Personnage(string nomVal, int vieVal, int attaqueVal, int defenseVal); 
    
    // Le destructeur
    ~Personnage();
};
```

---

# Instanciation avec constructeurs et destructeur
▶︎ Exemple d'instanciation de la classe `Personnage` 🧙
```cpp
int main (void){
    // Creation d'arthur avec constructeur par défaut
    Personnage arthur;

    // Creation de perceval avec 2nd constructeur
    Personnage perceval {"Perceval"};

    // Creation de karadoc avec le 2ème constructeur
    Personnage karadoc {"Karadoc", 100, 1, 1};

} // Fin du main les 3 destructeurs sont appelés
  // Celui d'arthur, de perceval et de karadoc  
```

---

# Instanciation avec constructeurs et destructeur
▶︎ Un autre exemple avec un pointeur sur un objet
```cpp
int main (void){
    
    // Creation de guenievre dans le heap avec 3ème constructeur
    Personnage *guenievre = new Personnage {"Guenievre",100,3,3};
    
    delete guenievre; // Appel du destructeur de guenievre lors du delete
}
```

---

<!-- _class: lead -->
# Le constructeur par défaut

---

# C'est quoi le constructeur par défaut ? 🤨
- Il n'a **pas de paramètres** (parfois appelé *no-args constructor*)
- Si **aucun constructeur n'est précisé dans la classe, C++ le génère par défaut**
- Appelé quand un nouvel objet est instancié sans aucun arguments.

---

# Implémentation d'un constructeur par défaut
▶︎ Constructeur par défaut pour la classe `Personnage` 🧙
```cpp
class Personnage{
private :
    string nom;
    int vie;
    int attaque;
    int defense;
public :
    // Implémentation du constructeur par défaut
    Personnage(){
        nom = "";
        vie = 100;
        attaque = 5;
        defense = 5;
    };   
};
```

---

# Instanciation avec constructeur par défaut
▶︎ Exemple d'instantiation de la classe `Personnage` 🧙

```cpp
int main(){
    // Création de lancelot avec le constructeur par défaut
    Personnage lancelot;
}
```
Dans cet exemple `lancelot` aura donc :
- Le nom ` `
- `100` points de vie
- `5` points d'attaque
- `5` points de défense

----

<!-- _class: lead -->
# Implémenter les constructeurs

---

# Principes d'implémentation
- On peut créer autant de constructeurs qu'on veut.
- Chaque constructeur doit **avoir une signature unique** :
  - Les paramètres du constructeur lors de sa déclaration **doivent être distincts**
- Une fois qu'un constructeur est créé le compilateur ne créera plus de constructeur par défaut automatiquement.

---

# Exemples d'implémentation
▶︎ Exemple classe `Personnage` déclarations 
```cpp
class Personnage{
private :
    string nom;
    int vie;
    int attaque;
    int defense;
public :
    // Déclaration des constructeurs
    Personnage();
    Personnage(string nomVal); 
    Personnage(string nomVal, int vieVal, int attaqueVal, int defenseVal);   
};
```

---

# Exemples d'implémentation
▶︎ Exemple classe `Personnage` implémentations

<div class="columns">
<div>

```cpp
// Implémentation du constructeur par défaut
Personnage::Personnage(){
    nom = "";
    vie = 100;
    attaque = 5;
    defense = 5;
}

// Implémentation du 2nd constructeur
Personnage::Personnage(string nomVal){
    nom = nomVal;
    vie = 100;
    attaque = 5;
    defense = 5;
}
```
    
</div>
<div>

```cpp
// Implémentation du dernier constructeur
Personnage::Personnage(string nomVal, 
int vieVal, int attaqueVal, int defenseVal){
    nom = nomVal;
    vie = vieVal;
    attaque = attaqueVal;
    defense = defenseVal;
}
```

</div>
</div>

---

<!-- _class: lead -->
# Liste d'initialisation de constructeurs
# *Constructor Initialization List*

---

# Pourquoi utiliser une liste d'initialisation ? 🤨
- Jusqu'à présent on initialisait les attributs dans le constructeur.
- Les listes d'initialisation de constructeurs :
  - Sont plus efficaces
  - Suivent immédiatement la liste de paramètres
  - Initialise les attributs quand l'objet est créé
  - L'ordre d'initialisation est l'ordre de déclaration dans la classe

---

# Exemple d'utilisation
▶︎ On implémente les constructeurs de la classe `Personnage` précédente :

```cpp
// Implémentation du constructeur par défaut
Personnage::Personnage()
    : nom {""},vie {100}, attaque {5}, defense {5}{
    }

// Implémentation du 2nd constructeur
Personnage::Personnage(string nomVal) 
    : nom {nomVal},vie {100}, attaque {5}, defense {5}{
}

// Implémentation du dernier constructeur
Personnage::Personnage(string nomVal, int vieVal, int attaqueVal, int defenseVal)
    : nom {nomVal},vie {vieVal}, attaque {attaqueVal}, defense {defenseVal}{
    }
```

---

<!-- _class: lead -->
# Déléguer les constructeurs
# *Constructor Delegation*

---

# Pourquoi déléguer les constructeurs ? 🤔
- Parfois le code dans les constructeurs est similaire
- Faire du copier-coller peux produire des erreurs
- C++ autorise la délégation des constructeurs :
  - Le code pour un constructeur peut appeler un autre constructeur dans la liste d'initialisation

---

# Exemple d'utilisation
▶︎ En se servant à nouveau de la classe `Personnage` précédente :
```cpp
// Implémentation du dernier constructeur celui avec tous les attributs
Personnage::Personnage(string nomVal, int vieVal, int attaqueVal, int defenseVal)
    : nom {nomVal},vie {vieVal}, attaque {attaqueVal}, defense {defenseVal}{
    }

// Implémentation du constructeur par défaut par délégation
Personnage::Personnage()
    : Personnage {"",100,5,5}{
    }

// Implémentation du 2nd constructeur par délégation
Personnage::Personnage(string nomVal) 
    : Personnage {nomVal,100,5,5} {
}
```

---

<!-- _class: lead -->
# Valeurs par défaut du constructeur

---

# Pourquoi ça peut être utile ?

- Peut parfois simplifier le code 
- Permet de réduire le nombre de constructeurs overloaded
- Dans la déclaration de la classe, on met un constructeur avec les valeurs des paramètres par défaut
- On déclare implémente ensuite un constructeur, un seul sera nécessaire.
- Lors de l’instanciation de la classe quand un argument n'est pas renseigné c'est la valeur par défaut du paramètre qui sera donnée.

---

# Mise en oeuvre
▶︎ Reprenons à nouveau la classe `Personnage`:

```cpp
class Personnage{
private :
    string nom;
    int vie;
    int attaque;
    int defense;
public :
    // Déclaration du constructeur avec initialisations
    Personnage(string nomVal="", int vieVal=100, int attaqueVal=5, int defenseVal=5);   
};

// Implémentation du constructeur
Personnage::Personnage(string nomVal, int vieVal, int attaqueVal, int defenseVal)
    : nom {nomVal},vie {vieVal}, attaque {attaqueVal}, defense {defenseVal}{
    }
```

---

<!-- _class: lead -->
# Le pointeur `this`

---

# C'est quoi un pointeur `this` ? 🤔
- `this` est un mot clé, réservé.
- Il contient l'adresse de l'objet, donc c'est un **pointeur sur l'objet**
- Peut **seulement être utilisé dans la classe**
- Tous les accès aux attributs de la classe peuvent être faits avec `this`
- Le développeur peut s'en servir pour :
  - Accéder aux attributs et aux méthodes de la classe
  - Déterminer si 2 objets sont identiques
  - Peut être déréférencé `*this` pour accéder à l'objet courant

---

# Exemple d'implémentation de constructeur
▶︎ Sans le pointeur `this`
```cpp
Personnage::Personnage(string nom, int vie, int attaque, int defense){
    nom = nom;
    vie = vie;
    attaque = attaque;
    defense = defense;
}
```
🔴 **Il y a une ambiguïté !** Le compilateur ne sait pas s'il doit prendre le paramètre ou l'attribut, comme les noms sont les mêmes.

---

# Exemple d'implémentation de constructeur
▶︎ Avec le pointeur `this`
```cpp
Personnage::Personnage(string nom, int vie, int attaque, int defense){
    this->nom = nom;
    this->vie = vie;
    this->attaque = attaque;
    this->defense = defense;
}
```
🟢 **On lève l’ambiguïté**, le compilateur sera différencier les attributs des paramètres.
