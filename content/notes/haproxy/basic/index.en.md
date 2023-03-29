---
title: Haproxy Variables
weight: 100
menu:
  notes:
    name: Variables
    identifier: notes-haproxy-variables
    parent: notes-haproxy
    weight: 100
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