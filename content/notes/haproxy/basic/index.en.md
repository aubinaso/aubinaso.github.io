---
title: Haproxy Variables
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
NAME="John"
echo $NAME
echo "$NAME"
echo "${NAME}
```

{{< /note >}}

<!-- Condition -->
{{< note title="Condition" >}}

```bash
if [[ -z "$string" ]]; then
  echo "String is empty"
elif [[ -n "$string" ]]; then
  echo "String is not empty"
fi
```

{{< /note >}}