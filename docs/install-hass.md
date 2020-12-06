# Installation de Home Assistant

### Sommaire

- [Suivi des modifications](#suivi-des-modifications)

J'ai tout d'abord essayé d'installer HA via la méthode la plus simple via ***HassOS*** en suivant ce tuto [Installer Home Assistant sur Raspberry Pi (ou autre SBC) via HassOS](https://forum.hacf.fr/t/installer-home-assistant-sur-raspberry-pi-ou-autre-sbc-via-hassos/201).

Mais, le boot sur mon disque dur n'a pas fonctionné. Je pense que mon boîtier HDD n'était pas compatible, pour ceux qui n'ont pas encore acheté le leur, voici une liste des [boîtiers compatibles](https://jamesachambers.com/raspberry-pi-4-usb-boot-config-guide-for-ssd-flash-drives/)

J'ai donc testé la solution via ***Docker supervised***. J'ai installé le boot de mon RPi sur le SDD en suivant ce tuto [Démarrer son Raspberry Pi 4 sur SSD](https://forum.hacf.fr/t/demarrer-son-raspberry-pi-4-sur-ssd/674) puis celui-ci pour installer HA sur Docker [Installer Home Assistant sur Raspberry Pi (ou autres SBC), Debian (Méthode Docker avec Supervisor)](https://forum.hacf.fr/t/installer-home-assistant-sur-raspberry-pi-ou-autres-sbc-methode-docker-avec-supervisor/676)

Un vrai bonheur !

## Suivi des modifications

*00/00* : 
