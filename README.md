# InfoNotes

```
# references
# https://stoacawks.z6.web.core.windows.net/#lab1-intro

# vegeta: load testing tool
# curl -LO https://github.com/tsenart/vegeta/releases/download/v12.8.4/vegeta_12.8.4_linux_amd64.tar.gz


# create azure container apps environment

az containerapp env create \
--name $CONTAINERAPPS_ENVIRONMENT \
--resource-group $RESOURCE_GROUP \
--logs-workspace-id $LOG_ANALYTICS_WORKSPACE_CLIENT_ID \
--logs-workspace-key $LOG_ANALYTICS_WORKSPACE_CLIENT_SECRET \
--location "$LOCATION"

# create azure container apps

az containerapp create \
  --name my-container-app \
  --resource-group $RESOURCE_GROUP \
  --environment $CONTAINERAPPS_ENVIRONMENT \
  --image mcr.microsoft.com/azuredocs/containerapps-helloworld:latest \
  --registry-server $ACR_NAME.azurecr.io \
  --registry-username $(az keyvault secret show --vault-name $AKV_NAME --name $ACR_NAME-pull-usr --query value -o tsv) \
  --registry-password $(az keyvault secret show --vault-name $AKV_NAME --name $ACR_NAME-pull-pwd --query value -o tsv) \
  --target-port 80 \
  --ingress 'external' \
  --query configuration.ingress.fqdn
```
