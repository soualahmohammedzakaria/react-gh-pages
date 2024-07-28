# Déploiement d'une application React* sur GitHub Pages

\* créée avec `create-react-app`

# Introduction

Dans ce tutoriel, je vais vous montrer comment créer une application React et la déployer sur GitHub Pages.

Pour créer l'application React, j'utiliserai [`create-react-app`](https://create-react-app.dev/), qui est un outil permettant de créer une application React de zéro. Pour déployer l'application React, j'utiliserai [`gh-pages`](https://github.com/tschaub/gh-pages), qui est un paquetage npm que les gens peuvent utiliser pour déployer des choses sur [GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages), un service d'hébergement web gratuit fourni par GitHub.

Si vous suivez ce tutoriel, vous obtiendrez une nouvelle application React - hébergée sur GitHub Pages - que vous pourrez ensuite personnaliser.

## Traductions

Ce tutoriel a été traduit de l'anglais original vers les langues suivantes:
- [Chinois traditionnel](https://github.com/gitname/react-gh-pages/issues/167#issuecomment-1925551338) (crédit: [@creaper9487](https://github.com/creaper9487))
- [Français](https://github.com/soualahmohammedzakaria/react-gh-pages/blob/master/README.md) (crédit: [@soualahmohammedzakaria](https://github.com/soualahmohammedzakaria))
- [Arabe](https://github.com/soualahmohammedzakaria/react-gh-pages/blob/master/READMEARABIC.md) (crédit: [@soualahmohammedzakaria](https://github.com/soualahmohammedzakaria))

# Tutoriel

## Prérequis

1. [Node et npm](https://nodejs.org/en/download/) sont installés. Voici les versions que j'utiliserai lors de la réalisation de ce tutoriel:

    ```shell
    $ node --version
    v16.13.2

    $ npm --version
    8.1.2
    ```
    > L'installation de npm ajoute deux commandes au système - `npm` et `npx` - que j'utiliserai toutes deux dans ce tutoriel.

2. [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) est installé. Voici la version que j'utiliserai pour ce tutoriel :

    ```shell
    $ git --version
    git version 2.29.1.windows.1
    ```

3. Un compte [GitHub](https://github.com/signup). :octocat:

## Procédure

### 1. Créer un dépôt **vide** sur GitHub

1. Connectez-vous à votre compte GitHub.
2. Visitez le formulaire [Créer un nouveau dépôt](https://github.com/new).
3. Remplissez le formulaire comme suit :
    - **Nom du dépôt:** Vous pouvez entrer le nom que vous voulez.

        > \* Pour un [site de projet](https://pages.github.com/#project-site), vous pouvez entrer le nom que vous voulez. Pour un [site utilisateur](https://pages.github.com/#user-site), GitHub [exige](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#types-of-github-pages-sites) que le nom du dépôt ait le format suivant : `{nom d'utilisateur}.github.io` (par exemple `gitname.github.io`)
        
        > Le nom que vous saisissez apparaîtra à plusieurs endroits : (a) dans les références au dépôt sur GitHub, (b) dans l'URL du dépôt, et (c) dans l'URL de l'application React déployée.

        > Dans ce tutoriel, je vais déployer l'application React en tant que site de projet.

        Je vais entrer : `react-gh-pages`
        
   - **Confidentialité du dépôt:** Sélectionnez _Public_ (ou _Privé_\*).

        > \* Pour les utilisateurs de [GitHub Free](https://docs.github.com/en/get-started/learning-about-github/githubs-products#github-free-for-user-accounts), le seul type de dépôt qui peut être utilisé avec GitHub Pages est _Public_. Pour les utilisateurs de [GitHub Pro](https://docs.github.com/en/get-started/learning-about-github/githubs-products#github-pro) (et les autres utilisateurs payants), les dépôts _Public_ et _Privé_ peuvent être utilisés avec les Pages GitHub.

        Je choisirai: _Public_

   - **Initialiser le dépôt:** Laissez toutes les cases à cocher vides.

        > Cela fera en sorte que GitHub crée un dépôt vide, au lieu de pré-remplir le dépôt avec un fichier `README.md`, `.gitignore`, et/ou `LICENSE`.
4. Soumettre le formulaire.

A ce stade, votre compte GitHub contient un dépôt vide, avec le nom et le type de confidentialité que vous avez spécifiés.

### 2. Créer une application React

1. Créez une application React nommée `my-app` :

    > Au cas où vous voudriez utiliser un nom différent de `my-app` (par exemple `web-ui`), vous pouvez le faire en remplaçant toutes les occurrences de `my-app` dans ce tutoriel, par cet autre nom (c'est-à-dire `my-app` --> `web-ui`).
  
    ```shell
    $ npx create-react-app my-app
    ```

    > Cette commande créera une application React écrite en JavaScript. Pour en créer une écrite en [TypeScript](https://create-react-app.dev/docs/adding-typescript/#installation), vous pouvez lancer cette commande à la place:
    > ```shell
    > $ npx create-react-app my-app --template typescript
    > ```

    Cette commande créera un nouveau dossier nommé `my-app`, qui contiendra le code source d'une application React.

    > En plus de contenir le code source de l'application React, ce dossier est aussi un dépôt Git. Cette caractéristique du dossier entrera en jeu à l'étape 6.

    > #### Noms de branches : `master` vs. `main`
    > 
    > Le dépôt Git aura une branche, qui sera nommée soit (a) `master`, le nom par défaut pour une nouvelle installation de Git ; ou (b) la valeur de la variable de configuration de Git, `init.defaultBranch`, si votre ordinateur utilise Git version 2.28 ou ultérieure _et_ si vous avez [défini cette variable](https://github.blog/2020-07-27-highlights-from-git-2-28/#introducing-init-defaultbranch) dans votre configuration Git (par exemple via `$ git config --global init.defaultBranch main`).
    >
    > Comme je n'ai pas défini cette variable dans mon installation Git, la branche dans mon dépôt sera nommée `master`. Dans le cas où la branche dans votre dépôt a un nom différent (que vous pouvez vérifier en lançant `$ git branch`), comme `main` ; vous pouvez **remplacer** toutes les occurrences de `master` dans le reste de ce tutoriel, avec cet autre nom (par exemple `master` → `main`).

2. Entrez dans le dossier nouvellement créé:
  
    ```shell
    $ cd my-app
    ```

A ce stade, il y a une application React sur votre ordinateur et vous êtes dans le dossier qui contient son code source. Toutes les autres commandes présentées dans ce tutoriel peuvent être exécutées à partir de ce dossier.

### 3. Installer le paquetage npm `gh-pages`.

1. Installez le paquet npm [`gh-pages`](https://github.com/tschaub/gh-pages) et désignez-le comme [dépendance de développement](https://docs.npmjs.com/specifying-dependencies-and-devdependencies-in-a-package-json-file):
 
    ```shell
    $ npm install gh-pages --save-dev
    ```

A ce stade, le paquettage npm `gh-pages` est installé sur votre ordinateur et la dépendance de l'application React à son égard est documentée dans le fichier `package.json` de l'application React.

### 4. Ajouter une propriété `homepage` au fichier `package.json`.

1. Ouvrez le fichier `package.json` dans un éditeur de texte.
   
    ```shell
    $ vi package.json
    ```

    > Dans ce tutoriel, l'éditeur de texte que j'utiliserai est [vi](https://www.vim.org/). Vous pouvez utiliser n'importe quel éditeur de texte ; par exemple, [Visual Studio Code](https://code.visualstudio.com/).

2. Ajoutez une propriété `homepage` dans ce format : `https://{nom d'utilisateur}.github.io/{nom du répertoire}`

    > \* Pour un [site de projet](https://pages.github.com/#project-site), c'est le format. Pour un [site utilisateur](https://pages.github.com/#user-site), le format est le suivant : `https://{nom d'utilisateur}.github.io`. Vous pouvez en savoir plus sur la propriété `homepage` dans la [section "GitHub Pages"](https://create-react-app.dev/docs/deployment/#github-pages) de la documentation `create-react-app`.
    ```diff
    {
      "name": "my-app",
      "version": "0.1.0",
    + "homepage": "https://gitname.github.io/react-gh-pages",
      "private": true,
    ```
A ce stade, le fichier `package.json` de l'application React inclut une propriété nommée `homepage`.

### 5. Ajouter des scripts de déploiement au fichier `package.json`.

1. Ouvrez le fichier `package.json` dans un éditeur de texte (s'il n'est pas déjà ouvert dans un).
   
    ```shell
    $ vi package.json
    ```

2. Ajoutez une propriété `predeploy` et une propriété `deploy` à l'objet `scripts` :

    ```diff
    "scripts": {
    +   "predeploy": "npm run build",
    +   "deploy": "gh-pages -d build",
        "start": "react-scripts start",
        "build": "react-scripts build",
    ```

A ce stade, le fichier `package.json` de l'application React inclut des scripts de déploiement.

### 6. Ajouter un "remote" qui pointe vers le dépôt GitHub

1. Ajouter un "[remote](https://git-scm.com/docs/git-remote)" au dépôt Git local.

    Vous pouvez le faire en lançant une commande dans ce format:
    
    ```shell
    $ git remote add origin https://github.com/{username}/{repo-name}.git
    ```
    
    Pour personnaliser cette commande en fonction de votre situation, remplacez `{nom d'utilisateur}` par votre nom d'utilisateur GitHub et remplacez `{nom du dépôt}` par le nom du dépôt GitHub que vous avez créé à l'étape 1.

    Dans mon cas, je vais exécuter:

    ```shell
    $ git remote add origin https://github.com/gitname/react-gh-pages.git
    ```

    > Cette commande précise à Git où je veux qu'il pousse les choses chaque fois que j'émets - ou que le paquet npm `gh-pages` agit en mon nom - la commande `$ git push` à partir de ce dépôt Git local.

A ce stade, le dépôt local a un "remote" dont l'URL pointe vers le dépôt GitHub que vous avez créé à l'étape 1.

### 7. Mettre l'application React dans le dépôt GitHub

1. Mettre l'application React dans le dépôt GitHub

    ```shell
    $ npm run deploy
    ```

    > Cela entraînera l'exécution des scripts `predeploy` et `deploy` définis dans `package.json`.
    >
    > Sous le capot, le script `predeploy` va construire une version distribuable de l'application React et la stocker dans un dossier nommé `build`. Ensuite, le script `deploy` va pousser le contenu de ce dossier vers un nouveau commit sur la branche `gh-pages` du dépôt GitHub, en créant cette branche si elle n'existe pas encore.

    > Par défaut, le nouveau commit sur la branche `gh-pages` aura un message de commit de "Updates". Vous pouvez [spécifier un message de livraison personnalisé](https://github.com/gitname/react-gh-pages/issues/80#issuecomment-1042449820) via l'option `-m`, comme ceci:
    > ```shell
    > $ npm run deploy -- -m "Deploy React app to GitHub Pages"
    > ```

A ce stade, le dépôt GitHub contient une branche nommée `gh-pages`, qui contient les fichiers qui composent la version distribuable de l'application React. Cependant, nous n'avons pas encore configuré GitHub Pages pour _servir_ ces fichiers.

### 8. Configurer GitHub Pages

1. Naviguez vers la page de configuration de **GitHub Pages**.
   1. Dans votre navigateur web, naviguez vers le dépôt GitHub
   1. Au-dessus du navigateur de code, cliquez sur l'onglet "Paramètres"
   1. Dans la barre latérale, dans la section "Code et automatisation", cliquez sur "Pages"
1. Configurez les paramètres "Construction et déploiement" comme suit : 
   1. **Source**: Déployer à partir d'une branche
   2. **Branche**: 
      - Branche: `gh-pages`
      - Dossier: `/ (root)`
1. Cliquez sur le bouton "Sauvegarder".

**L'application React a été déployée sur GitHub Pages! :rocket :

A ce stade, l'application React est accessible à toute personne qui visite l'URL `homepage` que vous avez spécifié à l'étape 4. Par exemple, l'application React que j'ai déployée est accessible à https://gitname.github.io/react-gh-pages.

### 9. (Facultatif) Stocker le _code source_ de l'application React sur GitHub

Dans une étape précédente, le paquetage npm `gh-pages` a mis la version distribuable de l'application React dans une branche nommée `gh-pages` dans le dépôt GitHub. Cependant, le _code source_ de l'application React n'est pas encore stocké sur GitHub.

Dans cette étape, je vais vous montrer comment vous pouvez stocker le code source de l'application React sur GitHub.

1. Livrez les changements que vous avez fait pendant que vous suiviez ce tutoriel, à la branche `master` du dépôt Git local; ensuite, poussez cette branche vers la branche `master` du dépôt GitHub.

    ```shell
    $ git add .
    $ git commit -m "Configure React app for deployment to GitHub Pages"
    $ git push origin master
    ```

    > Je recommande d'explorer le dépôt GitHub à ce stade. Il y aura deux branches : `master` et `gh-pages`. La branche `master` contiendra le code source de l'application React, tandis que la branche `gh-pages` contiendra la version distribuable de l'application React.

# Références

1. [Le guide officiel de déploiement de `create-react-app`](https://create-react-app.dev/docs/deployment/#github-pages)
2. [GitHub blog : Construire et déployer des pages GitHub à partir de n'importe quelle branche](https://github.blog/changelog/2020-09-03-build-and-deploy-github-pages-from-any-branch/)
3. [Préserver le fichier `CNAME` lors de l'utilisation d'un domaine personnalisé](https://github.com/gitname/react-gh-pages/issues/89#issuecomment-1207271670)

# Notes

- Un grand merci à GitHub (la société) pour nous avoir fourni gratuitement le service d'hébergement GitHub Pages.
- Et maintenant, il est temps de transformer l'application React par défaut générée par `create-react-app` en quelque chose d'unique!
- Ce dépôt consiste en deux branches : 
    - `master` - le _code source_ de l'application React
    - `gh-pages` - l'application React _construite à partir_ de ce code source

 # Contributeurs

Merci à ces personnes pour avoir contribué à la maintenance de ce tutoriel.
<!--

Template:
---------

<a href="https://github.com/____" target="_blank" title="____">
  <img src="https://github.com/____.png?size=40" height="40" width="40" alt="____" />
</a>

Instructions:
-------------

1. Copiez le modèle et collez-le ci-dessous.
2. Remplacez les quatre chaînes "____" par le nom d'utilisateur GitHub du contributeur.

Note: J'ai spécifié les avatars en utilisant HTML parce que, lorsque je l'ai fait en utilisant Markdown,
      seuls les avatars _personnalisés_ apparaissaient à la taille que j'avais spécifiée via l'URL
      (par exemple, 40px au carré, pour `https://github.com/gitname.png?size=40`) ;
      les avatars générés par GitHub semblaient ignorer le paramètre de taille et,
      et apparaissent à leur taille maximale (environ 420px au carré).
      En utilisant HTML, je peux forcer les deux types d'avatars à apparaître à 40px au carré.

-->

<a href="https://github.com/gitname" target="_blank" title="gitname">
  <img src="https://github.com/gitname.png?size=40" height="40" width="40" alt="gitname" />
</a>
<a href="https://github.com/rhulse" target="_blank" title="rhulse">
  <img src="https://github.com/rhulse.png?size=40" height="40" width="40" alt="rhulse" />
</a>
<a href="https://github.com/AbhishekCode" target="_blank" title="AbhishekCode">
  <img src="https://github.com/AbhishekCode.png?size=40" height="40" width="40" alt="AbhishekCode" />
</a>
<a href="https://github.com/adnjoo" target="_blank" title="adnjoo">
  <img src="https://github.com/adnjoo.png?size=40" height="40" width="40" alt="adnjoo" />
</a>
<a href="https://github.com/thebeatlesphan" target="_blank" title="thebeatlesphan">
  <img src="https://github.com/thebeatlesphan.png?size=40" height="40" width="40" alt="thebeatlesphan" />
</a>
<a href="https://github.com/valerio-pescatori" target="_blank" title="valerio-pescatori">
  <img src="https://github.com/valerio-pescatori.png?size=40" height="40" width="40" alt="valerio-pescatori" />
</a>
<a href="https://github.com/jackweyhrich" target="_blank" title="jackweyhrich">
  <img src="https://github.com/jackweyhrich.png?size=40" height="40" width="40" alt="jackweyhrich" />
</a>

<a href="https://github.com/soualahmohammedzakaria" target="_blank" title="soualahmohammedzakaria">
  <img src="https://github.com/soualahmohammedzakaria.png?size=40" height="40" width="40" alt="soualahmohammedzakaria" />
</a>

Cette liste est maintenue manuellement - pour l'instant - et inclut (a) chaque personne qui a soumis une pull request qui a finalement été fusionnée dans `master`, et (b) chaque personne qui a contribué d'une manière différente (par exemple en fournissant un feedback constructif) et qui a approuvé le fait que je l'inclue dans cette liste.
