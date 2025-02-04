# BudgetReports
 
Acesso a principais métodos da API ORACLE para informações de Uso de Serviços.


# COMO CONFIGURAR?

CRIAR DIRETÓRIO .OCI

Dentro do diretório .OCI, criar arquivo CONFIG com as seguintes informações:

[DEFAULT]
user=<cid1.user.oc1.xxxxxxxxxxxxxxxxxxxxxx>

fingerprint=<d:d0:cxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx>

tenancy=ocid1.tenancy.oc1..aaaaaaaatibiivijlqznqwwgrzxbx7ccsf4o4oxowqazkds7qurhtus6r6sa

region=sa-saopaulo-1

key_file=xxxxxxxxxxxxxx.pem


## CRIANDO AMBIENTE

no terminal powershell:

- python -m venv .venv
- .\.venv\Scripts\Activate.ps1  
- pip install -r requirements.txt



# UTILIZAÇÃO:


## SHOWUSAGE 
Application Command line parameters

   -c config    - OCI CLI Config
   -t profile   - profile inside the config file
   -p proxy     - Set Proxy (i.e. www-proxy-server.com:80)
   -ip          - Use Instance Principals for Authentication
   -g  grn      - Granularity DAILY / MONTHLY (Default DAILY)
   -dt          - Use Instance Principals with delegation token for cloud shell
   -ds date     - Start Date in YYYY-MM-DD format
   -de date     - End Date in YYYY-MM-DD format (Not Inclusive)
   -ld days     - Add Days Combined with Start Date (de is ignored if specified)
   -ld days     - Add Days Combined with Start Date (de is ignored if specified)
   -report type - Report Type = PRODUCT, DATE, REGION, SERVICE, RESOURCE, TENANT, SPECIAL, COMPARTMENT
                  SPECIAL is group by Service, Region, Product Description
   -csv         - Write to CSV files - usage_products.csv, usage_by_date.csv, usage_region.csvs,
                                       usage_resources.csv, usage_tenants.csv, usage_special.csv, usage_compartments.csv
Those are the valid options for GroupBy:
   "tagNamespace", "tagKey", "tagValue", "service", "skuName", "skuPartNumber", "unit", "compartmentName",
   "compartmentPath", "compartmentId", "platform", "region", "logicalAd", "resourceId", "tenantId", "tenantName"


### EXEMPLO DE COMANDO
 python showusage.py -ds 2025-01-01 -de 2025-01-20  -report SERVICE -t DEFAULT -csv 


## TAG RESOURCES TENANCIES

Application Command line parameters

```
   -t config       - Config file section to use (tenancy profile)  
   -p proxy        - Set Proxy (i.e. www-proxy-server.com:80) 
   -ip             - Use Instance Principals for Authentication 
   -dt             - Use Instance Principals with delegation token for cloud shell
   -cp compartment - filter by compartment name or id
   -rg region      - filter by region name
   -action add_defined | add_free | del_defined | del_free | list
   -tag            - tag information, can be either namespace.key=value or key=value with comma seperator for multiple tags
   -tagsep         - tag seperator default comma
   -service type   - Service Type default all, Services = all,compute,block,network,identity,loadbalancer,database,object,file
   -output         - list | json | summary
   -filter_by_name - Filter service by name, comma seperator for multi names
```
### Exemplo de comando

python tag_resources_tenancies.py -t DEFAULT -action list -cp ritm0023258pococrinssdiia  

## LISTANDO BUDGETS - CHAMADA PYTHON

```
 import oci
 import sys
 // Default config file and profile
 config = oci.config.from_file(file_location=".oci\\config")
 budget_client = oci.budget.BudgetClient(config)
 print(config)
 // The first argument is the name of the script, so start the index at 1
 compartment_id = config['tenancy']
 print("Compartment Id: " + compartment_id)
 // list all budgets
 budgets = oci.pagination.list_call_get_all_results(
     budget_client.list_budgets,
     compartment_id).data
  print('ListBudgets for compartment with OCID: {}'.format(compartment_id))
  for budget in budgets:
      print(budget)
```