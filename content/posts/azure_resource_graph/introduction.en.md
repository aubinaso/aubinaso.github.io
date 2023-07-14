---
title: "Azure Resource Graph Explorer & Kusto Query Language"
date: 2023-07-07T06:00:20+06:00
description: What is Azure Resource Graph Explorer and Kusto Query Language
menu:
  sidebar:
    name: Azure Resource Graph Explorer
    identifier: introduction
    parent: resourcegraph
    weight: 10
hero: /posts/azure_resource_graph/images/fond.png
tags: ["Markdown","Content Organization","Multi-lingual"]
categories: ["Basic"]
---

## What is Azure Resource Graph Explorer ?

`Azure Resource Graph Explorer` is a powerful tool provided by Microsoft Azure that allows you to efficiently and flexibly explore and query Azure resources at scale accoss a give set of subscriptions so that you can effectively govern your environment. It provides a user-friendly interface to query and visualize resource data using the Kusto query language.These queries provide the following abilities :
- Query resources with complex filtering, grouping, and sorting by resource properties
- Explore resources iteratively based on governance requirements
- Assess the impact of applying policies in a vast cloud environment
- Query changes made to resource properties

This tool allows you to create advanced queries to extract specific information from large amounts of Azure resource data. You can use logical operators, aggregations, joins, and functions to refine your queries and obtain the desired results.

It's important to understand that Azure Resource Graph's query language is based on the `Kusto Query Language (KQL)` used by Azure Data Explorer. To Use Resource Graph, you must have appropriate rights in Azure role-based access Control (Azure RBAC) with at least read access to the resources you want to query.

[More information](https://learn.microsoft.com/en-us/azure/governance/resource-graph/overview)

### What is Kusto Query Language / KQL ?

We've said that `KQL` is the query language used in Azure Resource Graph, but what is it ?
`KQL` or `Kusto Query Language` is a powerful tool to explore your data and discover patterns, identity anomalies and outliers, create statistical modeling, and more. the query uses schema entities that are organized in a hierarchy similar to SQLs: databases, tables, and columns.
`Kusto query` is a read-only request to process data and return results. There are `three kinds of user questy statement` :
- [tabular expression statement](https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/tabularexpressionstatements)
- [let statement](https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/letstatement)
- [set statement](https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/setstatement)

The most common kind of query statement is a tabular expression statement, which means both its input and output consist of tables or tabular datasets.

### What is Terraform ?
`Terraform` is an infrastructure as code tool that lets you build, change, and version infrastructure safely and efficiently. This includes low-level components like compute instances, storage, and networking; and high-level components like DNS entries and SaaS features.

To know more about this tool you can read
- [my note about Terraform](https://mct.aubinaso.fr/en/notes/terraform/)
- [Hashicorp Documentation](https://developer.hashicorp.com/terraform?product_intent=terraform)