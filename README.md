## This project contains sample utility notebooks/scripts for performing batch operations in Azure Purview. 
### This code is provided **As Is**
---
### **Dependancy:**
- Azure Purview CLI

---
### **Current functionality:**

1- Extract the following asset details from Purview into CSV files: (**Notebook: Extract Purview Assets**)
This will generate 2 files, one with asset level details and another with column level details. The second file takes longer time to generate. If you do not need this level of detail, skip this step.  

- name
- qualifiedName
- classification (Pipe separated)(configurable)
- term (Pipe separated) (configurable)
- description
- entityType
- assetType
- id (Guid)

2- Generate a PowerShell script of CLI commands and paylod files to update Purview assets (**Notebook: UpdateAssetLevelMetadata**)

Previously Extracted CSV from above or any other CSV in this format, can be further enriched with a Pipe separated (configurable) business glossary **formal names** and asset description. This notebook will use the enriched file to generate 2 PowerShell scripts. One will update asset description and the other one will update business glossary terms assignment.
Once UpdateAssetLevelMetadata notebook is run, by default a folder willl be created with this pattern ```{PurviewAccountName}_update``` which will host the PowerShell files along with all required .json payload files.
For safty reasons PowerShell files will have .ps1_ and will have to be renamed to .ps1.\
The PowerShell file will include lines to set the environment variables which it read from .env file except for AZURE_CLIENT_SECRET. This value will have to be populated before the script can run.\
**This will not remove existing term assignments but will overwrite desction for assets**\

--

### **Setup**
Setup.ipynb notebook contains configuration options.
provide a path for root_working_folder and the rest can be defaults.
The notebook will create a folder called ephemeral with a few .json transiant files to be used with CLI commands.

### **Authentication**
You will need to create a **.env** file in the root working folder and add the following lines to it.
```
PURVIEW_NAME="Purview Account Name"
AZURE_CLIENT_ID="Your client ID"
AZURE_TENANT_ID="Your tenant ID"
AZURE_CLIENT_SECRET="Your Client secret" 
```