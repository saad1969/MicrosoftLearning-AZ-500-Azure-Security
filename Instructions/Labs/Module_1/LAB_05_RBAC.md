
### Module 1: Manage Identity and Access 


**Scenario**

In this module, you'll learn about Role-Based Access Control as the foundation to organizing and managing an organization's administrative access based on the principle of least privilege. You will also review Azure Active Directory concepts, as well as gaining insight into the threat landscape and security risks that are exposed to IT organizations through breach of privileged access. Lessons include:

- Role-Based Access Control
- Azure Active Directory (Refresher)
- Protecting Privileged Access in the Environment



**Note:** To save time and simplify the course the Azure PowerShell Module and Azure CLI have already been installed in the Virtual Machine for you.


### Lab 5: Introduction to Identity Protection in Azure

#### Exercise 1: Role-Based Access Control

##### Task 1: Create a User

1.  Sign in to the Azure portal **`https://portal.azure.com/`**

1.  Select **Azure Active Directory** and on the overview blade note down your tennant domain.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-5/fd34b4a3-fdd5-4645-bd50-357f28a3cc18.png)

1.  Select **Users**, and then select **New user**.

    ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-5/14707a08-08e2-4e69-adfe-3f1815358799.png)

3.  On the **User** page, fill out the blade with the following information:

  - **Name**: Bill Smith
  - **User name**: bill@:_yourdomainnotedabove_.onmicrosoft.com
</br>
    ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-5/d53ed503-451a-4179-83ec-4c0f506d32e6.png)

  - **Profile**: Optionally, you can add more information about the user. You can also add user information at a later time. For more information about adding user info, see [How to add or change user profile information](active-directory-users-profile-azure-portal.md).

  - **Groups.** Optionally, you can add the user to one or more existing groups. You can also add the user to groups at a later time. Do not select any groups.

    - **Directory role.** Optionally, you can add the user to a directory role. You can assign the user to be a global administrator, or to one or more of the other administrator roles in Azure AD. Leave Bill as a **User**.

4.  Copy the auto-generated password provided in the **Password** box. You'll need to give this password to the user for the initial sign-in process.
  
  ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-5/67f27ff1-7102-4a46-9d6b-47aef7fd0e10.png)

5.  Select **Create**.

    The user is created and added to your Azure AD tenant.

8.  Launch **Azure Cloud Shell** by clicking on the PowerShell icon at the top of the Azure Portal and select PowerShell if prompted.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-100T01/Module-1/f09adc12-9b84-4621-9a49-9eff7cd12740.png)
  
9.  **Enter the following commands** to create a user in the PS cloud shell **replacing yourdomain** with your domain noted down erlier

 ```powershell
  $PasswordProfile = New-Object -TypeName Microsoft.Open.AzureAD.Model.PasswordProfile
  $PasswordProfile.Password = "Pa55w.rd"
  New-AzureADUser -DisplayName "Mark" -PasswordProfile $PasswordProfile -UserPrincipalName  "Mark@yourdomain.onmicrosoft.com" -AccountEnabled $true -MailNickName "Mark"

 ```

10.  Run the following comamand to get a list of the users in Azure AD 

 ```powershell
Get-AzureADUSer 
 ```
 
11.  Change the Azure cloud shell to azure CLI mode with Bash by using the drop down menu

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-100T01/Module-1/760c0c1f-a88d-43e5-8bdb-61a795269798.png)

12.  Enter the following command in **azure CLI** to create a user in Azure CLI **replacing yourdomain** with the domain you noted earlier.
 
 ```cli
az ad user create --display-name Tracy --password Pa55w.rd --user-principal-name Tracy@yourdomain.onmicrosoft.com
 ```


You should now have 3 users in your Azure AD


##### Task 2: Create Groups In Portal, PowerShell, and CLI

1.  In the Azure Portal click **Azure Active Directory**  on the **Azure AD blade** click **Groups** and select **New group**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-100T01/Module-1/735e812c-f081-4264-871d-7ab7db7a03aa.png)
 
16.  Fill in the details with the following details:
  - **Name**: Senior Admins Group 
  - **Type**: Security Membership type=Assigned
  </br>
  
 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-100T01/Module-1/ca61d95a-944e-41d0-8ddc-b994d75d3a29.png)

17.  Click **Members** and select **Bill**

18.  Click **Create**

1.  Launch the **cloud Shell Bash** by clicking the PowerShell icon at the top of the Azure Portal.

19.  In the **Cloud Shell** enter the following command:

 ```cli
az ad group create --display-name ServiceDesk --mail-nickname ServiceDesk
 ```

20.  Change the Cloud Shell to **PowerShell** and enter the following command:

 ```powershell
New-AzureADGroup -DisplayName "Junior Admins" -MailEnabled $false -SecurityEnabled $true -MailNickName JuniorAdmins
 ```
 
1.  Exit the **Cloud Shell**.

21.  In the **Active Directory blade** click **Groups** and confirm you have **3** groups

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-100T01/Module-1/adc99df8-ca52-496f-b0c4-37aaaa8424ea.png)


### Practice - RBAC

##### Task 1: Create a resource group

1.  In the navigation list, choose **Resource groups**.

1.  Choose **Add** to open the **Resource group** blade.

1.  For **Resource group name**, enter **myRBACrg**.

1.  Select your subscription and the location of **East US**.

1.  Choose **Create** to create the resource group.

1.  Choose **Refresh** to refresh the list of resource groups.

   The new resource group appears in your resource groups list.

##### Task 2: Grant access


In RBAC, to grant access, you create a role assignment.


1.  In the list of **Resource groups**, choose the new **myRBACrg** resource group.

1.  Choose **Access control (IAM)** to see the current list of role assignments.

   ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-5/3269f66f-85d1-4d16-8949-a806f328d409.png)

1.  Choose **Add** to open the **Add permissions** pane.

   If you don't have permissions to assign roles, you won't see the **Add** option.

   ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-5/30708190-633d-4ae8-b49c-b34235fb3ae9.png)

1.  In the **Role** drop-down list, select **Virtual Machine Contributor**.

1.  In the **Select** list, select **Bill Smith**.

1.  Choose **Save** to create the role assignment.

   After a few moments, the user is assigned the Virtual Machine Contributor role at the rbac-quickstart-resource-group resource group scope.

   ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-5/f7c7074d-871c-465d-bd5a-d789f4665449.png)
  
##### Task 3: Remove access


In RBAC, to remove access, you remove a role assignment.


1.  In the list of role assignments, add a checkmark next to user with the Virtual Machine Contributor role.
  
  ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-5/79853837-e092-49da-95e3-28d8d651f0a5.png)

1.  Choose **Remove**.

   ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-5/f047eec2-0114-4a82-bd0a-39c87ca854f0.png)

1.  In the remove role assignment message that appears, choose **Yes**.  
   
  
###  Role-based Access Control (RBAC) using the PowerShell


In this practice you use PowerShell to :

-   Use the Get-AzureRMRoleAssignment command to list the role assignments
-   Use the Remove-AzureRmResourceGroup command to remove access


##### Task 1: Grant access
  

To grant access for the user, you use the New-AzureRmRoleAssignment command to assign a role. You must specify the security principal, role definition, and scope.  


1.  Launch the **Cloud Shell PowerShell**.
  
1.  Get the ID of your subscription using the Get-AzureRmSubscription command.
  
 ```powershell
Get-AzureRmSubscription
 ```
  
 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-5/d0f6e82c-d69e-465d-a84c-8f47f48ee959.png)
  
1.  Save the subscription scope in a variable replacing the 000000's with your subscription ID.
  
 ```powershell
$subScope = "/subscriptions/00000000-0000-0000-0000-000000000000" 
 ```  
  
  ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-5/4320d3ba-95bd-4e8e-9451-a0b1d89222a3.png)
  
1.  Assign the Reader role to the user at the subscription scope by using the follownig command (Replacing your domain with the tennant domain you noted earlier):
  
 ```powershell
New-AzureRmRoleAssignment -SignInName bill@yourdomain.onmicrosoft.com -RoleDefinitionName "Reader" -Scope $subScope  
 ```
  
  ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-5/b10a68cd-92bc-4b47-a943-3d751ebe4e5f.png)
  
1.  Assign the Contributor role to the user at the resource group scope using the following command:
  
 ```powershell
New-AzureRmRoleAssignment -SignInName bill@yourdomain.onmicrosoft.com -RoleDefinitionName "Contributor" -ResourceGroupName "myRBACrg"
 ```
  
  ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-5/db970abe-e031-4b3c-9fe0-d97da3821649.png)
  
##### Task 2: List access  
  
1.  To verify the access for the subscription, use the Get-AzureRmRoleAssignment command to list the role assignments use the following command:
  
 ```powershell
Get-AzureRmRoleAssignment -SignInName bill@yourdomain.onmicrosoft.com -Scope $subScope
 ```

   ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-5/15337ca8-d48f-475e-aaa0-d63c10fad39e.png)

  In the output, you can see that the Reader role has been assigned to the RBAC Tutorial User at the subscription scope.

2.  To verify the access for the resource group, use the Get-AzureRmRoleAssignment command to list the role assignments use the following command:
  
 ```powershell
Get-AzureRmRoleAssignment -SignInName bill@yourdomain.onmicrosoft.com -ResourceGroupName "myRBACrg"
 ```

   ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-5/8f8e79bc-224e-4946-91f7-4a57e4473f97.png)

 In the output, you can see that both the Contributor and Reader roles have been assigned to the RBAC Tutorial User. The Contributor role is at the rbac-tutorial-resource-group scope and the Reader role is inherited at the subscription scope.

##### Task 3: Remove access
  

To remove access for users, groups, and applications, use Remove-AzureRmRoleAssignment to remove a role assignment.


1.  Use the following command to remove the Contributor role assignment for the user at the resource group scope.
  
 ```powershell
Remove-AzureRmRoleAssignment -SignInName bill@yourdomain.onmicrosoft.com -RoleDefinitionName "Contributor" -ResourceGroupName "myRBACrg"
 ```
  
  ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-5/a83f0ca5-e110-492e-9fa2-f452563faedb.png)
  
1.  Use the following command to remove the Reader role assignment for the user at the subscription scope.

 ```powershell
Remove-AzureRmRoleAssignment -SignInName bill@yourdomain.onmicrosoft.com -RoleDefinitionName "Reader" -Scope $subScope
 ```
  
  ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-5/4e0b92e2-5d11-4fd6-878e-71d1037f23ca.png)
  
1.  Remove the resource group by running the following command (When prompted to confirm press Y and press enter):
  
 ```powershell
Remove-AzureRmResourceGroup -Name "myRBACrg".  
 ```

1.  Close the **Cloud Shell**.  


**Results**: You have now completed this module.


**Congratulations**! You can now end the lab ready to coninue with your next module.

