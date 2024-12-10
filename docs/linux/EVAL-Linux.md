# Evaluation Linux - 1CIEL-IR

Vous devez mettre en oeuvre la configuration suivante sur le thème du *Seigneur des anneaux*, pour la VM `EvalLinux1CIELIR_DebianXfce`.

![](figures/ringFrodon.jpg){: style="width:70%"}

## Groups

- `magiciens`
- `elfes`
- `hommes`
- `hobbits`
- `bons`
- `mechants`

## Users

| User | Password | Groups |
| :---: | :---: | :---: |
| `gandalf` | `mithrandir` | `bons`, `magiciens`, `sudo` |
| `saroumane` | `curunir` | `mechants`, `magiciens`, `sudo`|
| `galadriel` | `arthanis` | `bons`,`elfes` |
| `legolas` | `legolas` | `bons`,`elfes` |
| `aragorn` | `elessar` | `bons`,`hommes` |
| `bilbon` | `bilba` | `bons`,`hobbits` |


## Directories

- Avec un éditeur de texte en mode console (sont disponibles vim et nano) vous créerez les fichiers suivants et appliquerez les permissions demandées :

| Fichier | Contenu fichier | Chemin | Permissions |
| :---: | :---: | :---: | :---: |
| `atoutsGandalf.txt` | `épée, baton`| `/home/gandalf` | `rwx r-x r-x gandalf gandalf`|
| `atoutsSaroumane.txt` | `palantir, baton`| `/home/saroumane`| `rwx r-x r-x saroumane saroumane` |
| `atoutsGaladriel.txt` | `nenya, épée`| `/home/galadriel` | `rwx r-x r-x galadriel galadriel` |
| `atoutsLegolas.txt` | `arc, épée`| `/home/legolas` | `rwx r-x r-x legolas legolas` |
| `atoutsAragorn.txt` | `anduril`| `/home/aragorn` | `rwx r-x r-x aragorn aragorn` |
| `atoutsBilbon.txt` | `dard, pipe`| `/home/bilbon` | `rwx r-x r-x bilbon bilbon` |
 

- Vous téléchargerez les fichiers suivants, ferez les déplacements et appliquerez les permissions demandées :
```text
wget http://eval.lan.rascol-info.org/comte.zip
wget http://eval.lan.rascol-info.org/fondcombe.zip
wget http://eval.lan.rascol-info.org/gondor.zip
wget http://eval.lan.rascol-info.org/isengard.zip
```

| Fichiers téléchargés | Chemin de déplacement | Permissions finales |
| :---: | :---: | :---: |
| `comte/*` |  `/TerreMilieu/Comte/` | `rwx r-- --- bilbon hobbits` |
| `fondcombe/*` |  `/TerreMilieu/Fondcombe/` | `rwx r-x --x galadriel elfes` |
| `gondor/*` |  `/TerreMilieu/Gondor/` | `rwx r-x r-x aragorn hommes` |
| `isengard/*` |  `/TerreMilieu/Isengard/` | `rwx r-x --x saroumane magiciens` |


**👨‍💻 À vos claviers !**

![](figures/gandalfMac.png){: style="width:30%"}