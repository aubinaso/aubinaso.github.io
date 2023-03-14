---
title: Haproxy Installation
weight: 210
menu:
  notes:
    name: Installation
    identifier: notes-haproxy-installation
    parent: notes-haproxy
    weight: 10
---

<!-- Installation -->
{{< note title="Installation" >}}

L'installation sur un système Linux, on a :
```bash
apt-get install haproxy
```

La configuration se fait dans le fichier **`/etc/haproxy/haproxy.cfg`**

La commande de test suivant nous permettra de voir la version installé : 
```bash
haproxy -v
```

Le fichier **`haproxy.cfg`** permet de faire la configuration de haproxy, et il servira à faire à peu près 95% de la config. Il est sectionné en plusieurs parties :
- global
- default
- frontend
- backend
- listen (qui a pour vocation a remplacé frontend et backend)

Vous aurez plus d'information sur la note dédiée un peu plus en avant.

Les configurations à savoir sont :
- **configuration du daemon** : il se fait dans le fichier **`/etc/sysconfig`**
- **configuration du logrotate** : il se fait en configurant le fichier **`/etc/haproxy/haproxy.cfg`**
- Le repertoire de stockage des données est **`/var/lib/haproxy`**
- Les templates d’erreurs de haproxy sont dans **`/usr/share/haproxy`**. Ces templates pourront nous aider à définir des formats de réponse automatique comme une réponse `404`. On pourra dans un contexte de sécurisation camoufler une erreur `404` avec une page légitime.

{{< /note >}}