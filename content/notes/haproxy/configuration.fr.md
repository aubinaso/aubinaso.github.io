---
title: Haproxy Configuration
weight: 20
menu:
  notes:
    name: Configuration
    identifier: notes-haproxy-configuration
    parent: notes-haproxy
    weight: 20
---

<!-- Configuration -->
{{< note title="Configuration" >}}

Haproxy fonctionne en **frontend** et redirige les requêtes vers un ensemble de ressources en **backend**. Pour configurer ce service, il faudra tout d'abord lui demander d'écouter sur :
- une IP
- un Port
- une URL
Cette configuration est celle du **frontend**. Par la suite, il faudra configurer le backend où on précisera des ressources telles que les serveurs... On pourra préciser plusieurs services et définir le type de **LoadBalancing** qui sera appliqué.
C'est également possible d'appliquer des règles spécifiques, de rajouter des headers sur les requêtes qui seront redirigées vers les services de backend. Le plus important à retenir jusqu'ici est le principe de frontend et de backend.
Vous pouvez consulter plus de documentation sur le [site officiel](https://docs.haproxy.org/dev/configuration.html).

Exemple : Soit un client qui fait une requête  sur le listener du Haproxy c'est-à-dire que la requête arrive sur le frontend. Cette requête sera redirigé vers un backend si elle vérifie certaines condition du frontend spécifique. Ensuite, on aura un chemin. Les étapes :
- **frontend** : IP/URL/Port d'écout tel que défini dans la configuration du haproxy. C'est possible d'avoir plusieurs frontend. Ici, la requête est arrivée sur une URL ou un IP précis et sur un port précis (443, 80...)
- **application des règles** : des règles sont appliquées pour déterminer le frontend correspondant à la requête cliente. Par la suite une décision sera faite :
  - la requête peut être `bloquée`
  - la requête peut être `modifiée` c'est-à-dire que des entêtes peuvent être ajoutées ou enlevées ou modifiée...
  - ...
- une règle de redirection du frontend vers le backend
- Dans le backend, une décision de LoadBalancing peut être appliquée. Des règles en place permettront de choisir le serveur vers qui redirigé la requête
- un chemin retour
- journalisation des échanges

    Dans le fichier de configuration de Haproxy, on note 2 partie :
- section `Global`
- section `Default`
## Global
Cette section correspond aux paramètres du service haproxy. Un exemple est définie comme suit :
```bash
global
    log /dev/log local5 debug
    chroot /var/lib/haproxy
    stats socket /run/haproxy/admin.sock mode 660 level admin
    stats timeout 30s
    user haproxy
    group haproxy
    daemon
```
Une pétite explication de ces paramètres :
- **log** : c'est la façon donc haproxy va s'occuper de la journalisation
- **chroot** : la sécurité de haproxy
- **stats** : pour permettre d'interargir avec haproxy avec des outils tiers notamment `hatop` pour configurer haproxy en GUI. Il permet aussi de définir le **timeout** qui est le temps de durer d'une connexion
- **user** : l'utilisateur du service haproxy
- **group** : groupe correspondant
- **daemon** : ce mode permet à haproxy de s'exécuter en tant que service.
- eventuellement le **ssl**...

## Default
Cette section s'applique si aucune configuration n'est précisée (définition d'un frontend et d'un backend pour une requête précise).
Il est comme suit :
```bash
defaults
    log global
    mode http
    option httplog
    option dontlognull
    timeout connect 5000
    timeout client 50000
    timeout server 50000
    errorfile 400 /etc/haproxy/errors/400.http
```
On a donc :
- **log global** : journalisation vers syslog ou suivant la définition de la section `global`
- **mode http** : protocole de LoadBalancing. Il est possible de définir autre chose notamment tcp, smtp...
- **option** : permet de préciser la nécessité de journalisation de certaines options
  - **option httplog**
  - **option dontlognull** : spécifie qu'il ne faut pas journaliser lorsque les requêtes sont nulles
- **timeout connect** : spécifie le durée d'essaie de connexion avec le **backend**. Ce temps est en **ms**. Après ce temps, si le serveur ne répond pas, on considère le serveur indisponible.
- **timeout client/server**
- **errorfile** : permet de spécifier le fichier d'erreur qui devra être affichée en cas d'erreur

Lorsqu'on a rédiger un fichier de configuration haproxy, il est possible de tester la configuration avec la commande :
```bash
haproxy -c -f [myconfig_file.conf]
```
Exemple :
```bash
haproxy -c -f /etc/haproxy/haproxy.conf
```
C'est important de faire ce test pour un nouveau fichier de configuration haproxy avant de remplacer le fichier par défaut.

{{< /note >}}