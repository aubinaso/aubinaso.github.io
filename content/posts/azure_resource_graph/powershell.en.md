---
title: "Powershell main command"
date: 2023-07-08
description: Powershell Code
menu:
  sidebar:
    name: Powershell Code
    identifier: powershell
    parent: resourcegraph
    weight: 25
#hero: /posts/azure_resource_graph/images/fond.png
tags: ["Markdown","Content Organization","Multi-lingual"]
categories: ["Basic"]
---

To achieve this architecture, we will first write our Powershell code which will be used by `Azure Automation Runbook`. The main commands to know in this code are :
- `Connect-AzAccount -Identity` : this command allows us to use the identities of the host which is executing our code. In our case, the Runbook will execute our Powershell code using the identity which has been assigned to `Azure Automation Account` and therefore the rights granted to this identity.
- `Get-AzStorageAccount`, `Get-AzStorageBlobContent`, `Set-AzStorageBlobContent` are used to manage our storage account.
- `Search-AzGraph` : This command allows us to use the Microsoft Graph API to make KQL queries. It is located in the `Az.ResourceGraph` module. Compared to the previous commands, this command is in a module that will need to be imported into Azure Automation Account. The module to import is `Az.ResourceGraph` which we will import in terraform with the `azurerm_automation_module` resource available on this [link](https://www.powershellgallery.com/api/v2/package/Az.ResourceGraph/0.13.0). It depends on the `Az.Account` module available at [link](https://www.powershellgallery.com/api/v2/package/Az.Accounts/2.12.4). Note that all modules are [available].(https://www.powershellgallery.com/packages).

The end result is the following code extract, also available on [github](https://github.com/aubinaso/DefenderForCloudAutomate/blob/main/get_compliance.ps1) :

```PowerShell
Connect-AzAccount -Identity
# ...
Get-AzStorageBlobContent -Container $containerName -Blob $queryfile -Context $Context -Destination "./$queryfile" -Force
(Get-Content -Path "./$queryfile") | ForEach-Object { $_ -replace $lastStandard, $newStandard } | Set-Content -Path "./$kql_query"
$policyevent = Search-AzGraph -Query $(Get-Content -Path "./$kql_query" -raw)
```

You can see that I've redacted some KQL code extracts in a file and with the `Get-Content` command, I retrieve these requests which I use on the Graph API.
The query takes the form :

```
    securityresources
    | where type == 'microsoft.security/regulatorycompliancestandards/regulatorycompliancecontrols/regulatorycomplianceassessments'
    | parse id with * 'regulatoryComplianceStandards/' complianceStandardId '/regulatoryComplianceControls/' complianceControlId '/regulatoryComplianceAssessments' *
    | extend complianceStandardId = replace( '-', ' ', complianceStandardId)
    | project complianceStandardId
    | summarize by complianceStandardId
```

On [Github](https://github.com/aubinaso/DefenderForCloudAutomate/tree/main), you will notice that I have 2 requests, the first retrieves the list of Conformance Standards and the second retrieves the safety recommendations for a specific standard.