---
title: "Migration to New Range"
date: 2023-03-13T08:06:25+06:00
description: Informations et Migration to the new game
menu:
  sidebar:
    name: Migration to New Range
    identifier: rich-content
    parent: sub-category
    weight: 10
hero: images/forest.jpg
tags: ["Markdown","Content Organization","Multi-lingual"]
categories: ["Basic"]
---

This post explains the methodology and good advice from OVH for the migration to the new range

- information on the new range
- Best practices for a Migration

### What is the new OVH range?
The new OVHcloud VPS offers :
- flexibility
- 50% performance increase compared to the previous range
- the storage technology used for the new range is NVMe SSD in raid 1, so the performance will be `much better on the new VPS`.

According to the specification of a VPS, proposals are given to us as to the target VPS.
{{< img src="images/ovh_new_range.png" align="center" title="Ovh new range">}}

{{< vs >}}

### Pourquoi migrer vos données vers la nouvelle gamme
To perform a migration, here are the prerequisites:
- the VPS must not have a disk mounted. If the migrate to new range button is missing,
check that no disk is mounted, if there is one, remove it and the button will reappear.

### Après la migration
After the migration, your new VPS will be configured like the current one. You will find your IP addresses, your additional disks and your FTP backup as well as all your options configured identically.

Once the migration is complete, you will be able to cancel your existing options or subscribe to new ones. Please note that neither your snapshot nor your automatic backups will be available.

### préréquis pour migrer vos données vers la nouvelle gamme
- No prerequisites are mentioned by OVH for the migration
- The migration allows us to switch to a new VPS offer. The new billing will take effect at the end of your subscription
- The operation will take from 20 minutes to 6 hours, in our case, it is 30 minutes. In the case of additional disks, you need to add to this time 2h to 12h
- During the migration, the VPS will no longer be accessible
- You will need to have enough disk space to allow the VPS to restart after the migration
  - the first boot requires `1GB` of free space on our system disk** **it is not a requirement to have a VPS
- it is not an obligation to migrate to the new range, the announcement of the end of marketing of VPS Cloud, VPS Cloud RAM or VPS SSD does not lead to the end of support for these solutions

### Best Practices de migration
The correct recommendations are :
| Current configuration | Recommended configuration |
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

[More information](https://www.ovhcloud.com/fr/vps/vps-offer-migration/)