# GitHub authentification SSH
GitHub a supprimé la possibilité de s'identifier en rentrant son mot de passe web à partir du terminal, sur une distribution Linux. Il faudra donc utiliser la méthode d'échange de clé SSH qui est davantage sécurisée.

## Génération d'une clé SSH
1. Sur votre session, ouvrez un terminal.
2. Collez le texte ci-dessous, en **remplaçant l’e-mail utilisé dans l’exemple par votre adresse e-mail GitHub**.
    ```
    ssh-keygen -t ed25519 -C "your_email@e.rascol.net"
    ```
3. Lors de la demande de répertoire dans lequel enregistrer votre clé, appuyez sur entrer :
    ```
    > Enter a file in which to save the key (/home/YOU/.ssh/id_ALGORITHM):[Press enter]
    ```
4. À l’invite, tapez une phrase secrète sécurisée. Ce sera le mot de passe qui sécurise votre clé privée, sans celui-ci impossible d'utiliser la clé.
   ```
   > Enter passphrase (empty for no passphrase): [Type a passphrase]
   > Enter same passphrase again: [Type passphrase again]
   ```

## Ajouter votre clé publique à GitHub
Après avoir généré une paire de clés SSH, vous devez ajouter la clé publique à GitHub.com afin d'activer l’accès SSH pour votre compte.

1. Copiez la clé publique SSH dans votre Presse-papiers.
```
cat ~/.ssh/id_ed25519.pub
```
![](assets/catCleSSHPub.png)
Copiez la clé affichée sur le terminal (tout la sortie de la commande `cat`, tout ce qui est affiché en bleu sur le screenshot)!
2. Dans l’angle supérieur droit d’une page de GitHub, cliquez sur la photo de votre profil, puis sur Paramètres.
3. Dans la section « Accès » de la barre latérale, cliquez sur 🔑 Clés SSH et GPG.
4. Cliquez sur Nouvelle clé SSH ou Ajouter une clé SSH.
5. Dans le champ « Titre », ajoutez une étiquette descriptive pour la nouvelle clé. Par exemple, si vous utilisez un ordinateur portable personnel, vous pouvez nommer cette clé « Ordinateur portable personnel ».
6. Sélectionnez le type de clé : **authentification**.
7. Dans le champ « Clé », collez votre clé publique.
8. Cliquez sur Ajouter une clé SSH.
9. **Refaite la même procédure pour une clé en mode signature**, vous collerez la même clé publique !

## Cloner un repos avec SSH
À présent quand vous devrez cloner un repository à partir de GitHub, il faudra choisir l'adresse SSH de celui-ci :

![](assets/cloneReposSSH.png){: style="width:400px"}

1. Utiliser la commande `git clone` sur le terminal avec le lien ssh copié sur le repos GitHub :
```bash
etudiant@VM-Debian-Etu:~$ git clone git@github.com:ciel-ir-rascol/cpp-tp20-revisions-richard-hendricks81.git

```
2. Répondez `yes` à la demande de connexion :
```bash
Clonage dans 'cpp-tp20-revisions-richard-hendricks81'...
The authenticity of host 'github.com (140.82.121.4)' can't be established.
ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
```
3. Entrez le mot de passe de votre clé SSH défini plus tôt :
```bash
Enter passphrase for key '/home/etudiant/.ssh/id_ed25519':
```