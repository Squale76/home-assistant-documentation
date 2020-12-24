# Installation de Zigbee

### Sommaire

- [Ajout d'un utilisateur MQTT](#ajout-dun-utilisateur-mqtt)
- [Installation](#installation)
  - [Ajout du broker](#ajout-du-broker)
  - [Ajout de zigbee2mqtt](#ajout-de-zigbee2mqtt)
  - [Ajout de l'assistant](#ajout-de-lassistant)
- [Intégration](#intégration)
  - [Ajouter un matériel](#ajouter-un-matériel)
  - [Renommer un matériel](#renommer-un-matériel)
- [Suivi des modifications](#suivi-des-modifications)

J'ai suivi ce tuto [Zigbee2MQTT, monter, intégrer, monitorer](https://hacf.fr/integrer-le-cc2531-via-zigbeetomqtt-sur-home-assistant/).

Quelques remarques :

- pour installer les drivers sur mon PC en Win10, j'ai dû passer par le gestionnaire des périphériques pour mettre à jour les pilotes du ***CC2531*** et ***CC Debugger*** sans quoi le ***CC2531*** n'était pas visible dans ***SmartRF Flash Programmer***.

## Ajout d'un utilisateur MQTT

Dans le menu latéral, cliquez sur `Configuration` puis `Utilisateurs`.

Cliquez sur le bouton en bas à droite `AJOUTER UN UTILISATEUR`.

Puis renseignez les informations :

- `Nom`: Indiquer le nom "humain" de l'utilisateur MQTT
- `Nom d'utilisateur`: Indiquer le login de l'utilisateur MQTT
- `Mot de passe`: Indiquer le mot de passe de l'utilisateur MQTT
- `Confirmer le mot de passe`: retaper le mot de passe
- `Administrateur`: ne pas cocher

## Installation

### Ajout du broker

[Ajouter un serveur MQTT a Home Assistant via l’addons Mosquito Broker](https://forum.hacf.fr/t/ajouter-un-serveur-mqtt-a-home-assistant-via-laddons-mosquito-broker/225)

Via `Supervisor`, puis `Add-on Store`, cliquez sur `Mosquitto broker`.

Cliquez sur `INSTALL`.

Dans `Configuration`, remplacer :

```yaml
logins: []
```

par :

```yaml
logins:
  - username: <le user MQTT>
    password: <le mot de pass du user MQTT>
```

Puis cliquez sur `SAVE`.

Dans l'onglet `Info`, on clique sur `START` puis on surveille les logs.

Pour configurer MQTT, dans le menu latéral, cliquez sur `Configuration`, puis `Intégrations` puis sur la carte `MQTT`, cliquer sur `CONFIGURER`.

Cocher `Activer la découverte` puis cliquer sur `SOUMETTRE`.

### Ajout de zigbee2mqtt

Ajouter un add-on non officiel, via `Supervisor`, puis `Add-on Store`, cliquez sur le 3 boutons en haut à droite.

Cliquez sur `Repositories`, dans `Add repository`, collez l'url <https://github.com/danielwelch/hassio-zigbee2mqtt> puis cliquez sur `ADD` puis sur `CLOSE`.

Recherchez `zigbee2mqtt`, **ATTENTION** pas ~~`zigbee2mqtt Edge`~~.

Cliquez sur `zigbee2mqtt`, puis cliquez sur `INSTALL`.

Cliquez sur `Configuration`, puis modifier les informations suivantes :

```yaml
mqtt:
  base_topic: zigbee2mqtt
  server: 'mqtt://core-mosquitto'
  user: <le user MQTT>
  password: <le mot de pass du user MQTT>
```

Cliquez sur `SAVE`.

Cliquez sur `START` et suivre les logs.

### Ajout de l'assistant

Ajouter un add-on non officiel, via `Supervisor`, puis `Add-on Store`, cliquez sur le 3 boutons en haut à droite.

Cliquez sur `Repositories`, dans `Add repository`, collez l'url <https://github.com/yllibed/hassio> puis cliquez sur `ADD` puis sur `CLOSE`.

Recherchez `zigbee2mqttassistant`, cliquez sur `zigbee2mqttassistant`, puis cliquez sur `INSTALL`.

Cliquez sur `Configuration`, puis modifier les informations suivantes :

```yaml
settings:
  mqttserver: addon_core_mosquitto
  mqttusername: <le user MQTT>
  mqttpassword: <le mot de pass du user MQTT>
```

Cliquez sur `SAVE`.

Cliquez sur `START` et suivre les logs.

## Intégration

### Ajouter un matériel

Pour autoriser l’ajout d’un matériel, dans `zigbee2mqttassistant`, cliquez sur l'nglet `Statut` puis cliquer sur `ALLOW NEW DEVICES TO JOIN NETWORK` puis effectuez la manipulation d’appairage de votre devices.

Une fois l’appairage fait cliquez sur l'onglet `Devices`, vous devriez voir apparaitre votre nouvel matériel.

Une fois vos matériels associés, rendez vous dans le menu latéral, cliquez sur `Configuration`, puis sur `Intégrations` puis MQTT.

Cliquer sur la roue dentée en haut droite.

Renseigner un nom plus humain, puis la pièce dans laquelle sera votre device.

Cliquer sur `METTRE A JOUR` puis dans la fenêtre d’après cliquer sur `RENOMMER` pour renommer les entités associées.

### Renommer un matériel

le menu latéral, cliquez sur `Configuration`, puis sur `Appareils`, cliquer sur l'appareil à renommer.

Ce n’est pas fini car actuellement c’est seulement le Friendly Name que nous avons modifié.

Dans Entités, cliquer sur chacune d’elles et remplacer si besoin dans ID d’entité. Vous pouvez aussi modifier l’icône par une autre du site Material Design.

NOTA : Il ne faut pas supprimer ce qu’il y a avant le . (sensor, binary_sensor, etc) et votre nom ne doit contenir que des minuscule, chiffres et _. Il ne doit pas contenir d’espace, de caractère accentué, etc.

## Suivi des modifications

- *21/12/2020* : Ajout du broker MQTT, de l'utilisateur & de l'intégration
