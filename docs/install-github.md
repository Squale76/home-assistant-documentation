# Home Assistant sur Github

### Sommaire

- [Recherches](#recherches)
- [Mettre au secret](#mettre-au-secret)
- [Créer le repository](#créer-le-repository)
- [Synchronisation Production / Développement](#synchronisation-production--développement)
- [La sauvegarde sur Github](#la-sauvegarde-sur-github)
- [L'organisation des fichiers](#lorganisation-des-fichiers)
- [Les explications](#les-explications)
  - [configuration.yaml](#configurationyaml)
  - [secrets.yaml](#secretsyaml)
  - [ui-lovelace.yaml](#ui-lovelaceyaml)
  - [entities/](#entities)
  - [influxdb/](#influxdb)
  - [integrations/](#integrations)
  - [lovelace/](#lovelace)
- [Suivi des modifications](#suivi-des-modifications)

## Recherches

Pour commencer, c'est ce [tuto](https://peyanski.com/automatic-home-assistant-backup-to-github/) en :uk: qui m'a donné envie de sauvegarder mon Home Assistant *automagiquement* (*petite dédicace à un de mes formateurs* :wink:) dans Github.
Une belle [vidéo](https://www.youtube.com/watch?v=9-OG3bCQFFQ) toujours en :uk:.

## Mettre au secret

La 1ère chose à faire est de bien vérifier que toutes les informations sensibles sont bien dans des fichiers séparés que je ne déposerais pas sur le repository.

## Créer le repository

Depuis Github, j'ai créer un repository [home-assistant-configuration](https://github.com/Squale76/home-assistant-configuration) qui me permettra de sauvegarder mes modifications en les versionnant.

## Synchronisation Production / Développement

Pour ne pas travailler sur mon Home Assistant de production et risquer de rendre hors service ma domotique, j'ai choisi de copier mes fichiers de mon Home Assisatnt de production vers un répertoire en local.

Cette copie s'effectue pour l'instant à la main avec un logiciel de comparaison de fichiers [WinMerge](https://winmerge.org/?lang=fr). WinMerge permet d'utiliser des [filtres](https://manual.winmerge.org/en/Filters.html) pour ne pas comparer l'ensemble des fichiers d'un répertoire comme les logs, la base de données , etc ...

<details><summary>Voici le filtre que j'utilise :</summary>

```texte
## This is a directory/file filter template for WinMerge
name: Home Assistant
desc: Ignorenon included files

## Select if filter is inclusive or exclusive
## Inclusive (loose) filter lets through all items not matching rules
## Exclusive filter lets through only items that match to rule
## include or exclude
def: include

## Filters for filenames begin with f:
## Filters for directories begin with d:
## (Inline comments begin with " ##" and extend to the end of the line)

f: \.gitignore$
f: package.json$
f: package-lock.json$
f: home-assistant_v2.db$
f: home-assistant_v2.db-shm$
f: home-assistant_v2.db-wal$
f: home-assistant.log$

d: \\\.cloud$
d: \\\.storage$
d: \\\.vscode$
d: \\deps$
```

</details>

## La sauvegarde sur Github

> en cours de rédaction

## L'organisation des fichiers

<details><summary>Mon arborescence</summary>

- [entities/](#entities)
  - [sensors/](#sensors)
    - xxxxxxxx.yaml
- [influxdb/](#influxdb)
  - xxxxxxxx.yaml
- [integrations/](#integrations)
  - [automation.yaml](#automationyaml)
  - [bdd.yaml](#bddyaml)
  - [default_config.yaml](#default_configyaml)
  - [http.yaml](#integrations\http.yaml)
  - [loggers.yaml](#loggersyaml)
  - [lovelace.yaml](#lovelaceyaml)
  - [panels.yaml](#panelsyaml)
  - [scene.yaml](#sceneyaml)
  - [script.yaml](#scriptyaml)
  - [sensor.yaml](#sensoryaml)
- [lovelace/](#lovelace)
  - [default/](#default)
    - [cards/](#cards)
      - xxxxxxxx.yaml
    - [views/](#views)
      - xxxxxxxx.yaml
    - [dashboard.yaml](#dashboardyaml)
  - [dashboards.yaml](#dashboardsyaml)
- [configuration.yaml](#configurationyaml)
- [secrets.yaml](#secretsyaml)
- [ui-lovelace.yaml](#ui-lovelaceyaml)

</details>

## Les explications

Le découpage des fichiers s'est fait pour une plus grande clareté du développement. Je me suis basé sur les conseils avisés de [Clemalex](https://forum.hacf.fr/t/resources-lovelace-dans-ui-lovelace-yaml/1660/4) et des configurations de :

- [oncleben31](https://github.com/oncleben31/home-assistant-config/tree/master/config)
- [frenck](https://github.com/frenck/home-assistant-config/tree/master/config)

Gràce à ce découpage, si je souhaites modifier une carte par exemple, je modifie uniquement le fichier associé à cette carte qui ne contient **que** le code de cette carte. Il en résulte moins d'effet de bord.

> Petit rappel :
> Dans un fichier YAML :
>
> - une **liste** est symbolisée par une énumération d'élément indenté au même niveau et commençant par un `'-'`.
> - un **dictionnaire** est symbolisé par un une énumération d'élément indenté au même niveau sans `'-'`.

Chaque fichier peut inclure d'autres fichiers via les commandes :

- `!include` :

  inclura le contenu du fichier à l'emplacement de cette directive.

- `!include_dir_named` :

  retournera le contenu d'un répertoire sous forme de dictionnaire qui associera le contenu du fichier au nom de ce fichier.

- `!include_dir_list` :

  retournera le contenu d'un répertoire sous forme de liste. Chaque fichier contenu dans ce répertoire sera une entrée de la liste. Les entrées de la liste seront classées par ordre alphanumérique.

- `!include_dir_merge_list` :

  retournera le contenu d'un répertoire sous forme de liste en fusionnant tous les fichiers pour obtenir une liste unique.

- `!include_dir_merge_named` :

  retournera le contenu d'un répertoire sous forme d'un dictionnaire en fusionnant tous les fichiers pour obtenir qu'un seul dictionnaire.

### configuration.yaml

Ce fichier est nécessaire à Home Assistant. C'est ce fichier qui sera lu en premier. Je n'ai pas réussi à exporter le bloc `homeassistant` de ce fichier.

### secrets.yaml

Ce fichier contient toutes les données personnelles et sensibles comme la localisation, les adresses IP des appareils et les compte / mot de passe utilisés dans Home Assistant.

> **ATTENTION**, il ne doit **absolument** pas être sauvegardé sur Github même une seule fois par erreur, sous peine d'être lisible par les personnes qui ont accès à votre Github vai les anciens commits.

### ui-lovelace.yaml

Ce fichier contient le tableau de bord par défaut affiché. Il permet d'être redirigé vers la page de son profil pour choisir son tableau de bord par défaut.

### entities/

Ce répertoire contient toutes les entités créées manuellement.

### influxdb/

Ce répertoire contient toutes les entités qui devront être sauvegardées en base de données pour une historisation supérieure à 24h (norme dans Home Assistant).

#### sensors/

### integrations/

Ce répertoire contient l'ensemble des intégrations. Pour être utilisé, il est nécessaire d'ajouter au fichier `configuration.yaml` la ligne :

```yaml
  packages: !include_dir_named integrations
```

Cette ligne permettra de lire chaque fichier ayant l'extension `.yaml` de ce répertoire et de l'inclure au fichier `configuration.yaml` pour être interprété par Home Assistant.

#### automation.yaml

Ce fichier permet d'inclure toutes les automatisations :

- celles générées via l'UI contenues dans le fichier `config/automations.yaml`
- celles gérées manuellement, rangées comme l'utilisateur le souhaite, dans le répertoire `config/automations/` (via la directive `!include_dir_merge_list`)

#### bdd.yaml

Ce fichier contient tous les paramètres liés à la connexion et à l'utilisation des bases de données.
Via la directive `include`, seules les entités listées dans le répertoire [influxdb](#influxdb) seront sauvegardées pour historisation.

#### default_config.yaml

Ce fichier contient la configuration par défaut de Home Assistant.

#### http.yaml

Ce fichier contient la configuration du serveur Web `http` de Home Assisant. Il est indispensable si vous utilisez des ressources locales (comme une page 404 personnalisée) stockées dans le répertoire `config/www/`.

#### loggers.yaml

Ce fichier contient la configuration du système de traçage. Il est particulièrement utile lors d'un débuggage. En changeant le niveau de traces par défaut, il est possible d'augmenter ou diminuer les traces récupérées dans le `Supervisor`.

Une documentation officielle plus détaillée est visible sur la page [Logger](https://www.home-assistant.io/integrations/logger/) de Home Assistant.

#### lovelace.yaml

Ce fichier contient la configuration de Lovelace (La couche logicielle permettant d'afficher les différents tableaux de bord).

C'est dans ce fichier que sera défini le mode de stockage de la configuration (`yaml` ou `storage`), les ressources externes utilisées et l'inclusion des différents tableaux de bords.

Une documentation officielle plus détaillée est visible sur la page [Dashboards and Views](https://www.home-assistant.io/lovelace/dashboards-and-views/) de Home Assistant.

#### panels.yaml

Ce fichier contient la configuration des différents panels affichés dasn des Iframe.

#### scene.yaml

Ce fichier permet d'inclure toutes les scene :

- celles générées via l'UI contenues dans le fichier `config/scenes.yaml`
- celles gérées manuellement, rangées comme l'utilisateur le souhaite, dans le répertoire `config/scenes/` (via la directive `!include_dir_list`)

#### script.yaml

Ce fichier permet d'inclure tous les scripts rangées comme l'utilisateur le souhaite, dans le répertoire `config/scripts/` (via la directive `!include_dir_named`).

#### sensor.yaml

Ce fichier permet d'inclure tous les capteurs rangées comme l'utilisateur le souhaite, dans le répertoire `config/entities/sensors/` (via la directive `!include_dir_list`)

### lovelace/

Ce répertoire contient l'ensemble des tableaux de bord.

#### dashboards.yaml

Ce fichier permet de définir tous les tableaux de bord avec leur caractéristiques.
Vous pouvez voir [la documentation officielle](https://www.home-assistant.io/lovelace/dashboards-and-views/#dashboards) malheureusement en :uk:

#### default/

Ce répertoire contient l'ensemble des informations nécessaire à la définition d'un tableau de bord.

Il a été nommé `default` mais peut être renommé différemment tant que la directive `filemname` du fichier [dashboards.yaml](#dashboardsyaml) est mise à jour.

#### dashboard.yaml

Ce fichier permet d'inclure les différentes vues à afficher dans ce tableau de bord ainsi que l'ordre d'affichage dans la liste d'onglet en haut de la page via la liste d'inclusion :

```yaml
views:
  - !include views/weather.yaml
  - !include views/energies.yaml
  - !include views/temperature.yaml
  - !include views/batteries.yaml
```

L'intérêt d'utiliser la directive `!include` plutôt que les autres directives d'inclusion permet de gérer l'ordre d'affichage dans les onglets des vues (Merci @Clemalex du forum HACF).

#### cards/

Ce répertoire contient les définitions des cartes utilisées dans ce tableau de bord.

#### views/

Ce répertoire contient les définitions des vues utilisées dans ce tableau de bord.
Ces vues seront appelées via la directive `!include` contenue dans le fichier [dashboard.yaml](#dashboardyaml).

Dans les vues, il sera possible de configurer :

- le chemin pour y accéder (via la directive `path`)
- l'icône à afficher (via la directive `icon`)
- les personnes autorisées à voir cette vue (via la directive `visible`)
- les badges visibles (via la directive `badge`)
- les cartes (via la directive `cards`) et l'ordre d'affichage de ces cartes (via la directive `!include`)

Les cartes seront listées dans le répertoire [cards](#cards)

## Suivi des modifications

- *27/12/2020* : ajout d'explications
- *25/12/2020* : ajout de l'arborescence
- *15/12/2020* : initialisation des modifications
- *06/12/2020* : initialisation de la recherche
