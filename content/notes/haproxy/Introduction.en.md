---
title: Haproxy Introduction
weight: 210
menu:
  notes:
    name: Introduction
    identifier: notes-haproxy-introduction
    parent: notes-haproxy
    weight: 10
---

<!-- Introduction -->
{{< note title="Introduction" >}}

**`Haproxy`** is a tool used for service discovery. Its features are :
- it acts as a **`proxy`** and is **`stateful`**.
- it does **`stickyness`** by maintaining a client at the same backend server.
- it serves as a **`Loadbalancer`** and does **`High Availability`** with 9 LoadBalancing algorithms
  - Round Robin
  - Least
  - First
  - Source
  - URI
  - HDR
  - ...
- it facilitates security and the implementation of SSL
- it allows **`address and port translation`** to be performed
- it is multi-protocol and facilitates configuration in terms of timeout
- it allows for **`forwarding`**
- it includes a **`monitoring system`**.
- it allows for **`service reload`**
- it allows **`spof`** with the **`keepAlive`** tool
- it allows for **`slow start`**
- it allows you to do **`stickyness`**
- it allows you to do **`url rewriting`**
- it is used to do **`service discovery`**

{{< /note >}}