# Manage Governance via Azure Policy

## Objective

In this lab, I learnt how to implement an organization’s governance plans. We learn how Azure policies can ensure operational decisions are enforced across the organization. I learnt how to use resource tagging to improve reporting.


*Ref 1: Architecture diagram*
 ![image](https://github.com/user-attachments/assets/d59d93aa-8639-46c2-ad36-8e589fe34e35)


### Job Skills Learned

- Create and assign tags via the Azure portal.
- Enforce tagging via an Azure Policy.
- Apply tagging via an Azure Policy.
- Configure and test resource locks.

### Tools Used

- Azure portal - https://portal.azure.com


## Steps

## Task 1: Assign tags via the Azure portal
In this task, you will create and assign a tag to an Azure resource group via the Azure portal. Tags are a critical component of a governance strategy as outlined by the Microsoft Well-Architected Framework and Cloud Adoption Framework. Tags can allow you to quickly identify resource owners, sunset dates, group contacts, and other name/value pairs that your organization deems important. For this task, you assign a tag identifying the resource role (‘Infra’ for ‘Infrastructure’).
1.	Sign in to the Azure portal - https://portal.azure.com.
2.	Search for and select Resource groups.
3.	From the Resource groups, select + Create.
4.	Select Next: Tags and create a new tag.
5.	Select Review + Create, and then select Create.
 ![image](https://github.com/user-attachments/assets/51d45334-5e18-41f3-87ea-46e28ccd036e)
![image](https://github.com/user-attachments/assets/95cb7667-2249-4c7e-aa5e-e2c20c75e24a)


 
## Task 2: Enforce tagging via an Azure Policy
In this task, you will assign the built-in Require a tag and its value on resources policy to the resource group and evaluate the outcome. Azure Policy can be used to enforce configuration, and in this case, governance, to your Azure resources.
1.	In the Azure portal, search for and select Policy.
2.	In the Authoring blade, select Definitions. Take a moment to browse through the list of built-in policy definitions that are available for you to use. Notice you can also search for a definition.
![image](https://github.com/user-attachments/assets/39c08caa-6308-403c-b5a6-08c709df6a5d)
 
3.	Click the entry representing the Require a tag and its value on resources built-in policy. Take a minute to review the definition.
4.	On the Require a tag and its value on resources built-in policy definition blade, click Assign.
5.	Specify the Scope by clicking the ellipsis button and selecting the following values. Click Select when you are done.
![image](https://github.com/user-attachments/assets/579888ff-26e1-4e33-bbfa-3726f5527641)
 
6.	Configure the Basics properties of the assignment by specifying the following settings (leave others with their defaults):
7.	Click Next and set Parameters to the following values:
8.	Click Next and review the Remediation tab. Leave the Create a Managed Identity checkbox unchecked.
9.	Click Review + Create and then click Create.
![image](https://github.com/user-attachments/assets/857315d1-39af-4838-ad0a-dab7922ebc3b)
 
10.	In the portal, search for and select Storage Account, and select + Create.
11.	On the Basics tab of the Create storage account blade, complete the configuration.
![image](https://github.com/user-attachments/assets/738ec031-fc0e-4f02-899c-452b3c3efcb1)
 
12.	Select Review and then click Create.
13.	You should receive a Validation failed message. View the message to identify the reason for the failure. Verify the error message states that the resource deployment was disallowed by the policy.
![image](https://github.com/user-attachments/assets/47bc5fa3-f39d-40e8-979a-ac7bdcbae914)
 
The deployment failed because the storage account we attempted to create did not have a tag named Cost Center with its value set to Default.
![image](https://github.com/user-attachments/assets/e145dbcb-070f-4da7-be57-863b0124773b)
 

## Task 3: Apply tagging via an Azure policy
In this task, we will use the new policy definition to remediate any non-compliant resources. In this scenario, we will make any child resources of a resource group inherit the Cost Center tag that was defined on the resource group.
1.	In the Azure portal, search for and select Policy.
2.	In the Authoring section, click Assignments.
3.	In the list of assignments, click the ellipsis icon in the row representing the Require Cost Center tag with Default value policy assignment and use the Delete assignment menu item to delete the assignment.
![image](https://github.com/user-attachments/assets/1396c940-efad-428a-8a12-2f262881e975)
 
4.	Click Assign policy and specify the Scope by clicking the ellipsis button and selecting the following values:
![image](https://github.com/user-attachments/assets/2a87af9d-7317-4b1a-bcbe-6696a41ce4a8)


5.	To specify the Policy definition, click the ellipsis button and then search for and select Inherit a tag from the resource group if missing.
![image](https://github.com/user-attachments/assets/b972365d-4884-4826-addf-17ace724bc50)
 
6.	Select Add and then configure the remaining Basics properties of the assignment.
![image](https://github.com/user-attachments/assets/27893d11-88c5-44f2-b904-81caa33893f0)
![image](https://github.com/user-attachments/assets/d72b37c8-a2d1-4daa-a9d5-a102a1d5962f)
 
 
7.	Click Next twice and set Parameters to the following values:
![image](https://github.com/user-attachments/assets/0846851c-3c0c-4015-b322-333930c7f2f0)
 
8.	Click Next and, on the Remediation tab, configure the following settings (leave others with their defaults):
![image](https://github.com/user-attachments/assets/5acf051b-182a-4d7c-aa9e-6fab7c32cdcb)
 
9.	Click Review + Create and then click Create.
10.	Search for and select Storage Account, and click + Create.
11.	On the Basics tab of the Create storage account blade, verify that you are using the Resource Group that the Policy was applied to and specify the following settings (leave others with their defaults) and click Review:
![image](https://github.com/user-attachments/assets/6df227f6-1708-4928-a5ef-2ea523960645)
 
12.	Verify that this time the validation passed and click Create.
![image](https://github.com/user-attachments/assets/4a89cdc7-2a5d-4502-8932-d2d9633b241b)
 
13.	Once the new storage account is provisioned, click Go to resource.
![image](https://github.com/user-attachments/assets/d4a14e78-f16f-4c43-8aef-42e71e8575f2)

14.	On the Tags blade, note that the tag Cost Center with the value 000 has been automatically assigned to the resource.
![image](https://github.com/user-attachments/assets/74d08bbf-2d8e-47cf-b0d2-5876017d67a7)
 
## Task 4: Configure and test resource locks
In this task, you configure and test a resource lock. Locks prevent either deletions or modifications of a resource.
1.	Search for and select your resource group.
2.	In the Settings blade, select Locks.
3.	Select Add and complete the resource lock information. When finished select Ok.
![image](https://github.com/user-attachments/assets/7bf6e522-584b-48e2-91e5-4d451b5135e0)
 
4.	Navigate to the resource group Overview blade, and select Delete resource group.
5.	In the Enter resource group name to confirm deletion textbox provide the resource group name, az104-rg2. Notice you can copy and paste the resource group name.
![image](https://github.com/user-attachments/assets/e7074ae6-a11d-4a1e-8700-8ab9c5c60e40)
 
6.	Notice the warning: Deleting this resource group and its dependent resources is a permanent action and cannot be undone. Select Delete.
7.	You should receive a notification denying the deletion.
![image](https://github.com/user-attachments/assets/19b36eab-1d01-4ec0-8f8c-1170280dd579)
 
## Note: You will need to remove the lock if you intend to delete the resource group.
