# Introduction 
Deploying Power BI reports using Azure DevOps involves creating a pipeline that automates the process of publishing the reports to a Power BI workspace. Here's a step-by-step guide for setting up a DevOps pipeline for deploying Power BI reports:

# Prerequisites
1. Power BI Service Account: This account should have appropriate permissions in the target Power BI workspace (e.g., Admin or Member).
2. Azure DevOps Account: You need an Azure DevOps organization and project.
3. Power BI Service Principal or App Registration: Create an Azure AD app registration and configure it with necessary API permissions to the Power BI Service. Create a secret for the app
4. Create a Keyvalut in azure and under Access Control-> Role assignment -> add the service principal -> roles : Keyvault Secret Officer
5. Store the secret in a secure store/ Azure Keyvault6.
6. Create a Service connection in Azure Devops, the service connetion will be used in the pipeline to securely retrieve the app Secreat from teh KeyVault
7. Power BI Workspace: The workspace where the reports will be deployed.
8. Power BI Rest API: Familiarity with Power BI Rest API, which is used to automate report deployments.

# Step 1: Create a Service Principal in Azure AD
1. Go to Azure Active Directory and create a new App Registration.
2. Configure the API permissions:
3. Add Power BI Service permissions (Tenant.Read.All, Tenant.ReadWrite.All).
4. Add Delegated permissions as needed.
5. Assign admin consent for the permissions.

# Step 2: Add the Service Principal to Power BI Workspace
1. Go to the Power BI Service.
2. Navigate to the target workspace.
3. Add the service principal as a member or admin of the workspace.

# Step 3: Prepare the PBIX File in Source Control 
1. Store the .pbix file in a repository in Azure DevOps (Git or TFVC).
2. Ensure that the repository is connected to your project in Azure DevOps.

# Step 4: Create a Release Pipeline in Azure DevOps
1. Navigate to the Pipelines section in Azure DevOps and select Create Pipeline.
2. Choose your repository where the .pbix file is stored.
3. Select Starter Pipeline or define a pipeline in YAML.
   (Refer the YML Pipeline in the repo.)
4. Under Variables: add your Tenant, Powerbiworkspace name, ID, App REgistration ID etc
   ![image](https://github.com/user-attachments/assets/2474290a-5863-4d51-a645-d4ce9a3b79c8)

6. Rename your service connection in teh Azure Key Vault task or use the same name

![image](https://github.com/user-attachments/assets/d6595d3a-d8f4-4bc6-b6cb-189815bb8cc4)

7. Update the report folder path from the repo:
![image](https://github.com/user-attachments/assets/79f9f777-bebc-4c47-b8e2-d392c9b83972)   

# Step 5: Automate and Test
1. Test the pipeline by triggering it manually.
2. Verify that the Power BI report is updated in the target workspace.

# Important Considerations
1. Automation Authentication: Make sure the service principal has appropriate permissions in both Azure and Power BI Service.
2. File Path Management: Use the correct path to the .pbix file from the build artifact.
3. Error Handling: Implement logging and error handling to capture any issues during deployment.
