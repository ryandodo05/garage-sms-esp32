# Projet : Carte ESP32 + SIM7080G, pilotage d'une porte de garage par SMS

Carte PCB ESP32 avec module SIM7080G, relais et capteur ultrason, pour surveiller
et piloter une porte de garage par SMS.

Auteur : Ryan, https://ryan-dodo.be/Projet1.html

## Description

Le but du projet est de surveiller et piloter à distance plusieurs éléments de mon
domicile, principalement ma porte de garage. Le cœur de la carte est un ESP32,
complété par un module SIM7080G qui assure la communication cellulaire par SMS.

- **Porte de garage** : une broche de l'ESP32 est reliée à l'entrée du boîtier de
  gestion de la porte. Un SMS contenant « Garage » envoie une impulsion : si la
  porte est fermée, elle s'ouvre, et inversement.
- **Détection de voiture** : un capteur ultrason HC-SR04 (portée d'environ 5 mètres)
  est fixé au mur du garage. En réponse au SMS « Garage », il indique si une voiture
  est garée ou non.
- **Pilotage de charges** : deux relais permettent de commuter du 12 V. Comme la
  sortie de l'ESP32 ne fournit pas assez de tension ni de courant pour la bobine,
  chaque relais est commandé par un transistor et des résistances. Un SMS tel que
  « relai1 » active le relais 1, par exemple pour alimenter un spot LED.
- **Sécurité** : seuls les SMS envoyés depuis mon numéro de téléphone sont pris en
  compte. Tout message provenant d'un autre numéro est ignoré.

## Fonctionnalités

- Ouverture / fermeture de la porte de garage par SMS (impulsion sur broche dédiée)
- Détection de présence de voiture par capteur ultrason HC-SR04 (~5 m)
- Réponse par SMS : voiture garée ou garage libre
- Commande de deux relais 12 V par SMS (ex. « relai1 », « relai2 »)
- Commande des relais via transistors et résistances de base
- Filtrage des commandes : acceptées uniquement depuis mon numéro
- Communication cellulaire LTE-M avec le module SIM7080G
- PCB conçue entièrement par mes soins sous Eagle

## Caractéristiques

| Élément | Détail |
|---|---|
| Microcontrôleur | ESP32 |
| Communication | SIM7080G (LTE-M uniquement) |
| Sorties | 2 relais 12 V, pilotés par transistor |
| Capteur | HC-SR04, portée ~5 m |
| Commande porte | Impulsion sur broche dédiée |
| Conception | PCB dessinée par mes soins, fabriquée chez JLCPCB |

## Conception & fabrication

La carte a été entièrement conçue par mes soins sous Eagle (schéma, placement et
routage). Les fichiers Gerber ont été exportés puis la carte est fabriquée chez
JLCPCB, afin de limiter au maximum le risque de défaut de fabrication.

## Coûts indicatifs

| Élément | Prix |
|---|---|
| ESP32 | 13 € |
| Relais (unité) | 3 € |
| Module SIM7080G | 56 € |
| Reste des composants (transistors, résistances, capteur HC-SR04, connecteurs, PCB…) | 30 à 40 € |
| Abonnement SIM Orange (LTE-M), SMS illimités entrants et sortants | 15 € / mois |

La SIM doit être en LTE-M, car le module SIM7080G n'accepte que cette technologie.
Le forfait choisi permet d'envoyer et de recevoir autant de messages que souhaité.

## Vue 3D de la PCB

Voir la vue 3D interactive (chargement des Gerbers) sur
https://ryan-dodo.be/Projet1.html

<!-- ![Vue 3D de la PCB](images/pcb-3d.png) -->

## Défis rencontrés

Le placement des composants RF du SIM7080G (antenne, découplage, masse) a demandé
une attention particulière pour limiter les interférences avec le reste de la carte.
La commande des relais 12 V a également nécessité l'ajout de transistors, car la
sortie de l'ESP32 ne suffit pas à alimenter directement les bobines.
