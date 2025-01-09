# Cobweb - Azure Naming Convention Initiative

This repository holds a bunch of bicep templates that creates and assigns Azure polices to audit or enforce a specific naming convention. 

The preset follows Microsoft naming convention which was proposed [here](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/resource-abbreviations) and adds some that where missing (e.g. private endpoints). For resource types where Microsoft doesn't make any suggestions I have created my own proposals, which can be found [here](https://github.com/matthiasguentert/azure-naming-convention-initiative/blob/main/PROPOSAL.md).

However you can modify them according to your needs. The underyling module uses a `notLike` condition so you can check for pre- and postfixes, e.g. `app-*` would match `app-some-web-application` whereas `*-app` would match `some-web-application-app`. 

## 🏗 Todo

- Update templates, so that pattern takes an array of strings, instead of a single string

## 👉 Important notes & limitations

- After assigning an initiative/policy it can take up to 30min until it becomes active, so be patient!
- You need to have the `Resource Policy Contributor` role assigned on the target subscription.
- Bicep currenlty only supports a [single scope](https://github.com/Azure/bicep/blob/main/docs/spec/resource-scopes.md) why I decided to stick with `subscription` scope for the moment.
- I didn't bundle them inside an initiative on purpose, so the user can freely decided on what to policy to use.
- When deploying a policy assignment via template, we currently can't set a `non-compliant message`. This seems to be a limitation of ARM.

This polices are ready to use. You don't have to rebuild them. However, in case you would like to apply your own naming schema follow this steps

1. Adjust the array at the begining of `Generate-Biceps.ps1` according to your needs 
2. Run `Generate-Biceps.ps1` that will outout *.biceps into the 'dist` folder
3. Run `Generate-Templates.ps1` to transpile them into JSON-based ARM templates (outputs to the `dist` folder)

## 🚀 Currently implemented resources

🟢 Tested 🟡 Not tested yet, feedback welcome! 🔴 Not yet implemented, PR welcome!

### General 

|Asset type | Abbreviation | Status | Deploy 
|--|--|--|--|
| Management group | `mg-` |🟢|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-mg.json)|
| Resource group | `rg-` |🟢|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-rg.json)|
| Policy definition | `policy-` |🟡|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-policy.json)|
| API management service instance | `apim-` |🟡|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-apim.json)|
| Managed Identity | `id-` |🟢|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-id.json)|

### Networking 

|Asset type | Abbreviation | Status | Deploy 
|--|--|--|--|
| Private endpoint | `pe-` |🔴||
| Virtual network | `vnet-` |🟢|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-vnet.json)|
| Subnet | `snet-` |🟡|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-snet.json)|
| Virtual network peering | `peer-` |🟡|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-peer.json)|
| Network interface (NIC) | `nic-` |🟡|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-nic.json)|
| Public IP address | `pip-` |🟡|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-pip.json)|
| Load balancer (internal) | `lbi-` |🔴||
| Load balancer (external) | `lbe-` |🔴||
| Network security group (NSG) | `nsg-` |🟡|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-nsg.json)|
| Application security group (ASG) | `asg-` |🟡|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-asg.json)|
| Local network gateway | `lgw-` |🟡|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-lgw.json)|
| Virtual network gateway | `vgw-` |🟡|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-lgw.json)|
| VPN connection | `cn-` |🟡|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-cn.json)|
| ExpressRoute circuit | `erc-` |🟡|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-erc.json)|
| Application gateway | `agw-` |🟡|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-agw.json)|
| Route table | `route-` |🟡|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-route.json)|
| User defined route (UDR) | `udr-` |🟡|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-udr.json)|
| Traffic Manager profile | `traf-` |🟡|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-traf.json)|
| Front door | `fd-` |🟡|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-fd.json)|
| CDN profile | `cdnp-` |🟢|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-cdnp.json)|
| CDN endpoint | `cdne-` |🟢|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-cdne.json)|
| Web Application Firewall (WAF) policy | `waf` |🟡|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-waf.json)|

### Compute and Web 

Asset type | Abbreviation | Status | Deploy 
|--|--|--|--|
| Virtual machine | `vm` |🟢|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-vm.json)|
| Virtual machine scale set | `vmss-` |🟡|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-vmss.json)|
| Availability set | `avail-` |🟡|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-avail.json)|
| Managed disk (OS) | `osdisk` |🔴||
| Managed disk (data) | `disk` |🔴||
| VM storage account | `stvm` |🔴||
| Azure Arc enabled server | `arcs-` |🔴||
| Azure Arc enabled Kubernetes cluster | `arck` |🔴||
| Container registry | `cr` |🔴||
| Container instance | `ci-` |🔴||
| AKS cluster | `aks-` |🟡|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-aks.json)|
| Service Fabric cluster | `sf-` |🔴||
| App Service environment | `ase-` |🔴||
| App Service plan | `plan-` |🟢|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-plan.json)|
| Web app | `app-` |🟢|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-app.json)|
| Static web app | `stapp` |🔴||
| Function app | `func-` |🟡|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-func.json)|
| Cloud service | `cld-` |🔴||
| Notification Hubs | `ntf-` |🟡|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-ntf.json)|
| Notification Hubs namespace | `ntfns-` |🟡|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-ntfns.json)|

### Databases 

Asset type | Abbreviation | Status | Deploy 
|--|--|--|--|
| Azure SQL Database server | `sql-` |🟡|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-sql.json)|
| Azure SQL database | `sqldb-` |🟡|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-sqldb.json)|
| Azure Cosmos DB database | `cosmos-` |🟢|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-cosmos.json)|
| Azure Cache for Redis instance | `redis-` |🟢|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-redis.json)|
| MySQL database | `mysql-` |🟡|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-mysql.json)|
| PostgreSQL database | `psql-` |🟢|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-psql.json)|
| Azure SQL Data Warehouse | `sqldw-` |🔴||
| Azure Synapse Analytics | `syn-` |🔴||
| SQL Server Stretch Database | `sqlstrdb-` |🔴||
| SQL Managed Instance | `sqlmi-` |🟡|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-sqlmi.json)|

### Storage 

Asset type | Abbreviation | Status | Deploy 
|--|--|--|--|
| Storage account | `st` |🟢|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-st.json)|
| Azure StorSimple | `ssimp` |🔴||
| Azure Container Registry | `acr` |🟢|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-acr.json)|

### AI and Machine Learning

Asset type | Abbreviation | Status | Deploy 
|--|--|--|--|
| Azure Cognitive Search | `srch-` |🔴||
| Azure Cognitive Services | `cog-` |🔴||
| Azure Machine Learning workspace | `mlw-` |🔴||

### Analytics and IoT

Asset type | Abbreviation | Status | Deploy 
|--|--|--|--|
| Azure Analysis Services server | `as` |🔴||
| Azure Databricks workspace | `dbw-` |🔴||
| Azure Stream Analytics | `asa-` |🔴||
| Azure Data Explorer cluster | `dec` |🔴||
| Azure Data Factory | `adf-` |🔴||
| Data Lake Store account | `dls` |🔴||
| Data Lake Analytics account | `dla` |🔴||
| HDInsight - Hadoop cluster | `hadoop-` |🔴||
| HDInsight - HBase cluster | `hbase-` |🔴||
| HDInsight - Kafka cluster | `kafka-` |🔴||
| HDInsight - Spark cluster | `spark-` |🔴||
| HDInsight - Storm cluster | `storm-` |🔴||
| HDInsight - ML Services cluster | `mls-` |🔴||
| IoT hub | `iot-` |🔴||
| Power BI Embedded | `pbi-` |🔴||
| Time Series Insights environment | `tsi-` |🔴||

### Developer tools

Asset type | Abbreviation | Status | Deploy 
|--|--|--|--|
| App Configuration store | `appcs-` |🟢|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-appcs.json)|
| Azure Static Web Apps | `stap-` |🟡|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-stap.json)|

### Integration

Asset type | Abbreviation | Status | Deploy 
|--|--|--|--|
| Integration account | `ia-` |🟢|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-ia.json)|
| Logic apps | `logic-` |🟢|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-logic.json)|
| Service Bus | `sb-` |🟢|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-sb.json)|
| Service Bus queue | `sbq-` |🟢|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-sbq.json)|
| Service Bus topic | `sbt-` |🟢|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-sbt.json)|
| Event Hubs namespace | `evhns-` |🟢|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-evhns.json)|
| Event hub | `evh-` |🟢|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-evh.json)|
| Event Grid domain | `evgd-` |🟢|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-evgd.json)|
| Event Grid topic | `evgt-` |🟢|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-evgt.json)|
| Event Grid system topic | `evgst-` |🔴||
|Event Grid Subscriptions | `evgs-`|🔴|`Microsoft.EventGrid/eventSubscriptions`|

### Management and governance

Asset type | Abbreviation | Status | Deploy 
|--|--|--|--|
| Automation account | `aa-` |🟡|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-aa.json)|
| Azure Monitor action group | `ag-` |🔴||
| Azure Purview instance | `pview-` |🔴||
| Blueprint | `bp-` |🔴||
| Blueprint assignment | `bpa-` |🔴||
| Key vault | `kv-` |🟢|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-kv.json)|
| Log Analytics workspace | `log-` |🟢|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-log.json)|
| Application Insights | `appi-` |🟢|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-appi.json)|

### Migration

Asset type | Abbreviation | Status | Deploy 
|--|--|--|--|
| Azure Migrate project | `migr-` |🔴||
| Database Migration Service instance | `dms-` |🟡|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-dms.json)|
| Recovery Services vault | `rsv-` |🟡|[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmatthiasguentert%2Fazure-naming-convention-initiative%2Fmain%2Fdist%2Fnaming-convention-rsv.json)|

## 🤓 Further reading 

- [Azure Policy as Code workflow](https://docs.microsoft.com/en-us/azure/governance/policy/concepts/policy-as-code)
- [Resource providers for Azure services](https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/azure-services-resource-providers)
- [Azure Templates](https://docs.microsoft.com/en-us/azure/templates/)
