# OnBoarding Subscriptions in Management-Group to Azure Light House
Steps to Onboard all the Subscriptions in Management Group to the Azure Light House

1)	Login to the Customer tenant with the user having Owner access to the Management Group
2)	Execute the attached PowerShell script. The description of the scripts are as below : 
deployLighthouseIfNotExistsManagementGroup.parameters.json – It contain the ARM template written by Microsoft to delegate the Subscription in the Management Group to the Service Provider Tenant. No changes has to be performed in this file.
deployLighthouseIfNotExistManagementGroup.json contains the parameters. Please update the parameters in the file such as Tenant ID of the Service Provider Tenant Name, Object ID of the Security Group of the Service Provider Tenant, Security Group Name and RBAC ID of the specific role which you want to assign to the group
3)	Execute the above PowerShell script using below command
New-AzManagementGroupDeployment -Name <DeploymentName> -Location <location> -ManagementGroupId <ManagementGroupName> -TemplateFile <path to file> -TemplateParameterFile <path to parameter file> -verbose
4)	Once the script is executed successfully, go to Policies and click on Definitions. You will be able to see the Policy “Enforce Lighthouse on Subscriptions” . This policy will reflect under the scope of Management Group.
![image](https://github.com/user-attachments/assets/cefc1916-7434-4c7f-be03-cd0a0070a6b3)
5) Click on the Policy and Assign the Policy at the Management Group level
   ![image](https://github.com/user-attachments/assets/ae45e653-f828-4248-bb0d-674309c9e8ac)
6) Once the policy is assigned, click on Compliance to see the Compliance state. The existing resource will be in the Non Compliant state. This is because the policy will be applied automatically to the new subscriptions which will be added to the management group in future. However, the policy will not be applied automatically to the existing subscriptions in the management group. To make the existing subscriptions in the management group complaint with the policy, you have to create Remediation task
   ![image](https://github.com/user-attachments/assets/271a228a-c5fb-4cc2-ad30-e90b0c004bff)
7) You can see the remediation in remediation blade once the task is created and applied
   ![image](https://github.com/user-attachments/assets/d9f727f0-cddb-46ab-aa5d-82e4b756d934)
8) Once the remediation is completed, you will see the compliance state as compliant
   ![image](https://github.com/user-attachments/assets/9f6474b3-49aa-406c-89d9-dbd559777603)
9) Once, the compliance state is compliant, the customers subscriptions will be successfully onboarded

Confirm Successful Onboarding
1)	In the Service Provider Tenant, login with the user who is the member of Security Group
2)	Click on Portal Settings | Directories + subscriptions, the customers tenants are visible
3)	Under Current + delegated directories, click on all the customers tenant and under Subscriptions you can see all the delegated subscriptions. Click on all the      subscriptions
![image](https://github.com/user-attachments/assets/e5b7e7ca-742c-4eaf-90ef-ab1a83d5b400)
![image](https://github.com/user-attachments/assets/107e7544-825b-4506-934e-f938bdb20952)
4) In the Service Provider tenant, click on My Customers and Customers. Here, you will be able to see the customer tenants and the delegated subscriptions
![image](https://github.com/user-attachments/assets/1dab9dc6-e861-4e42-a76f-5c7fb903ca51)
5) All the resources present in the customers subscription are now visible in thew Service Provider tenant. Service provider can efficiently manage (perform any management task) on these resources without need to change the directory.


