# Les commandes essentielles de Github

### Sommaire

- [Les Forks](#les-forks)
  - [Forker un repository (1)](#forker-un-repository-1)
  - [Récupérer une copie locale (2)](#récupérer-une-copie-locale-2)
  - [Relier sa copie local au repository d'origine (7)](#relier-sa-copie-local-au-repository-dorigine-7)
  - [Créer une branche de travail (2)](#créer-une-branche-de-travail-2)
  - [Modifier votre copie local (4 & 5)](#modifier-votre-copie-local-4--5)
  - [Maintenez votre copie distante (6 & 10)](#maintenez-votre-copie-distante-6--10)
  - [Maintenez votre copie local synchronisé (8)](#maintenez-votre-copie-local-synchronisé-8)
  - [Maintenez votre branche synchronisé (9)](#maintenez-votre-branche-synchronisé-9)

![Le process Github](resources/github-process.png)

## Les Forks

### Forker un repository (1)

Sur [Github](https://github.com/), allez sur repository que vous souahitez forker.

Dans le coin en haut à droite, cliquez sur `Fork`.

Ce repository doit apparaitre sur votre Github.

### Récupérer une copie locale (2)

Créer un clone de ce nouveau fork :

```git
git clone https://github.com/<votre-nom-utilisateur-github>/<le-nom-du-fork>
```

### Relier sa copie local au repository d'origine (7)

Reliez votre clone local au repository d'origine :

```git
git remote add upstream <URL du repository d'origine>
```

Verifiez en tapant la commande :

```git
git remote -v
origin https://github.com/<votre-nom-utilisateur-github>/<le-nom-du-fork> (fetch)
origin https://github.com/<votre-nom-utilisateur-github>/<le-nom-du-fork> (push)
upstream <URL du repository d'origine> (fetch)
upstream <URL du repository d'origine> (fetch)
```

### Créer une branche de travail (2)

> /!\ encours de rédaction

```git
git checkout -b <newBranch>
```

### Modifier votre copie local (4 & 5)

> /!\ encours de rédaction

```git
git add .
```

```git
git commit -m <message de commit>
```

### Maintenez votre copie distante (6 & 10)

> /!\ encours de rédaction

```git
git push origin <newBranch>
```

### Maintenez votre copie local synchronisé (8)

> /!\ encours de rédaction

```git
git checkout master
git pull upstream master
git push origin master
```

### Maintenez votre branche synchronisé (9)

> /!\ encours de rédaction

```git
git checkout <newBranch>
git rebase master
```
