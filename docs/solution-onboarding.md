# How to add 'AzureMonitor-Containers' solution to a Azure Loganalytics workspace

You can either use the Azure Powershell or Azure cli to deploy the solution.

## Create Deployment files 
If you are not familiar with the concepts of deploying resources using a template with PowerShell, see [Deploy resources with Resource Manager templates and Azure PowerShell](https://review.docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-template-deploy)

1. Get the below template files to your local computer.
..* Template file [azuremonitor-containerSolution.json](https://github.com/Microsoft/OMS-docker/blob/ci_feature_prod/docs/templates/azuremonitor-containerSolution.json)
..* TemplateParams file [azuremonitor-containerSolutionParams.json](https://github.com/Microsoft/OMS-docker/blob/ci_feature_prod/docs/templates/azuremonitor-containerSolutionParams.json)
2. Edit the TemplateParams file in your local computer.
..* workspaceResourceId parameter :
....1. Replace <SubscriptionId> with Azure subscriptionID for your Workspace
....2. Replace <ResourceGroup> with Azure ResourceGroup name for your Workspace
....3. Replace <workspaceName> with Azure LogAnalytics Workspace name for your Workspace
..* workspaceRegion parameter :
....1. Replace <eastus> with your Azure LogAnalytics Workspace region

## Deploy using Powershell
- Use the following PowerShell commands from the folder containing the template files:

``` sh 
New-AzureRmResourceGroupDeployment -Name OnboardCluster -ResourceGroupName ClusterResourceGroupName -TemplateFile .\azuremonitor-containerSolution.json -TemplateParameterFile .\azuremonitor-containerSolutionParams.json 
```

The configuration change can take a few minutes to complete. When it finishes, you see a message similar to the following that includes the result:

``` sh
provisioningState       : Succeeded 
```

## Deploy using Azure CLI on Linux:
- Run the following command from the folder containing the template files:

``` sh 
az login
az account set --subscription "<Subscription Name of your Log Analytics Workspace>"
az group deployment create --resource-group <ResourceGroupName> --template-file ./existingClusterOnboarding.json --parameters @./existingClusterParam.json 
```

The configuration change can take a few minutes to complete. When it finishes, you see a message similar to the following that includes the result:

``` sh
provisioningState       : Succeeded 
```

After monitoring is enabled, it can take around 15 minutes before you are able to see operational data for the cluster.