# Installation de la téléinfo via WiFi

### Sommaire

- [Recherches](#recherches)
- [ESPHome et flashage ESP32](#esphome-et-flashage-esp32)
- [Réalisation du shield](#réalisation-du-shield)
- [Configuration pour la téléinfo](#configuration-pour-la-téléinfo)
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

Reste à configurer mon ESP32 pour qu'il puisse lire la téléinfo ...
Je crois que je ne vais pas pouvoir attendre les plaques de prototypage et je vais me lancer sur une breadboard ...

## Suivi des modifications

*00/00* : xxx
