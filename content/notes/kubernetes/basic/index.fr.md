---
title: Variables en Bash
weight: 210
menu:
  notes:
    name: Variables
    identifier: notes-bash-variables
    parent: notes-bash
    weight: 10
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