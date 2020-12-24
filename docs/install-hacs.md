# Installation de HACS

### Sommaire

- [Pré requis](#pré-requis)
- [Récupérer HACS](#récupérer-hacs)
  - [Lancer HACS](#lancer-hacs)
- [Suivi des modifications](#suivi-des-modifications)

## Pré requis

Avoir installé le partage Samba sur Home Assistant.

## Récupérer HACS

Allez sur le [Github de HACS](https://github.com/hacs/integration/releases/) pour récupérer la dernière release.

Récupérer le fichier `hacs.zip` puis décompressez ce fichier.

Dans le partage Samba, vérifier qu'un répertoire `custom_components` existe. Si ce n'est pas le cas, créez le.

Dans ce répertoire `custom_components`, copiez le répertoire `hacs` qui vient d'être décompressé.

Dans Home Assistant, cliquez sur `File Editor`, puis vérifiez que le répertoire `custom_components` est bien visible et qu'il est bien au même niveau que le fichier `configuration.yaml`.

Allez dans `Configuration` puis `Intégrations`.

> En cours de rédaction

Cocher toutes les cases qui vous indique que vous allez utiliser un logiciel qui ne fait pas parti intégrante de Home Assistant.

Cliquez sur le lien afficher dans la fenêtre et coller la clé fournit par HACS dans la fenêtre Github.

Puis cliquez sur `SOUMETTRE`. J'ai dû redémarrer Home Assistant pour que l'entrée `HACS` dans le menu soit visible.

### Lancer HACS

Dans le menu latéral, cliquez sur `HACS`.

> En cours de rédaction

## Suivi des modifications

- *20/12/2020* : Initialisation
