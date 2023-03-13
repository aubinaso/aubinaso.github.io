---
title: "Migration vers une nouvelle gamme"
date: 2020-06-08T08:06:25+06:00
description: Informations et Migration to the new game
menu:
  sidebar:
    name: Migration vers une nouvelle gamme
    identifier: rich-content
    parent: sub-category
    weight: 10
hero: images/forest.jpg
tags: ["Markdown","Content Organization","Multi-lingual"]
categories: ["Basic"]
---

Ce poste explique la méthodologie et les bons conseils d'OVH pour la migration vers la nouvelle gamme
- informations sur la nouvelle gamme
- Bonnes pratiques pour une migration

### C'est quoi la nouvelle gamme OVH ?
Les nouveaux VPS OVHcloud offre :
- flexibilité
- performance en hausse de `50%` par rapport à la gamme précédente
- la technologie de stockage utilisée pour la nouvelle gamme est SSD NVMe en raid 1. Les performances seront donc `bien supérieures sur le nouveau VPS`

Selon les spécification d'un VPS, des propositions nous sont données qu'en à la cible VPS.
{{< img src="/posts/CPH/sub-category/rich-content/images/ovh_new_range.png" align="center" title="Ovh new range">}}

{{< vs >}}

### Pourquoi migrer vos données vers la nouvelle gamme
Pour effectuer une migration, voici les prérequis :
- le VPS ne doit pas avoir de disque monté. Si le bouton migrer vers la nouvelle gamme est absente,
vérifier qu'aucun disque n'est monté, s'il y'en a un, démonter le et le bouton réapparaîtra.

### Après la migration
Après la migration, votre nouveau VPS sera configuré comme l’actuel. Vous retrouverez vos adresses IP, vos disques additionnels et votre FTP backup ainsi que l'ensemble de vos options configurées à l'identique.

Une fois la migration réalisée, vous pourrez résilier les options existantes ou en souscrire de nouvelles. `Veuillez noter que ni votre snapshot ni vos sauvegardes automatiques ne seront disponibles`.

### préréquis pour migrer vos données vers la nouvelle gamme
- Aucun préréquis n'est mentionné par OVH quant à la migration
- La migration nous permet de basculer vers une nouvelle offre VPS. La nouvelle facturation prendra effet à l'échéance de votre abonnement
- L'opération prendra de 20 minutes à 6h, dans notre cas, c'est 30 minutes. Dans le cas de disques additionnel, il faut rajouter à ce temps de 2h à 12h
- Durant la migration, le VPS ne sera plus accessible
- **Il faudra avoir assez d'espace disque pour permettre le redémarrage du VPS après la migration**
  - **le premier demarrage nécessite `1Go` d'espace libre sur notre disque système**
- ce n'est pas une obligation de migrer vers la nouvelle gamme, l'annonce de la fin de commercialisation des VPS Cloud, VPS Cloud RAM ou VPS SSD n'entraîne pas l'arrêt de prise en charge de ces solutions

### Best Practices de migration
Les bonnes recommendations sont :
| Configuration actuelle | Configuration recommandée |
|--|--|
| 1-2-10 | 1-2-20 |
| 1-4-20 | 1-4-20 |
| 2-8-40 | 2-8-40 |
| 1-2-25 | 1-2-80 |
| 4-4-50 | 4-8-80 |
| 8-8-100 | 8-8-160 |
| 1-6-25 | 1-4-80 |
| 2-12-50 | 2-8-80 |
| 4-24-100 | 8-8-160 |

[Plus d'informations](https://www.ovhcloud.com/fr/vps/vps-offer-migration/)