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

Haproxy has many options that we can use, including :
- **ACL** which allows us to better manage incoming requests and redirect them to certain backend servers
- **Forwrad for** which allows to transport the IP of the client responsible for the request between the Haproxy server and the backend server. In this case, Haproxy will no longer replace the client's ip with its ip.
- ...

In this section, we'll just look at how to implement **ACL**, I recommend that you visit the Haproxy documentation for more information on its features.
An **ACL** allows a better filtering and redirection of the requests received at the frontend level. It is possible to filter them according to the URL, which is what we will do in this example...
For a filtering according to 2 urls, namely: `mct.aubinaso.fr` and `www.aubinaso.fr`, we will have the following frontend configuration:
```bash
frontend myapp_front
    bind *:80
    mode http

    acl myapp_front1 hdr_dom(host) -i mct.aubinaso.fr
    use_backend mybackend1 if myapp_front1

    acl myapp_front2 hdr_dom(host) -i www.aubinaso.fr
    use_backend mybackend2 if myapp_front2
```

The line `http mode` informs that this is an acl applied to layer 7. We have added 2 entries for loadbalancer on 2 ACLs. The urls are `mct.aubinaso.co.uk` and `www.aubinaso.fr`. So we create 2 acl rules with names **myapp_front1** and **myapp_front2**. The keyword `hdr_dom(host)` retrieves the URLs of the request and depending on the url, the client will be redirected to **mybackend1** or **mybackend2**.

{{< /note >}}