# BudgetReports
 
Acesso a principais métodos da API ORACLE para informações de Uso de Serviços.


# COMO CONFIGURAR?

CRIAR DIRETÓRIO .OCI

Dentro do diretório .OCI, criar arquivo CONFIG com as seguintes informações:

[DEFAULT]
user=<cid1.user.oc1.xxxxxxxxxxxxxxxxxxxxxx
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

 python showusage.py -ds 2025-01-01 -de 2025-01-20  -report SERVICE -t ALMEIDA -csv 
