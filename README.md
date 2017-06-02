# BOSH Azure Cookbook
Convenient ARM-based deployment to bootstrap bosh in a new resource group and install a release

Quick HOWTO

1. Clone this repository

2. Create an azuredeploy.parameters.json file with the following format;

```
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adminSSHKey": {
      "value": "ssh-rsa AAAAB3..."
    },
    "tenantID": {
      "value": "xxxxxxx"
    },
    "clientID": {
      "value": "xxxxxxx"
    },
    "clientSecret": {
      "value": "xxxxxxx"
    },
    "vmSize": {
      "value": "Standard_DS2_v2"
    },
    "adminUsername": {
      "value": "pivotal"
    },
    "location": {
      "value": "westus"
    },
    "recipeName": {
      "value": "concourse"
    }

  }
}
```

3. Deploy with the azure CLI as normal or use the deploy.sh script file, passing the name of the resource group, the script will wait
for a bootstrap vm to become available and then ssh to it. From there you can monitor the logs for the install process (stdout, errout) in the usual location for
Azure linux extension scripts (/var/lib/waagent/Microsoft..../download/0) to monitor the install of the BOSH director and release.

4. Once the deployment is complete, download the creds.yml file that was uploaded to the storage account created in the specified resource group, this
should contain all BOSH generated credentials for the deployment.
