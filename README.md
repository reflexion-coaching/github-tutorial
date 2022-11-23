# Tutoriel : GitHub

Site officiel de GitHub : https://github.com/

Répertoire du projet : https://github.com/reflexion-coaching/

Présentation de GitHub : https://www.youtube.com/watch?v=pBy1zgt0XPc

Tutoriel OpenClassRoom : https://openclassrooms.com/fr/courses/7162856-gerez-du-code-avec-git-et-github

Tutoriel officiel : https://docs.github.com/en/get-started

## Quoi ?

**Git** est un gestionnaire de versions. Git se présente sous la forme d'un petit dossier **.git** conservé dans le dossier contenant les fichiers. 

**GitHub** est un outil en ligne de gestion de répertoire Git. Il existe des alternatives comme GitLab ou Bitbucket. 

Git et GitHub sont spécialisés dans le contrôle de version du code informatique. 

## Pourquoi ?

**Git** permet aux développeurs de conserver un historique des modifications et des versions de tous leurs fichiers. Il est notamment possible de travailler sur une partie du code pendant qu'un collègue travaille sur une autre partie. Git s'occupera ensuite de *merger* (ou combiner) les deux versions du code. 

**GitHub** permet de conserver/partager des fichiers et de travailler en équipe sur un même projet. GitHub sert de *point de rencontre* entre les différentes versions d'un même répertoire Git.

## Les concepts 

**Un répertoire** ou dépot est le dossier contenant notre code.

**Un répertoire distant** est le dossier contenant notre code **sur GitHub**. Les répertoires sont publics (ouverts à tous) ou privés (accès sous condition).

**Un répertoire local** est le dossier contenant notre code **sur notre ordinateur**. 

**Cloner** un répertoire signifie télécharger en local (i.e. sur son ordinateur) en répertoire distant (i.e. sur GitHub).

**Les forks** désignent les versions d'un répertoire distant clonées sur les ordinateurs. Par exemple : lorsque je clone un répertoire sur mon ordinateur, je fais une *fork* du répertoire GitHub.

**Les branches** sont les différentes versions du code. Habituellement, la branche *main* ou *master* contient la version principale. Une bonne pratique est de modifier le code sur une branche différente de la branche *main* et puis de la fusionner avec la branche principale lorsque que les modifications ont été codées et testées.

**Merge** une branche signifie fusionner deux branches. Généralement, on merge une branche de développement avec la branche principal *main*.

**Les commits** sont des modifications apportées au code et enregistrées dans Git.

**Les pushs** sont des mises à jour du répertoire distant à partir du répertoire local. Par exemple : j'ai bien travaillé et j'ai ajouté plusieurs fonctionnalités dans mon code. J'ai écrit ces nouvelles fonctionnalités dans une branche `dev/Arnaud`, puis j'ai fait des *commits* pour enregistrer ces modifications dans le répertoire local Git. Pour partager mes améliorations avec le reste de l'équipe, je fais un *push* de mon répertoire sur GitHub. 

**Les pulls** sont l'inverse des *pushs* : ce sont les mises à jour du répertoire local à partir du répertoire distant. Dans l'exemple précédent, les autres membres de l'équipe devront faire un *pull* pour recevoir la mise à jour du code sur leur ordinateur.


## Comment ?

### 1. Installation

La partie du tutoriel d'OpenClassRoom sur l'installation est très bien faire (https://openclassrooms.com/fr/courses/7162856-gerez-du-code-avec-git-et-github/7165721-installez-git-sur-votre-ordinateur).

La première étape est de créer un compte sur https://github.com/. La plan tarifaire gratuit suffit amplement. 

La deuxième étape est d'installer Git sur son ordinateur : https://git-scm.com/downloads. Généralement, les commandes Git s'effecutent en ligne de commande dans le terminal.

La troisième étape est d'enregistrer ses identifiants Git sur son ordinateur. Il y a peu, GitHub a arrêté l'identification par mot de passe au profit des clés d'authentification. Depuis, l'authentification est devenue un peu plus laborieuse à mettre en place mais GitHub décrit la marche à suivre sur sa page https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/about-authentication-to-github.

### 2. Cloner un répertoire existant

Pour télécharger sur son ordinateur (dépôt local) un répertoire Git existant sur Github (dépôt distant), on utilise la commade `git clone`. 

Sur la page GitHub du répertoire à cloner, l'onglet **Code** contient l'adresse HTTPS du répertoire distant. Par exemple, l'adresse GitHub de notre repertoire pour ce tutoriel : https://github.com/reflexion-coaching/github-tutorial.git

Pour cloner le répertoire, j'ouvre un terminal à l'endroit où je vais placer le répertoire et je tape :

```
$ git clone https://github.com/reflexion-coaching/github-tutorial.git
Cloning into 'github-tutorial'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.
```

Le répertoire sera téléchargé dans le dossier dans lequel on se trouve. :)

### 3. Créer un répertoire sur GitHub

GitHub facilite et décrit la création d'un nouveau répertoire GitHub sur la page **repositories** d'un compte. Les instructions sont très claires.

### 4. Créer une branche

La commande `git branch` affiche les branches en local :

```
$ git branch
* main
```

L'astérix indique la branche actuelle. 

Pour créer une nouvelle branche, j'utilise la commande `git branch` à laquelle j'ajoute le nom de la branche :

```
$ git branch add-gitignore

$ git branch # on affiche à nouveau toutes les branches
add-gitignore
* main
```

Maintenant que la branche est créée, je me place sur la nouvelle branche :

```
$ git checkout add-gitignore
Switched to branch 'add-gitignore'

$ git branch
* add-gitignore
  main
```

Impeccable : On va pouvoir modifier le code sur notre branche !

### 5. Modifier le code d'une branche

Les commandes pour modifier une branche sont `git add` et `git commit`. 

Par exemple : je veux ajouter un fichier *.gitignore* à mon répertoire. Le fichier *.gitignore* est un fichier qui contient la liste des éléments que Git ne doit pas ajouter au répertoire. C'est assez utile pour éviter que des identifiants ou clés de sécurité ne se retrouvent sur le répertoire GitHub. Pour cet exemple, je veux juste enlever de Git les fichiers *.DS_Store*.

Je crée le fichier `.gitignore` et y ajoute `**/.DS_Store` :

```
$ touch .gitignore

$ echo "**/.DS_Store" >> .gitignore
```

Super, maintenant je veux dire à Git que j'ai modifié le contenu de mon répertoire. J'utilise donc la commande `git add .` pour ajouter le code à Git et `git commit -m ""` afin de créer un commit :

```
$ git add .

$ git commit -m "ajout du .gitignore" 
[add-gitignore f98c9ac] ajout du .gitignore
 1 file changed, 1 insertion(+)
 create mode 100644 .gitignore
```

Parfait ! Le message indique qu'un nouveau fichier *.gitignore* a été ajoutée au dépôt avec comme message de commit "ajout du .gitignore".

### 6. Pusher le nouveau code sur GitHub

La commande servant à *pusher* du code local sur le répertoire distant est `git push` : 

```
$ git push origin add-gitignore
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 8 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 292 bytes | 292.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
remote: 
remote: Create a pull request for 'add-gitignore' on GitHub by visiting:
remote:      https://github.com/reflexion-coaching/github-tutorial/pull/new/add-gitignore
remote: 
To https://github.com/reflexion-coaching/github-tutorial.git
 * [new branch]      add-gitignore -> add-gitignore
```

Ici, on a mis à jour la branche `add-gitignore` sur Github. `origin` contient les adresses GitHub de notre répertoire. Pour afficher les adresses, la commande est :

```
$ git remote -v
origin	https://github.com/reflexion-coaching/github-tutorial.git (fetch)
origin	https://github.com/reflexion-coaching/github-tutorial.git (push)
```

Attention ! Pour que le *push* fonctionne, il faut être un *collaborateur* du répertoire GitHub. L'administrateur du dépôt doit au préalable ajouter à la liste des collaborateurs toute personne qui souhaite faire un *push*.

### 7. Fusionner deux branches

La plupart du temps, les *pull requests & merges* (les deux actions permettant de fusionner les branches) se font directement sur GitHub. Il suffit d'aller sur la page du répertoire (https://github.com/reflexion-coaching/github-tutorial), de cliquer sur **Compare & pull request** et suivre les instructions

### 8. Supprimer une branche 

Avant de supprimer une branche sur un répertoire local, il faut s'assurer de ne pas être sur la branche à supprimer et le cas échant, changer de branche. Dans notre cas, je veux supprimer la branche `add-gitignore` et je me place donc sur la branche principale :

```
$ git branch 
* add-gitignore
  main

$ git checkout main
Switched to branch 'main'
```

Ensuite, on utilise la commande `git branch -d` pour supprimer une branche :

```
$ git branch -d add-gitignore
Deleted branch add-gitignore (was e047582).

$ git branch
* main
```

CQFD !

### 9. Faire un pull

Enfin, pour mettre à jour notre code en local avec le répertoire GitHub, on effectue un **pull**. Le pull s'effectue sur la branche `main` avec la commande :

```
$ git pull origin main
 * branch            main       -> FETCH_HEAD
Updating e775f70..e047582
Fast-forward
 .gitignore | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 .gitignore
```

La branche *main* du répertoire local et distant sont maintenant à jour :)

## Commandes utiles

Voici une liste des commandes Git les plus souvent utilisées :

* create a repository: `git init .`

* add content: `git add .`

* make a commit: `git commit -m "bla bla bla"`

* push to remote github account (main branch): `git push origin main`

* pull contents from main branch: `git pull origin main`

* create a new branch: `git branch new_branch`

* push a new branch to remote: `git push (-u) origin new_branch`

* check which branch we use: `git branch`

* switch branch : `git checkout new_branch`

* delete a branch (switch before to another branch): `git branch -d branch_to_delete`

* delete a branch on remote repository: `git push origin -d branch_to_delete`

* update after modifying *.gitignore* :

    ```
    git rm -r --cached .
    git add -A
    git commit -m 'removing ignored files'
    ```

