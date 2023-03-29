---
title: Haproxy Exemple
weight: 25
menu:
  notes:
    name: Exemple
    identifier: notes-haproxy-example
    parent: notes-haproxy
    weight: 25
---

<!-- Example -->
{{< note title="Exemple" >}}

[[_TOC_]]

## Frontend

Avec Haproxy, on peut définir plusieurs frontend et cette capacité nous permet de mutualisé ce service. Un exemple de frontend minimaliste est :

```bash
frontend myapp_front
    bind *:80
    default_backend myapp_back
```

Le mot clé `frontend` permet de définir un nouveau frontend. L'indentation est très important dans la rédaction d'un fichier Haproxy. Dans **frontend**, on pourra définir des paramètres dont les plus importants sont :
- `bind` : ici la valeur `*:80` a été donné. `*` spécifie qu'on souhaite écouter sur tous les ip de la machine sur lequel tourne le service haproxy. C'est également possible de définir un ip précis. On aura par exemple : `bind 10.0.0.1:80`
- `default_backend` : est une variable imposée, il spécifie le backend correspondant. La valeur donnée est le **nom d'un backend qui a été défini**

## Backend
    
La définition d'un backend est comme suit :
```bash
backend myapp_back
    server server1 10.0.0.1:80
```

Le mot clé `backend` permet de définir un backend. Comme paramètre, on peut spécifier les serveurs qu'on aimerait lié avec le mot clé `server`.
Dans le cas où on a plusieurs serveurs dans le backend, il est possible de spécifier un algorithme de loadbalancing avec le mot clé `balance`. Dans cet exemple, nous allons utiliser un algorithme de **Round Robin**
On retrouve alors la configuration suivante :

```bash
backend myapp_back
    balance roundrobin
    server server1 10.0.0.1:80
    server server2 10.0.0.2:5000
```

L'algorithme de **Round Robin** est l'algorithme par défaut utiliser lorsque ce paramètre n'est pas précisé.

Au final, nous obtenons le fichier suivant :

```bash
global
    log /dev/log local5 debug
    chroot /var/lib/haproxy
    stats socket /run/haproxy/admin.sock mode 660 level admin
    stats timeout 30s
    user haproxy
    group haproxy
    daemon

defaults
    log global
    mode http
    option httplog
    option dontlognull
    timeout connect 5000
    timeout client 50000
    timeout server 50000
    errorfile 400 /etc/haproxy/errors/400.http

frontend myapp_front
    bind *:80
    default_backend myapp_back

backend myapp_back
    balance roundrobin
    server server1 10.0.0.1:80
    server server2 10.0.0.2:5000
```

{{< /note >}}