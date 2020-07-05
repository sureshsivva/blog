---
title: Azure CosmosDB Adjust Throughput Settings
author: Suresh Siva
date: 2020-07-04 08:00:00 +0800
categories: [Azure, Cosmosdb]
tags: [azure, cosmosdb, tuning, optimization, throughput, azure-cli, cli, az]
math: true
---

## **Intro**

`az cosmosdb` command allows us to adjust the `Request Units (RUs)` setting of both databases and collections. RUs can be modified at any point of time.

I have used the commands utilizing the `sql api` here to perform the RUs value adjustment on databases and collections. Here I am only covering about `updating` the existing entities RUs.

## **Scenario**
I happened to perform update in RUs when I had to `Bulk Import` huge volume of rows within a SLA time periodically, where in the database and collection RUs need to be spiked for a while for bulk operations and have to rolled back to serve the predicted RW requests.

> Autoscale settings are not available through `az cli` by the time of writing this

## **Database RUs**

Below command helps in viewing the current RUs setting of a database.

``` shell
az cosmosdb sql database throughput show --subscription demo-sub-1 --resource-group demo-rg-1 --account-name demo-cosmos-account-name --name db-name-1
```

It returns the result similar to the below one,

``` json
{
  "id": "/subscriptions/id/resourceGroups/rg-name/providers/Microsoft.DocumentDB/databaseAccounts/db-account-name/apis/sql/databases/db-name/settings/throughput",
  "location": null,
  "name": "VfFU",
  "resourceGroup": "rg-name",
  "tags": null,
  "throughput": 14000,
  "type": "Microsoft.DocumentDB/databaseAccounts/apis/databases/settings"
}
```

To `update` a database's RUs, use the below command,

``` shell
az cosmosdb sql database throughput update --subscription demo-sub-1 --resource-group demo-rg-1 --account-name demo-cosmos-account-name --name db-name-1 --throughput 14000
```

> The larger RUs value changes will take sometime to reflect, so handle it wisely with some time waits.

## **Collection RUs**

Below command helps in viewing the current RUs setting of a collection.

``` shell
az cosmosdb sql container throughput show --subscription demo-sub-1 --resource-group demo-rg-1 --account-name demo-cosmos-account-name --database-name db-name-1 --name test_coll-1
```

It returns result similar to the below one,

``` json
{
  "id": "/subscriptions/id/resourceGroups/rg-name/providers/Microsoft.DocumentDB/databaseAccounts/db-account-name/apis/sql/databases/db-name/containers/tcollection-name/settings/throughput",
  "location": null,
  "name": "yYLA",
  "resourceGroup": "rg-name",
  "tags": null,
  "throughput": 400,
  "type": "Microsoft.DocumentDB/databaseAccounts/apis/databases/containers/settings"
}
```

If the collection's RUs were not yet provisioned explicitly, the below error message might occur,

``` ruby
Operation failed with status: 'NotFound'. Details: Entity with the specified id does not exist in the system.
ActivityId: 17cd9fe2-bef7-11ea-8872-dummy, Microsoft.Azure.Documents.Common/2.11.0
```

Above activity can be also performed using the below `collection` subcommand
``` shell
az cosmosdb collection show --subscription demo-sub-1 --resource-group-name demo-rg-1 --name demo-cosmos-account-name --db-name db-name-1 --collection-name test_coll-1
```

To `update` a collection's RUs, use the below command,

``` shell
az cosmosdb sql container throughput update --subscription demo-sub-1 --resource-group demo-rg-1 --account-name demo-cosmos-account-name --database-name db-name-1 --name test_coll-1 --throughput 400
```

Above activity can be also performed using the below `collection` subcommand

``` shell
az cosmosdb collection update --subscription demo-sub-1 --resource-group-name demo-rg-1 --name demo-cosmos-account-name --db-name db-name-1 --collection-name test_coll-1 --throughput 400
```

Hope this helps!!
