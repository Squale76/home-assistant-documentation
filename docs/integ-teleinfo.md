# Installation de la téléinfo via WiFi

### Sommaire

- [Recherches](#recherches)
- [ESPHome et flashage ESP32](#esphome-et-flashage-esp32)
- [Réalisation du shield](#réalisation-du-shield)
- [Configuration pour la téléinfo](#configuration-pour-la-téléinfo)
  - [Flashage de mon ESP32](#flashage-de-mon-esp32)
  - [Intégration dans une carte Lovelace](#intégration-dans-une-carte-lovelace)
- [Reste à faire](#reste-à-faire)
- [Suivi des modifications](#suivi-des-modifications)

## Recherches

En préparation sur ce fil de [discussion](https://forum.hacf.fr/t/teleinfo-via-wifi/1077/)...

## ESPHome et flashage ESP32

Suite à la réception de mes ESP32, j'ai flashé mon 1er en suivant ce tuto [Installer ESPHome sur Home Assistant et créer votre première configuration](https://forum.hacf.fr/t/installer-esphome-sur-home-assistant-et-creer-votre-premiere-configuration/223)

[u]Quelques remarques :[/u]

- Mon ESP32 n'était effectivement pas reconnu sous Win10, il a fallu installé les drivers qui se trouvent sur le site de [silabs.com](https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers)
- Après le flashage, dans ESPHome, j'ai vu dans les logs de mon nouveau device :

  ```logs
  WARNING Error resolving IP address of teleinfo.local. Is it connected to WiFi?
  WARNING (If this error persists, please set a static IP address: https://esphome.io/components/wifi.html#manual-ips)
  WARNING Initial connection failed. The ESP might not be connected to WiFi yet (Error resolving IP address: Error resolving address with mDNS: Did not respond. Maybe the device is offline., [Errno -2] Name or service not known). Re-Trying in 1 seconds
  ```

  Je suis donc aller voir à l'adresse indiquée <https://esphome.io/components/wifi.html#manual-ips)> pour ajouter une adresse IP statique à mon ESP32.
  J'ai ajouté un bail statique depuis l'interface de ma freebox pour être sûr.

## Réalisation du shield



## Configuration pour la téléinfo

### Flashage de mon ESP32

Reste à configurer mon ESP32 pour qu'il puisse lire la téléinfo ...
Je crois que je ne vais pas pouvoir attendre les plaques de prototypage et je vais me lancer sur une breadboard ...

Via Samba, je me suis connecté au partage puis copié le fichier `my_tic_component.h` que l'on peut trouver sur le [repository](https://github.com/schmurtzm/Teleinfo-TIC-with-ESPhome/blob/master/my_tic_component.h) de Schmurtzm.

> **Attention** : bien copier le code **RAW** et pas comme moi la première fois `Enregistrer le lien sous...`

Dans ESPHome, j'ai copié le contenu RAW du fichier `ESP32.yaml` en modifiant les données personnelles :

> je n'ai mis **QUE** les données que j'ai modifiées

```yaml
esphome:
  name: teleinfo
  board: nodemcu-32s

wifi:
  # Optional manual IP
  manual_ip:
    static_ip: <IP de l'ESP32>
    gateway: <IP de ma gateway>
    subnet: <masque de sous réseau>


  # Enable fallback hotspot (captive portal) in case wifi connection fails
  ap:
    ssid: "Teleinfo Fallback Hotspot"
    password: !secret ap_pass
#  domain: .local           # Problème d'accès avec cette configuration
#  power_save_mode: LIGHT   # Problème d'accès avec cette configuration
#  fast_connect: false      # Problème d'accès avec cette configuration
#  reboot_timeout: 15min    # Problème d'accès avec cette configuration
#  use_address: tic.local   # Problème d'accès avec cette configuration

# Enable Home Assistant API
api:
  password: !secret ota_pass

ota:
  password: !secret ota_pass
  
# ajout du composant uart pour la communication série avec la sortie TIC du compteur
uart:
  tx_pin: GPIO1     # J'ai utilisé l'UART 0 au lieu de l'UART 2
  rx_pin: GPIO3     # J'ai utilisé l'UART 0 au lieu de l'UART 2
```

Clique sur `SAVE`, puis `CLOSE`, clique sur `VALIDATE` pour vérifier la validité de mon code. Puis `UPLOAD` pour mettre à jour mon ESP32...........

### Intégration dans une carte Lovelace

`Configuration`, puis `AJOUTER L'INTEGRATION`, je recherche `ESPHome` et clique dessus.

Dans la nouvelle fenêtre, je renseigne l'adresse IP fixe de mon ESP32 en laissant le port par défaut `6053`, puis clique sur `SOUMETTRE`.

Une nouvelle carte `ESPHome` apparait avec 9 entités.

![entités téléinfo](resources/install-teleinfo_entites.png)

Dans le dashboard de Home Assistant choisi pour accueillir ces nouvelles infos, un clic sur `Modifier le tableua de bord`

![Modifier le dashboard](resources/install-teleinfo_modifier-dashboard.png)

Clique sur `AJOUTER UNE ACTION`, j'ai choisi la carte `Capteur` et dans `Entité`, j'ai choisi `Puissance` ou plutôt `sensor.puissance` puis `ENREGISTRER`

Et voilà, un suivi de la puissance utilisée.

## Reste à faire

- Modifier la fréquence de mise à jour de la courbe de suivi de la puissance (pas assez réactive à mon goût).
- Vérifier pourquoi l'index passe à zéro sur le graphique.
- Sauvegarder les informations dans InfluDB pour avoir un meilleur historique.
- Afficher via Grafana un plus joli graphique.

## Suivi des modifications

*07/12/2020* : Intégrations du code de suivi de la téléinfo
*04/12/2020* : Flashage de l'ESP32 pour OTA via WiFi
