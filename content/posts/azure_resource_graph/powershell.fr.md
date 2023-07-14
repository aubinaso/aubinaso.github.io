---
title: "commande Powershell principale"
date: 2023-07-14
description: Code Powershell
menu:
  sidebar:
    name: Code Powershell
    identifier: powershell
    parent: resourcegraph
    weight: 25
hero: /posts/azure_resource_graph/images/fond.png
tags: ["Markdown","Content Organization","Multi-lingual"]
categories: ["Basic"]
---

Pour réaliser cette architecture, nous allons premièrement rédiger notre code Powershell qui sera exploité par `Azure Automation Runbook`. Les commandes principales à savoir dans ce code sont les suivantes :
- `Connect-AzAccount -Identity` : cette commande permet de se servir des identités de l'hôte qui exécute notre code. Dans notre cas, le Runbook va exécuter notre code Powershell en se servant de l'identité qui a été attribuée à `Azure Automation Account` et donc des droits accordés à cette identité.
- `Get-AzStorageAccount`, `Get-AzStorageBlobContent`, `Set-AzStorageBlobContent` permet de gérer notre compte de stockage.
- `Search-AzGraph` : cette commande permet de nous servir de l'API Graph Microsoft pour faire des requêtes KQL. Elle se trouve dans le module `Az.ResourceGraph`, comparée aux précédentes commandes, cette commande est dans un module qu'il faudra importer dans Azure Automation Account. Le module à importer est `Az.ResourceGraph` que nous allons importer en terraform avec la resource `azurerm_automation_module` disponible sur ce [lien](https://www.powershellgallery.com/api/v2/package/Az.ResourceGraph/0.13.0). Il dépend du module `Az.Account` disponible sur le [lien](https://www.powershellgallery.com/api/v2/package/Az.Accounts/2.12.4). Il faut noté que l'ensemble des modules sont [disponibles](https://www.powershellgallery.com/packages).

Nous aurons au final l'extrait de code suivant aussi disponible sur [github](https://github.com/aubinaso/DefenderForCloudAutomate/blob/main/get_compliance.ps1) :

```PowerShell
Connect-AzAccount -Identity
# ...
Get-AzStorageBlobContent -Container $containerName -Blob $queryfile -Context $Context -Destination "./$queryfile" -Force
(Get-Content -Path "./$queryfile") | ForEach-Object { $_ -replace $lastStandard, $newStandard } | Set-Content -Path "./$kql_query"
$policyevent = Search-AzGraph -Query $(Get-Content -Path "./$kql_query" -raw)
```

On peut remarquer que j'ai rediger des extraits de code KQL dans un fichier et avec la commande `Get-Content`, je recupère ces requêtes que j'utilise sur l'API Graph.
La requête se présente sous la forme :

```
    securityresources
    | where type == 'microsoft.security/regulatorycompliancestandards/regulatorycompliancecontrols/regulatorycomplianceassessments'
    | parse id with * 'regulatoryComplianceStandards/' complianceStandardId '/regulatoryComplianceControls/' complianceControlId '/regulatoryComplianceAssessments' *
    | extend complianceStandardId = replace( '-', ' ', complianceStandardId)
    | project complianceStandardId
    | summarize by complianceStandardId
```

Sur le [Github](https://github.com/aubinaso/DefenderForCloudAutomate/tree/main), vous allez remarquer que j'ai 2 requêtes, la première recupère la liste des Standards de Conformité et la seconde recupère les recommandations de sécurité pour un standard précis.