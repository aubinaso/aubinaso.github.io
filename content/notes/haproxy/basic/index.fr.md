---
title: Variables en Haproxy
weight: 10000
menu:
  notes:
    name: Variables
    identifier: notes-haproxy-variables
    parent: notes-haproxy
    weight: 10000
---

<!-- Variable -->
{{< note title="Variable" >}}

```bash
NOM="John"
echo $NOM
echo "$NOM"
echo "${NOM}
```

{{< /note >}}

<!-- Condition -->
{{< note title="Condition" >}}

```bash
if [[ -z "$chaine" ]]; then
  echo "La chaine est vide"
elif [[ -n "$chaine" ]]; then
  echo "La chaine est vide"
fi
```

{{< /note >}}