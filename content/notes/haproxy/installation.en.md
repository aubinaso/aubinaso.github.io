---
title: Haproxy Installation
weight: 20
menu:
  notes:
    name: Installation
    identifier: notes-haproxy-installation
    parent: notes-haproxy
    weight: 20
---

<!-- Installation -->
{{< note title="Installation" >}}

Installing on a Linux system, we have:
```bash
apt-get install haproxy
```

The configuration is done in the file **`/etc/haproxy/haproxy.cfg`**

The following test command will allow us to see the installed version: 
```bash
haproxy -v
```

The **`haproxy.cfg`** file is where the haproxy configuration is done, and it will be used to do about 95% of the config. It is divided into several parts:
- global
- default
- frontend
- backend
- listen (which is intended to replace frontend and backend)

You will have more information on the dedicated note a little further.

The configurations to know are :
- **daemon configuration** : it is done in the file **`/etc/sysconfig`**
- **logrotate configuration** : it is done by configuring the file **`/etc/haproxy/haproxy.cfg`**
- The data storage directory is **`/var/lib/haproxy`**
- The haproxy error templates are in **`/usr/share/haproxy`**. These templates can help us define automatic response formats such as a `404` response. In a security context, a `404` error can be disguised with a legitimate page.

{{< /note >}}