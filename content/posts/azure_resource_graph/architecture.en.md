---
title: "Get Compliance Reports from Defender for Cloud using Terraform"
date: 2023-07-08
description: Architecture of Compliance Report
menu:
  sidebar:
    name: Azure Architecture
    identifier: architecture
    parent: resourcegraph
    weight: 20
hero: images/forest.jpg
tags: ["Markdown","Content Organization","Multi-lingual"]
categories: ["Basic"]
---

The aim of this article is to find out about the Resource Graph solution that I use to retrieve Microsoft Defender compliance reports.
After some research I realised that, apart from the possibility of configuring automatic retrieval of compliance reports from the Azure portal, there was no scripting solution for doing this.
So in this project, using a PowerShell code that I'm going to upload to an `Azure Automation Runbook`, I'm going to be able to perform the list of the following actions :
- Retrieve compliance information for a particular standard from Defender for Cloud
- Generate a csv file
- upload the result to a Storage Account

We will then have the following diagram:

{{< img src="./images/figure23.png" align="center" title="Architecture">}}

{{< vs >}}

Dans cette architecture, nous retrouvons :
- `Microsoft Defender for Cloud` which is a Microsoft cloud security solution offering advanced protection against threats and attacks targeting cloud environments such as Microsoft Azure, Amazon Web Services and Google Cloud Platform. It should be noted that the latter includes the option of activating security and compliance standards such as PCI DSS, CIS...
- `Azure Resource Graph` which we will query with `KQL` commands.
- `Azure Automation Account` which allows us to define automation operations. It is from this service that we are going to define a `Runbook` which will contain our Powershell code to be executed at defined times.
- `Azure RBAC` : Note that our PowerShell function will certainly need to access resources requiring a certain number of privileges. Here we will define a `System Managed Identity` for our Azure Automation Account service.
- `Azure Storage Account` where we will upload our recovered csv files.

It is also possible to use the `Azure Function` service instead of Azure Automation Account, but in this case, we will need to define files to facilitate the installation of PowerShell modules, which our code will need in a zip file as follows in powershell

```bash
  app_settings = {
    "FUNCTIONS_WORKER_RUNTIME"       = "powershell"
    "WEBSITE_RUN_FROM_PACKAGE"       = 1
    "APPINSIGHTS_INSTRUMENTATIONKEY" = azurerm_application_insights.application_insights.instrumentation_key
  }
  zip_deploy_file = var.zip_file
```

This is the terraform code, which you can read more about [here](https://github.com/aubinaso/DefenderForCloudAutomate/blob/main/modules/function_app/main.tf).