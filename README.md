## This project contains sample utility notebooks/scripts for performing batch operations in Microsoft Purview. 
### This code is provided **As Is**
---
### **Dependancy:**
- Azure Purview CLI

---
### **Current functionality:**

1- Extract the following asset details from Purview into CSV files: (**Notebook: Extract Purview Assets**)
If extract_schema_level_details is False, the export file will have data only at the asset level. If extract_schema_level_details is True, the file will contain rows for each asset and if the asset has a schema, the details of schema will be populated after asset row. 
This will take a considerably longer time to generate.  

- name
- qualifiedName
- classification (Pipe separated)(configurable)
- term (Pipe separated) (configurable)
- description
- entityType
- id (Guid)
- certifiedBy

2- Generate a PowerShell script of CLI commands and paylod files to update Purview assets (**Notebook: UpdateAssetLevelMetadata**)

Previously Extracted CSV from above or any other CSV in this format, can be further enriched with a Pipe separated (configurable) business glossary **formal names**, asset description and classifications. This notebook will use the enriched file to generate 3 PowerShell scripts. One will update asset description and the other 2 will update business glossary terms and classifications assignment.
Once UpdateAssetLevelMetadata notebook is run, by default a folder will be created with this pattern ```{PurviewAccountName}_update``` which will host the PowerShell files along with all required .json payload files.
For safty reasons PowerShell files will have .ps1_ and will have to be renamed to .ps1.
The PowerShell file will include lines to set the environment variables which it read from .env file except for AZURE_CLIENT_SECRET. This value will have to be populated before the script can run.\
**This will not remove existing term assignments but will overwrite description for assets**

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