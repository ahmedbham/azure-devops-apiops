# azure-devops-apiops

## Instructions for setting up Azure DevOps APIM Extraction and Publishing pipelines

1. Create two instances of APIM in Azure, if they do not already exist
2. In one of the instances, which will be the `dev` instance, create/import an API that need to be published to the other, `prod` instance
3. Create a new project in Azure DevOps
4. Create a new repository in the project by importing **https://github.com/ahmedbham/azure-devops-apiops.git**
5. Create a new service connection in the project settings
  - Service connection type: Azure Resource Manager
    - Authentication method: Workload Identity Federation (automatic)
        - Check `Security` - Allow all pipelines to use this connection
6. In Azure Portal, navigate to Entra ID
  - In `App Registration`, search for the app registration created for the `Service Connection` (should have a date of today)
    - note down the `Display name` 
7. In Azure Portal, navigate to the first APIM instance, which will be the `dev` instance
  - In `Access control (IAM)` 
    - select Add `Role assignments`
    - select `API Management Service Contributor` role, and click `Next`
    - select `+ Add members`
    - search for the `Application (client) ID` created for the `Service Connection`and `Select` it
    - click `Review + assign`twice     
8. In Azure Portal, navigate to the second APIM instance, and repeat step 8
9. In Azure DevOps, navigate to the `Pipelines` section
  - Create a new pipeline
  - Select `Azure Repos Git`
  - Select the repository imported from this GitHub repository
  - Select `Existing Azure Pipelines YAML file`
  - Select the `/tools/pipelines/run-extractor.yaml` file
  - Click dropdwon next to `Run`and select `Save`
  - Select the three dots next to `Run Pipeline`, and select `Rename/move`
    - Rename the pipeline to `Run Extractor`
10. In Azure DevOps, navigate to the `Pipelines` section
  - Create a new pipeline
  - Select `Azure Repos Git`
  - Select the repository imported from this GitHub repository
  - Select `Existing Azure Pipelines YAML file`
  - Select the `/tools/pipelines/run-publisher.yaml` file
  - Click dropdwon next to `Run`and select `Save`
  - Select the three dots next to `Run Pipeline`, and select `Rename/move`
    - Rename the pipeline to `Run Publisher`
11. In Azure DevOps, navigate to the `Pipelines` --> `Library` section
  - Create a new variable group
    - Name: `apim-automation`
    - Add the following variables:
      - `APIM_NAME`: the name of the `dev` APIM instance
      - `APIM_NAME_Prod`: the name of the `prod` APIM instance
      - `apiops_release_version`: `v5.1.4` (the version of the APIOps tool)
      - `RESOURCE_GROUP_NAME`: the resource group of the `dev` APIM instance
      - `RESOURCE_GROUP_NAME_Prod`: the resource group of the `prod` APIM instance
      - `SERVICE_CONNECTION_NAME`: the name of the service connection created in step 6
    - Click `Save`
    - Select `Pipeline permissions`
      - Select `Run Extractor` and `Run Publisher` pipelines
        - Click `Save`
12. In Azure DevOps, navigate to the `Pipelines` section
    - Select the `Run Extractor` pipeline
    - Click `Run`
    - Populate the `Paramters` with appropriate values
      - `APIM instance name`: the name of the `dev` APIM instance
      - `Folder where you want to extract the artifacts`: `artifacts`
      - `APIM instance resource group name`: the resource group of the `dev` APIM instance
      - `APIM repository for pull request`: the name of the repository created in step 4
      - `Target branch for pull request`: `main`
    - Click `Run`
13. After the `Run Extractor` pipeline has completed, navigate to the `Repos` --> `Pull requests` section
    - Select `Active` tab
    - Review the changes and click `Approve`
    - Click `Complete`
14. This should trigger `Run Publisher` pipeline
  - Check the progress of the pipeline in the `Pipelines` section
  - You may be prompted to approve deployment to `Prod`environment
  - Once the pipeline has completed, the API should be published to the `prod` APIM instance
