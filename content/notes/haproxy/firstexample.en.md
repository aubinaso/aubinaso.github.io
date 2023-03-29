---
title: Haproxy Example
weight: 25
menu:
  notes:
    name: Exemple
    identifier: notes-haproxy-example
    parent: notes-haproxy
    weight: 25
---

<!-- Example -->
{{< note title="Example" >}}

[[_TOC_]]

## Frontend

With Haproxy, we can define several frontends and this ability allows us to mutualise this service. An example of a minimalist frontend is :

```bash
frontend myapp_front
    bind *:80
    default_backend myapp_back
```

The `frontend` keyword is used to define a new frontend. Indentation is very important when writing a Haproxy file. In **frontend**, you can define parameters, the most important of which are :
- `bind` : Here the value `*:80` has been given. `*` specifies that we want to listen on all ip's of the machine on which the haproxy service is running. It is also possible to specify a specific ip. For example: `bind 10.0.0.1:80`.
- `default_backend` : is a forced variable, it specifies the corresponding backend. The given value is the **name of a backend that has been defined**.

## Backend
    
The definition of a backend is as follows :

```bash
backend myapp_back
    server server1 10.0.0.1:80
```

The `backend` keyword is used to define a backend. As a parameter, one can specify the servers one would like to link with the `server` keyword.
In the case of multiple servers in the backend, it is possible to specify a load balancing algorithm with the `balance` keyword. In this example, we will use a **Round Robin** algorithm.
The configuration is as follows:

```bash
backend myapp_back
    balance roundrobin
    server server1 10.0.0.1:80
    server server2 10.0.0.2:5000
```

The **Round Robin** algorithm is the default algorithm to use when this parameter is not specified.

In the end, we obtain the following file :

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