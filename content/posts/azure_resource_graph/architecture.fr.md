---
title: "Obtenir des rapports de conformité de Defender for Cloud à l'aide de Terraform"
date: 2023-07-08
description: Architecture du rapport de conformité
menu:
  sidebar:
    name: Architecture Azure
    identifier: architecture
    parent: resourcegraph
    weight: 20
hero: forest.jpg
tags: ["Markdown","Content Organization","Multi-lingual"]
categories: ["Basic"]
---

Le but dans cet article est de découvrir la solution Resource Graph que j'exploite pour recupérer les rapports de conformité de Microsoft Defender.
Après quelques recherches je me suis rendu compte qu'hormis la possibilité de configurer la recupération automatique des rapports de conformité depuis le portail Azure, il n'y avait pas de solution de scripting pour effectuer cela.
Ainsi dans ce projet, à l'aide d'un code PowerShell que je vais uploader dans un `Azure Automation Runbook`, je vais pouvoir effectuer la liste des actions suivantes :
- Recupérer les informations de conformité d'un standard en particulier sur Defender for Cloud
- Générer un fichier csv
- uploader le resultat dans un Storage Account

Nous aurons alors le schéma suivant :

{{< img src="./images/figure23.jpg" align="center" title="Architecture">}}

{{< vs >}}

Dans cette architecture, nous retrouvons :
- `Microsoft Defender for Cloud` qui est une solution de sécurité cloud de Microsoft offrant une protection avancée contre les menaces et les attaques ciblant les environnements cloud tels que Microsoft Azure, Amazon Web Services, Google Cloud Plateform. Il faut noté que ce dernier intègre la possibilité d'activer des standard de sécurité et de conformité notamment le PCI DSS, CIS...
- `Azure Resource Graph` que nous allons requêter avec des commandes `KQL`
- `Azure Automation Account` qui nous permet de définir des opérations d'automatisation. C'est à partir de ce service que nous allons définir un `Runbook` qui contiendra notre code Powershell à exécuter à des périodes définies
- `Azure RBAC` : il est à noté que notre function PowerShell aura certainement besoin d'accéder à des ressources nécessitant un certain nombre de privilèges. Nous allons ici définir un `System Managed Identity` pour notre service Azure Automation Account
- `Azure Storage Account` où nous allons uploader nos fichiers csv recupérés.

Il est également possible d'utiliser à la place de Azure Automation Account le service `Azure Function` mais dans ce cas, il faudra définir des fichiers facilitant l'installation des modules PowerShell donc notre code aura besoin dans un fichier zipé comme suit en powershell

```bash
  app_settings = {
    "FUNCTIONS_WORKER_RUNTIME"       = "powershell"
    "WEBSITE_RUN_FROM_PACKAGE"       = 1
    "APPINSIGHTS_INSTRUMENTATIONKEY" = azurerm_application_insights.application_insights.instrumentation_key
  }
  zip_deploy_file = var.zip_file
```

Il s'agit ici du code terraform que vous pouvez retrouver la suite [ici](https://github.com/aubinaso/DefenderForCloudAutomate/blob/main/modules/function_app/main.tf).