---
title: "Azure Resource Graph Explorer & Kusto Query Language"
date: 2023-07-07T06:00:20+06:00
description: C'est quoi Azure Resource Graph Explorer et Kusto Query Language
menu:
  sidebar:
    name: Azure Resource Graph Explorer
    identifier: introduction
    parent: resourcegraph
    weight: 10
#hero: /posts/azure_resource_graph/images/fond.png
tags: ["Markdown","Content Organization","Multi-lingual"]
categories: ["Basic"]
---

## C'est quoi Azure Resource Graph Explorer ?

`Azure Resource Graph Explorer` est un outil puissant fourni par Microsoft Azure qui vous permet d'explorer et d'interroger de manière efficace et flexible les ressources Azure à l'échelle selon un ensemble donné d'abonnements afin que vous puissiez gouverner efficacement votre environnement. Il fournit une interface conviviale pour interroger et visualiser les données des ressources à l'aide du langage de requête Kusto. Ces requêtes offrent les capacités suivantes :
- Interroger les ressources avec des filtres complexes, des regroupements et des tris par propriétés de ressources.
- Explorer les ressources de manière itérative en fonction des exigences de gouvernance
- Évaluer l'impact de l'application de politiques dans un vaste environnement en nuage
- Interroger les changements apportés aux propriétés des ressources

Cet outil vous permet de créer des requêtes avancées pour extraire des informations spécifiques à partir de grandes quantités de données sur les ressources Azure. Vous pouvez utiliser des opérateurs logiques, des agrégations, des jointures et des fonctions pour affiner vos requêtes et obtenir les résultats souhaités.

Il est important de comprendre que le langage de requête d'Azure Resource Graph est basé sur le `Kusto Query Language (KQL)` utilisé par Azure Data Explorer. Pour utiliser Resource Graph, vous devez disposer des droits appropriés dans Azure RBAC (Azure Role-based Access Control) avec au moins un accès en lecture aux ressources que vous souhaitez interroger.

[Plus d'information](https://learn.microsoft.com/en-us/azure/governance/resource-graph/overview)

### C'est quoi Kusto Query Language / KQL ?

Nous avons dit que `KQL` est le langage de requête utilisé dans Azure Resource Graph, mais qu'est-ce que c'est ?
`KQL` ou `Kusto Query Language` est un outil puissant pour explorer vos données et découvrir des modèles, identifier des anomalies et des valeurs aberrantes, créer des modèles statistiques, et plus encore. La requête utilise des entités de schéma qui sont organisées dans une hiérarchie similaire à SQL : bases de données, tables et colonnes.
`Kusto query` est une requête en lecture seule qui permet de traiter des données et de renvoyer des résultats. Il existe `trois types d'instructions de requête utilisateur` :
- [Instruction d’expression tabulaire](https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/tabularexpressionstatements)
- [Instruction let](https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/letstatement)
- [Instruction set](https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/setstatement)

Le type le plus courant d’instruction de requête est une instruction d’expression tabulaire, ce qui signifie que son entrée et sa sortie sont des tables ou des jeux de données tabulaires.

### C'est quoi Terraform ?
`Terraform` est un outil d'infrastructure en tant que code qui vous permet de construire, de modifier et de réviser l'infrastructure de manière sûre et efficace. Il s'agit de composants de bas niveau comme les instances de calcul, le stockage et le réseau, et de composants de haut niveau comme les entrées DNS et les fonctions SaaS.

Pour en savoir plus sur cet outil, lisez
- [my note about Terraform](https://mct.aubinaso.fr/notes/terraform/)
- [La documentation Hashicorp](https://developer.hashicorp.com/terraform?product_intent=terraform)