---
title: Haproxy Options
weight: 30
menu:
  notes:
    name: Options
    identifier: notes-haproxy-options
    parent: notes-haproxy
    weight: 30
---

<!-- Options -->
{{< note title="Options" >}}

Haproxy a beaucoup d'options que nous pouvons utilise, il s'agit notamment de :
- **ACL** qui permet de mieux gérer les requêtes entrantes et les regiriger vers certains server de backend
- **Forwrad for** qui permet de transporter l'IP du client responsable de la requête entre le serveur Haproxy et le serveur de backend. Dans ce cas, Haproxy ne remplamcera plus l'ip du client par son ip.
- ...

Dans cette partie, nous allons juste voir comment implémenter des **ACL**, je vous recommande de vous rendre sur la documentation Haproxy pour plus d'informations sur ses fonctionnalités.
Une **ACL** permet un meilleur filtrage et redirection des requêtes reçues au niveau du frontend. On peut notamment les filtrer suivant l'URL, ce que nous allons faire dans cet exemple...
Pour un filtrage en fonction de 2 url à savoir : `mct.aubinaso.fr` et `www.aubinaso.fr`, on aura la configuration du frontend suivant :
```bash
frontend myapp_front
    bind *:80
    mode http

    acl myapp_front1 hdr_dom(host) -i mct.aubinaso.fr
    use_backend mybackend1 if myapp_front1

    acl myapp_front2 hdr_dom(host) -i www.aubinaso.fr
    use_backend mybackend2 if myapp_front2
```

La ligne `mode http` informe qu'il s'agit d'une acl appliquée à la couche 7. Nous avons rajouté 2 entrées pour loadbalancer sur 2 ACL. Les urls sont `mct.aubinaso.fr` et `www.aubinaso.fr`. nous créons donc 2 règles acl avec pour nom **myapp_front1** et **myapp_front2**. Le mot clé `hdr_dom(host)` recupère les URL de la requête et en fonction de l'url, le client sera redirigé sur **mybackend1** ou **mybackend2**.

{{< /note >}}