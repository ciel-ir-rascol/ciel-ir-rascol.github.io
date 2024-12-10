# ACT03 : Gérer les permissions

Vous êtes technicien dans l'entreprise de service réseau AlbiTech et un de vos client M.Turing fait appel à vous pour la configuration d'un serveur linux, tournant sur une carte Raspberry Pi. Vous établissez ensemble le cahier des charges suivant :

- Création de 4 comptes utilisateurs et de 3 nouveaux groupes:
  
 | Utilisateur | Groupes                 | Pass     |
 | ----------- | ----------------------- | -------- |
 | alan        | sudoers parents famille | enigma   |
 | grace       | sudoers parents famille | hopper   |
 | richard     | enfants famille         | stallman |
 | linus       | enfants famille         | torvalds |

!!! info
    Lorsque un utilisateur est créé Linux crée automatiquement le groupe du même nom.

- Création de répertoires :

| Répertoire             | Propriétaire | Groupe  | Droits      |
| ---------------------- | ------------ | ------- | ----------- |
| /media/photos          | alan         | famille | rwx rwx r-x |
| /partage/cadeaux       | alan         | parents | rwx rwx --- |
| /partage/administratif | alan         | parents | rwx rwx --- |
| /home/alan/TuringTest  | alan         | alan    | rwx rwx --- |
| /home/grace/Cobol      | grace        | grace   | rwx rwx --- |

- Transfert de fichiers dans les répertoires créés, depuis un serveur web :

| Fichiers        | Répertoire de destination |
| --------------- | ------------------------- |
| administratif/* | /partage/administratif    |
| photos/*        | /media/photos             |
| cobol/*         | /home/grace/Cobol         |
| turingtest/*    | /home/alan/TuringTest     |

Pour télécharger les fichiers à classer :

```bash
wget https://ciel-ir-rascol.github.io/linux/ressources/files.zip
```

!!! info
    Pour décompresser l'archive .zip téléchargée vous aurez besoin de télécharger l'utilitaire `unzip` :
    ```bash    
    sudo apt install unzip

    #Pour décompresser
    unzip archive.zip
    ```

Bien vérifier que les permissions des dossiers soient répercutées sur les fichiers.

!!! question
    1. Créez les utilisateurs
    2. Créez les groupes
    3. Ajouter les utilisateurs aux groupes
    4. Créez les répertoires 
    5. Téléchargez les fichiers et mettez les dans les bons répertoires
    6. Appliquez les permissions récursivement aux répertoires
    7. Appelez l'enseignant pour vérifier