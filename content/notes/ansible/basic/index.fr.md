---
title: Variables en Ansible
weight: 210
menu:
  notes:
    name: Variables
    identifier: notes-ansible-variables
    parent: notes-ansible
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