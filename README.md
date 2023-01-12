# essential-azure-apim

essential-azure-apim

<https://learn.microsoft.com/en-us/azure/api-management/api-management-key-concepts>

<https://learn.microsoft.com/en-us/azure/api-management/quickstart-arm-template>

<https://learn.microsoft.com/en-us/azure/api-management/import-and-publish>

## Step 1 Install az cli

```bash
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```

## Step 2 Deploy apim

```bash
source .env
az login --tenant $TENANT
az account set -s $SUBSCRIPTION
az deployment group create --subscription $SUBSCRIPTION \
                           --resource-group $RESOURCE_GROUP \
                           --name rollout01 \
                           --template-file ARMTemplate/APIM/template.json \
                           --parameters ARMTemplate/APIM/parameters.json
```


## Step 3 Example to import an API into API Management


## Step 4 Test the API in the Azure portal



## Finally Delete resources

After experiment, delete all resources to avoid charging a lot of money

```bash
source .env
az group delete -y --name $RESOURCE_GROUP
```

There can be some managed resources to delete. Check them by

```bash
az group list --subscription $SUBSCRIPTION
```

Delete them by

```bash
source .env
az group delete --name $(az group list --subscription $SUBSCRIPTION | jq '.[].name' | tr -d '"')
```
