---
layout: post
title: Azure Devops
date: 2023-12-29 09:56 -0600
categories: [Cloud, Azure, Devops]
image: 
  path: /2023-12-29-azure-devops/profile.png
---

- [Lifecycle](#lifecycle)
  - [5 core Azure devops services](#5-core-azure-devops-services)
- [Azure Bicep](#azure-bicep)
- [Azure Resource manager](#azure-resource-manager)
- [Arm Templates](#arm-templates)
- [Install Azure powershell module](#install-azure-powershell-module)
- [Bicep](#bicep)
  - [String Intrepolation](#string-intrepolation)
  - [Arrays](#arrays)
  - [Output to screen](#output-to-screen)
  - [Parameters](#parameters)
  - [Unique string](#unique-string)
  - [Ternary operator](#ternary-operator)
  - [VSCode Bicep extension](#vscode-bicep-extension)


# Lifecycle
  - ![alt-text](/2023-12-29-azure-devops/devops_lifecycle.png)
  - Dev Steps
    - plan
    - code
    - build
    - test
  - Ops steps
    - release
    - deploy
    - operate
    - monitor

## 5 core Azure devops services
  - ![alt-text](/2023-12-29-azure-devops/core_services.png)

# Azure Bicep
  - step up from just basic Arm templates

# Azure Resource manager
  - Azure resource manager uses Azure AD for authentication so it doesn't matter if you use the Azure portal, cli or azure bicep it is all secure
  - ![alt-text](/2023-12-29-azure-devops/resource_manager.png)


  - environments typically have a production and dev subscription
  - along with different resource groups that are separated by their layer like the db layer, or the application server layer
  - ![alt-text](/2023-12-29-azure-devops/hierarcy.png)

  - we can create a resource just like in the gui except using a arm template json
  - ![alt-text](/2023-12-29-azure-devops/gui_template.png)

# Arm Templates
  - Benefits
    - IAC
    - (Governance as code) Policy and roles as code
    - Repeatable results
    - Orchestration
    - Built-in validation

# Install Azure powershell module
  - `Install-module -name Az -AllowClobber`

# Bicep

## String Intrepolation
  - use dollarsign curly braces inside a string to use string interpolation

```bicep
var prefix = 'prod'
var storageName = '${prefix}teststorage01'
```

## Arrays
  - Arrays are simple in bicep they are just

```bicep
// use commas if they are on the same line
var x = [
  1, 2, 3
]

// don't use commas if they are on different lines
var y = [
  1
  2
  3
]
```


> This will loop through the 3 different regions and create a storage account in each region
{: .prompt-tip }

> This also gets the index from each iteration by using **(region, i)**. You can name i anything you want like index
{: .prompt-tip }

```bicep
var regions = [
  'centralus', 'southeastasia', 'northeurope' 
]

// location and storage account name
param location string = resourceGroup().location
var uString = uniqueString(resourceGroup().id)
var storageAccountName = 'toylaunch${uString}'

resource storageaccount 'Microsoft.Storage/storageAccounts@2021-02-01' = [for (region,i) in regions: {
  name: '${storageAccountName}${i}'
  kind: 'StorageV2'
  location: region
  sku: {
    name: 'Premium_LRS'
  }
  properties: {
    accessTier: 'Cool'
  }
}]

```

## Output to screen
  - you can output the to screen when executing a bicep file with the **output** keyword

```bicep
  // output
  output location string = 'Hello world'
```

```text
DeploymentName          : param
ResourceGroupName       : Test
ProvisioningState       : Succeeded
Timestamp               : 12/30/2023 10:02:35 PM
Mode                    : Incremental
TemplateLink            : 
Parameters              : 
Outputs                 : 
                          Name             Type                       Value     
                          ===============  =========================  ==========
                          location         String                     "Hello world"
                          
DeploymentDebugLogLevel : 
```

## Parameters
  - you can specify parameters to your bicep code like this

```bicep
@allowed([
  'john', 'briana', 'tresten'
])
param location string
```

```text
PS /home/tpool/Playground/PowershellBicepExamples/Basic_Examples> New-AzResourceGroupDeployment -TemplateParameterObject @{location='tresten'} -TemplateFile ./param.bicep -ResourceGroupName Test

DeploymentName          : param
ResourceGroupName       : Test
ProvisioningState       : Succeeded
Timestamp               : 12/30/2023 10:04:06 PM
Mode                    : Incremental
TemplateLink            : 
Parameters              : 
                          Name             Type                       Value     
                          ===============  =========================  ==========
                          location         String                     "tresten" 
                          
Outputs                 : 
DeploymentDebugLogLevel : 
```

However if we passed something that isn't in the @allowed array we get the following error
```text
PS /home/tpool/Playground/PowershellBicepExamples/Basic_Examples> New-AzResourceGroupDeployment -TemplateParameterObject @{location='NOra'} -TemplateFile ./param.bicep -ResourceGroupName Test      

New-AzResourceGroupDeployment: 4:05:19 PM - Error: Code=InvalidTemplate; Message=Deployment template validation failed: 'The provided value for the template parameter 'location' is not valid. The value 'NOra' is not part of the allowed value(s): 'john,briana,tresten'.'.
New-AzResourceGroupDeployment: The deployment validation failed
```

## Unique string
  - you may sometimes need to generate a unique string that is the same for resources in the same resource group but different when run in a different resource group

```bicep
var unique_id = uniqueString(resourceGroup().id)
```

## Ternary operator
  - bicep has a ternary operator we can take advantage of 

```bicep
var storageAccountSkuName = (environmentType == 'prod') ? 'Standard_GRS' : 'Standard_LRS'
var appServicePlanSkuName = (environmentType == 'prod') ? 'P2V3' : 'F1'
```

## VSCode Bicep extension
  - to get resource template snippets use the keyword **res-** and it will suggest some resource such as this 
  - ![alt-text](/2023-12-29-azure-devops/res.png)

  - to add the required properties for a resource you can select required-properties
  - ![alt-text](/2023-12-29-azure-devops/required_properties.png)



