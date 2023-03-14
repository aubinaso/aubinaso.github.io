---
title: Haproxy Introduction
weight: 210
menu:
  notes:
    name: Introduction
    identifier: notes-haproxy-introduction
    parent: notes-haproxy
    weight: 10
---

**Haproxy** est un outil utilisé pour faire du service discovery. Ses caractéristiques sont :
- il sert de **proxy** et est **stateful**
- il fait du **stickyness** en maintenant un client au même serveur de backend.
- il sert de **Loadbalancer** et fait du **High Availability** avec 9 algorithmes de LoadBalancing
  - Round Robin
  - Least
  - First
  - Source
  - URI
  - HDR
  - ...
- il facilite ainsi la sécurisation et la mise en place du SSL
- il permet de faire de la **translation d'adresse et de port**
- il est multi-protocole et facilite la configuration en terme de timeout
- il permet de faire du **forwarding**
- il comprend un **système de monitoring**
- il permet de faire du **service reload**
- il permet de faire du **spof** avec l'outil **keepAlive**
- il permet de faire du **slow start**
- il permet de faire du **stickyness**
- il permet de faire de la **réécriture d'url**
- il est utilisé pour faire du **service discovery**
