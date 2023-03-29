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

Haproxy works in **frontend** and redirects requests to a set of resources in **backend**. To configure this service, you must first ask it to listen on :
- an IP
- a Port
- a URL
This is the configuration of the **frontend**. Afterwards, we will have to configure the backend where we will specify resources such as servers... You can specify several services and define the type of **LoadBalancing** that will be applied.
It is also possible to apply specific rules, to add headers on the requests which will be redirected towards the backend services. The most important thing to remember so far is the principle of frontend and backend.
You can read more documentation on the [official website](https://docs.haproxy.org/dev/configuration.html).

Example: A client makes a request to the Haproxy listener, i.e. the request arrives on the frontend. This request will be redirected to a backend if it checks some specific frontend condition. Then we will have a path. The steps :
- **frontend**: IP/URL/listening port as defined in the haproxy configuration. It is possible to have several frontends. Here, the request arrived on a precise URL or IP and on a precise port (443, 80...)
- **Application of rules**: rules are applied to determine the frontend corresponding to the client request. Then a decision will be made:
  - the request can be `blocked`
  - the request can be `modified` i.e. headers can be added or removed or modified...
  - ...
- a redirection rule from the frontend to the backend
- In the backend, a LoadBalancing decision can be applied. Rules are in place to choose the server to which the request is redirected
- a way back
- logging of exchanges

    In the Haproxy configuration file, we note 2 parts:
- `Global` section
- `Default` section
## Global
This section corresponds to the parameters of the haproxy service. An example is defined as follows:
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
A short explanation of these parameters:
- **log** : this is how haproxy will handle the logging
- **chroot** : the security of haproxy
- **stats** : to allow interarguing with haproxy with third party tools including `hatop` to configure haproxy in GUI. It also allows you to set the **timeout**, which is the length of time a connection will last
- **user** : the user of the haproxy service
- **group**
- **daemon** : this mode allows haproxy to run as a service.
- possibly **ssl**...

## Default
This section applies if no configuration is specified (definition of a frontend and a backend for a specific request).
It is as follows:
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
- **log global** : logging to syslog or as defined in the `global` section
- **mode http** : LoadBalancing protocol. It is possible to define other protocols such as tcp, smtp...
- **option** : allows you to specify the need to log certain options
  - **option httplog**
  - **option dontlognull** : specifies not to log when requests are null
- **timeout connect** : specifies the time to try to connect to the **backend**. This time is in **ms**. After this time, if the server does not respond, the server is considered unavailable.
- **timeout client/server**
- **errorfile** : allows you to specify the error file that should be displayed in case of an error

When you have written a haproxy configuration file, you can test the configuration with the command :
```bash
haproxy -c -f [myconfig_file.conf]
```
Example:
```bash
haproxy -c -f /etc/haproxy/haproxy.conf
```
It is important to do this test for a new haproxy configuration file before replacing the default file.

{{< /note >}}