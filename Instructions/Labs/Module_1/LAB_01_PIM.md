# Module 1: Lab 1 - Azure AD Privileged Identity Management

## Scenario

In this lab, you'll learn how to use Azure Privileged Identity Management (PIM) to enable just-in-time administration and control the number of users who can perform privileged operations. You'll also learn about the different directory roles available as well as newer functionality that includes PIM being expanded to role assignments at the resource level. Lessons include:

- Getting Started with PIM
- PIM Security Wizard
- PIM for Directory Roles
- PIM for Role Resources

✔️ The Managing Identities course also covers Azure RBAC and Azure Active Directory. This content has been included here also to provide more context and foundation for the remainder of the course.


#### Azure AD Privileged Identity Management

#### Exercise 1 - Discover and Manage Azure Resources

##### Task 0: Lab Setup

This lab requires a user cerating that will be used for PIM.


1.  Run the following PowerShell Commands in the Azure cloud shell to create an AD user and password in your default domain

 ```powershell
$PasswordProfile = New-Object -TypeName Microsoft.Open.AzureAD.Model.PasswordProfile
 ```
 ```powershell
$PasswordProfile.Password = "Pa55w.rd"
 ```
 ```powershell
$domainObj = get-azureaddomain
 ```
 ```powershell
$domain = $domainObj[0].name
 ```
 ```powershell
New-AzureADUser -DisplayName "Isabella Simonsen" -PasswordProfile $PasswordProfile -UserPrincipalName "Isabella@$domain" -AccountEnabled $true -MailNickName "Isabella"
 ```

##### Task 1: Discover resources

1.  Sign in to the Azure portal.

1.  Open **Azure AD Privileged Identity Management**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/7a7347d8-412f-413a-859c-71228e73ba7d.png)

1.  Click consent to PIM.
warning
**Note**: If you have already setup MFA you may not need to complete the next few steps.


 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/7a514236-21db-4e8b-a02a-f2ab92a62fa6.png)

1.  Click **Verify my identity**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/9f13d135-995e-42af-a5e3-d20013b6b4a7.png)

1.  Clikc **Next**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/2f736633-f40d-4d8a-8a5f-50981b66b09c.png)

1.  Enter your mobile/cell phone details and click **Next*.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/5d27478d-3688-4e46-9538-5fbd36e02c0d.png)
 
1.  Enter the code when you receive it via SMS and click **Verify**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/82dcbc46-bf36-4b76-95c9-b837d46741eb.png)

1.  Back on the **Concent to PIM blade** click **Consent** and click **Yes**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/7b75c9aa-a95e-4b69-887a-523e4b780aa3.png)

1.  Click **Azure resources**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/6b0a6758-b47f-4ae5-bbcd-428831a59cf4.png)


1.  Click **Discover resources** to launch the discovery experience.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/5afe0f50-0da6-48ee-8307-c2de30342a6b.png)


1.  On the Discovery pane, use **Resource state filter** and **Select resource type** to filter the management groups or subscriptions you have write permission to. It's probably easiest to start with **All** initially.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/41139025-cf3c-4ee9-97f2-7b06e614174f.png)

1.  Add a checkmark next to your Azure subscription.
   
 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-103T00/Module-10/879578bd-74d0-46da-aac7-61275653b9c2.png)

1.  Click **Manage resource** to start managing the selected resources.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/2abc95b8-26a7-4466-bddf-b84665b1fa2c.png)

1.  Click **Yes** when prompted.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-103T00/Module-10/c4bee645-754c-4585-9a23-87f2e4573dad.png)
warning
**Note**: You can only search for and select management group or subscription resources to manage using PIM. When you manage a management group or a subscription in PIM, you can also manage its child resources.

warning
**Note**: Once a management group or subscription is set to managed, it can't be unmanaged. This prevents another resource administrator from removing PIM settings.


#### Practice - Assign Directory Roles

##### Task 1:  Make a user eligible for a role

In the following task you will make  a user eligible for an Azure AD directory role.


1.  Sign in to Azure portal

1.  Open **Azure AD Privileged Identity Management**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-103T00/Module-10/7c5bc8dc-c7a8-455e-bb05-aa76a3e4571b.png)

1.  Select **Azure AD Roles**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-103T00/Module-10/6d452230-df27-467d-a104-299b7a9c3558.png)

1.  Click **Sign up PIM for Azure AD Roles**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/5c2cdbf4-7573-451a-bb55-6ade5c5e79cc.png)


1.  Click **Sign Up** and click **Yes**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/611ca1e6-d4d7-4749-a7b9-38c5010f7a74.png)

1.  **Refresh the Broswer**.

1.  Click **Roles**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-103T00/Module-10/c5f57c37-3632-4267-ba9c-9f8801bbf8b9.png)


1.  Click **Add member** to open Add managed members.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/6d01a24f-7346-45de-b575-801eff33dafb.png)

1.  Click **Select a role**, and lick **Billing Administrator** and then click  **Select**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/5600566b-7ef9-46bb-bb5f-0a4ac662465e.png)

1.  Click **Select members**, select Isabella and then click **Select**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/3f73f083-9dde-4dac-99ad-3a802e102b87.png)

1.  In Add managed members, click **OK** to add the user to the role.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/c752ddbd-ce16-472a-bb7e-8c5ae3454255.png)

1.  In the list of roles, click the role you just assigned to see the list of members.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/2b1a5b42-91fa-477e-ae4d-14ab969cb67b.png)

1.  Review the added memeber

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/daff233f-dc8a-4ca8-a3a4-748a5ec40031.png)

1.  When the role is assigned, the user you selected will appear in the members list as **Eligible** for the role.


##### Task 2: Make a role assignment permanent

By default, new users are only eligible for a directory role. Follow these steps if you want to make a role assignment permanent.


1.  Open **Azure AD Privileged Identity Management**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-103T00/Module-10/7c5bc8dc-c7a8-455e-bb05-aa76a3e4571b.png)

1.  Click **Azure AD directory roles**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/9c62581f-2b37-4a3b-8ba9-b9eb9dc6f26b.png)

1.  Click **Members**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/a765bcf9-2f50-43d3-b93f-960400e3be46.png)

1.  Click the **Eligible** role that you want to make permanent.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/29a7ba06-ae58-4d35-8f3e-d6d41d43c420.png)
 
1.  Click **More** and then click **Make permanent**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/e54b9bca-3688-489d-84c9-00e5fd987706.png)
 
success
**Results**: The role is now listed as **permanent**.


##### Task 3: Remove a user from a role

You can remove users from role assignments, but make sure there is always at least one user who is a permanent Global Administrator.



1.  Open **Azure AD Privileged Identity Management**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-103T00/Module-10/7c5bc8dc-c7a8-455e-bb05-aa76a3e4571b.png)

1.  Click **Azure AD directory roles**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/9c62581f-2b37-4a3b-8ba9-b9eb9dc6f26b.png)

1.  Click **Members**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/a765bcf9-2f50-43d3-b93f-960400e3be46.png)

1.  Click a role assignment you want to remove.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/7884b324-1146-4526-9ba0-bfe2e5f7b010.png)
1.  Click **More** and then click **Remove**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/b3ad0069-c75a-40f8-b1e0-e49d50586e83.png)
 
1.  In the message that asks you to confirm, click **Yes**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/7caca5ff-ca42-4934-8d1e-b3afe789b2c4.png)

1.  The role assignment is removed.



#### Practice - Activate and Deactivate PIM Roles

##### Task 1: Activate a role

When you need to take on an Azure AD directory role, you can request activation by using the **My roles** navigation option in PIM.


1.  Sign in to the Azure portal **`https://portal.azure.com`**

1.  Open **Azure AD Privileged Identity Management**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-103T00/Module-10/7c5bc8dc-c7a8-455e-bb05-aa76a3e4571b.png)

1.  Click **Azure AD Roles**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-103T00/Module-10/7058acfe-467d-4c48-b767-de670788e714.png)

1.  Click **Quick Start** and cliuck **Assign eligibility**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-103T00/Module-10/de83dea3-14b9-444b-9918-bcda31ad0d29.png)

1.  Click **Billing Administrator** and add Isabella back into the **Billing Administrators** role.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/a37dce38-95dd-4986-a76c-c9fbf5294bca.png)


1.  Open an **In Private** browsing session and navigate to portal.azure.com and login as **Isabella**.  You may need to confirm the details for MFA.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-103T00/Module-10/d57267d7-fad5-4605-ad20-7379192570cb.png)

1.  Open **Azure AD Privileged Identity Management**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-103T00/Module-10/5dfcdd0a-410d-4af0-9e02-f712ad13c276.png)

1.  Click **Azure AD Roles**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-103T00/Module-10/55058f35-6592-46b4-95a2-2c98e8c2ccd8.png)

1.  Click **Quick start** and click **Activate your role**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-103T00/Module-10/fbe71f05-0b9e-4947-9dcc-ac9e708df6c4.png)

1.  On the Billing Administrator role, scroll to the right and click **Activate**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-103T00/Module-10/1fc30488-bd3e-40fe-b433-2cfe2a357662.png)

1.  Click **Activate** to open the Role activation details pane.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-103T00/Module-10/be71f369-343c-41f6-a5ef-d77743d7d9ae.png)

1.  **IF** your role requires multi-factor authentication (MFA), click **Verify your identity before proceeding**. You only have to authenticate once per session.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-103T00/Module-10/48e16e7c-a2de-4aa3-90c7-a5a381f82839.png)


1.  In the **Activation reason** box, enter the reason for the activation request. 


1.  Click **Activate**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-103T00/Module-10/668bd979-82df-45fa-b839-6240f4c5e67a.png)

 If the role does not require approval, it is activated and added to the list of active roles. If you want to use the role right away, follow the steps in next section.

 If the role requires approval to activate, a notification will appear in the upper right corner of your browser informing you the request is pending approval.


##### Task 2: Use a role immediately after activation

When you activate a role in PIM, it can take up to 10 minutes before you can access the desired administrative portal or perform functions within a specific administrative workload. To force an update of your permissions, use the **Application access** page as described in the following steps.


1.  Click **Sign Out**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-103T00/Module-10/fd853a1e-3033-423f-aeea-d769f5d811ef.png)

1.  Log back in as Isabella.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-103T00/Module-10/6fa95f13-6160-4bc8-95aa-fd08bccc9a4c.png)

##### Task 3: View the status of your requests

You can view the status of your pending requests to activate.


1.  Still signed in as **Isabella**, open **Azure AD Privileged Identity Management**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-103T00/Module-10/4d9be542-9fcf-4bf7-abbb-0e10fb1d44e4.png)

1.  Click **Azure AD Roles**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-103T00/Module-10/8ef3ef56-772f-4c57-9192-3dd740f405d9.png)

1.  Click **My requests** to see a list of your requests.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-103T00/Module-10/2098e2fa-4043-4179-af81-cf8111b33b3c.png)


##### Task 4: Deactivate a role

Once a role has been activated, it automatically deactivates when its time limit (eligible duration) is reached.

If you complete your administrator tasks early, you can also deactivate a role manually in Azure AD Privileged Identity Management.



1.  Still signed in as **Isabella**, open Azure AD Privileged Identity Management.

1.  Click **Azure AD roles**.

1.  Click **My roles**.

1.  Click **Active roles** to see your list of active roles.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-103T00/Module-10/f7012537-0755-42e3-8d88-265426137062.png)

1.  Find the role you're done using and then click **Deactivate**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-103T00/Module-10/abb17665-04e8-4496-8939-f868eca6b8c0.png)

1.  Click **Deactivate** again.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-103T00/Module-10/fe8993f3-4c46-475d-94a5-9d003b1870a6.png)

1.  Click **Yes** to confirm.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-103T00/Module-10/9b169dd6-f374-4ed4-ada8-711c57da3bca.png)

##### Task 5: Cancel a pending request

If you do not require activation of a role that requires approval, you can cancel a pending request at any time.


1.  Open Azure AD Privileged Identity Management.

1.  Click **Azure AD roles**.

1.  Click **My requests**.

1.  For the role that you want to cancel, click the **Cancel** button.
warning
**Note**: The cancel button in this task is greyed out as the request was approved.
When you click Cancel, the request will be cancelled. To activate the role again, you will have to submit a new request for activation.


#### Practice - Directory Roles (General)

##### Task 1: Start an access review for Azure AD directory roles in PIM

Role assignments become "stale" when users have privileged access that they don't need anymore. In order to reduce the risk associated with these stale role assignments, privileged role administrators or global administrators should regularly create access reviews to ask admins to review the roles that users have been given. This task covers the steps for starting an access review in Azure AD Privileged Identity Management (PIM).


1.  Return back to the browser which is logged in as your Global Admin Account.

1.  From the PIM application main page click **Azure AD Roles** under the **Manage** section click **Access reviews** and click > **New**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/60281a0a-b018-4a6d-af82-5d3c899e8248.png)

1.  Enter the following details and click **Start**:

  - Review name:  **Global Admin Review**
  - Frequency: **One TIme**
  - Start Date:  **Todays Date** 
  - End Date:  **End of next month**
  - Review role Membership:  **Global Administrator**
 </br>
 
 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/467f0422-a813-43f4-817d-6158291637b9.png)
 
1.  Once the review has completed and has a status of Active.  Click on the **Global Admin Review**.

1.  Select Results and see the outcome of **Not reviewed**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/94afa05d-ec29-4ed9-a2e6-2425581f2f88.png)

##### Task 2: Approve or deny access

When you approve or deny access, you're just telling the reviewer whether you still use this role or not. Choose Approve if you want to stay in the role, or Deny if you don't need the access anymore. Your status won't change right away, until the reviewer applies the results. Follow these steps to find and complete the access review:


1.  In the PIM application, select **Review access**. 

2.  Select the **Global Admin Review**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/7781565d-4a63-4732-8bf6-7754975b7c7a.png)

3.  Unless you created the review, you appear as the only user in the review. Select the check mark next to your name.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/87c1b43e-7a33-4df8-bcb2-7f478e66964c.png)

4.  Choose **Approve**. You will need to include a reason for your decision in the **Provide a reason** text box.  

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/5180879d-a00c-4e6c-80e4-cab8c24fe9b8.png)

5.  Close the **Review Azure AD roles** blade.

##### Task 3: Complete an access review for Azure AD directory roles in PIM

Privileged role administrators can review privileged access once an access review has been started. Azure AD Privileged Identity Management (PIM) will automatically send an email prompting users to review their access. If a user did not get an email, you can send them the instructions in how to perform an access review.

After the access review period is over, or all the users have finished their self-review, follow the steps in this task  to manage the review and see the results.



1.  Go to the Azure portal and select the **Azure AD Privileged Identity Management**.

1.  Select **Azure AD Roles**.

2.  Select the **Access reviews**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/63380d00-02e1-4d17-be5c-6ee67b83f7ba.png)

3.  Select the Global Admin Review.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/fdc49a4b-b608-4c29-a4c4-9f35ac6336a7.png)

1.  On the access review's detail blade, there are a number options for managing that review.

  - **Remind** - If an access review is set up so that the users review themselves, the **Remind** button sends out a notification. 
  - **Stop** - All access reviews have an end date, but you can use the **Stop** button to finish it early. If any users haven't been reviewed by this time, they won't be able to after you stop the review. You cannot restart a review after it's been stopped.
  - **Apply** - After an access review is completed, either because you reached the end date or stopped it manually, the **Apply** button implements the outcome of the review. If a user's access was denied in the review, this is the step that will remove their role assignment.  
  - **Export** - If you want to apply the results of the access review manually, you can export the review. The **Export** button will start downloading a CSV file. You can manage the results in Excel or other programs that open CSV files.
  - **Delete** - If you are not interested in the review any further, delete it. The **Delete** button removes the review from the PIM application.
</br>

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/8403c678-2908-4068-b0de-2308f07689ee.png)


##### Task 4: Configure security alerts for Azure AD directory roles in PIM

You can customize some of the security alerts in PIM to work with your environment and security goals. Follow these steps to open the security alert settings:



1.  Open **Azure AD Privileged Identity Management**.

1.  Click **Azure AD roles**.

1.  Click **Settings** and then **Alerts**.

    ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/fc29b855-0bac-4e35-964a-1347a626dc23.png)

1.  Click an alert name to configure the setting for that alert.

    ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/32d3778c-e568-4d49-afd2-8cd6aec14191.png)

1.  You can find more information about each alert here: **`https://docs.microsoft.com/en-us/azure/active-directory/privileged-identity-management/pim-how-to-configure-security-alerts`**

#### Practice - PIM Resource Workflows

##### Task 1:  Configure the Global Administrator role to require approval.

1.  Open **Azure AD Privileged Identity Management**.

1.  Click **Azure AD roles**.

1.  Click **Settings** 

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/4b416b8f-7b48-44b9-8b2b-3d30acc398e0.png)

1.  Click **Roles** and select **Global Administrator**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/1e83c190-4840-417f-b4a3-c5e7bca38874.png)

1.  Scroll down and change **Require Approbal** to **Enable** and click **Save**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/036c737d-ebec-45d9-9263-c9ad0c1b0168.png)


##### Task 2: Enable Isabella for Global Administrator privliges.

1.  Open **Azure AD Privileged Identity Management**.

1.  Click **Azure AD roles**.

1.  Click the **Quick Start** and select **Assign eligibility**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/7be34226-1975-4a06-8f06-0187c1e361e7.png)

1.  Select **Global Administrator**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/28c616ce-6224-4a55-8ee6-69cfd4ccf9e5.png)

1.  Select **+ Add Member** and select **Isabella**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/47ca1f15-0fa6-49eb-94be-96fa158d4aa3.png)

1.  Open an in Private Browsing session and login to portal.azure.com as Isabella.

1.  Open **Azure AD Privileged Identity Management**.

1.  Select **My Roles**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/e3dc655f-dd4a-47ed-8072-d0b03e886fe8.png)

1.  **Activate** the Global Administrator Role.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/9d9caf35-a335-40f3-8bc5-78d3491c5070.png)

1.  Click **Activate**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/a911964e-9dc4-41b7-ab6e-d2c39330b88f.png)

1.  Enter the justification **I need to carry out some administrative tasks** and click **Acitvate**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/810b1a97-2206-49ab-b1c1-bbff3cbf5b81.png)


##### Task 3: Approve or deny requests for Azure resource roles in PIM

With Azure AD Privileged Identity Management (PIM), you can configure roles to require approval for activation, and choose one or multiple users or groups as delegated approvers. Follow the steps in this article to approve or deny requests for Azure resource roles.


###### View pending requests

As a delegated approver, you'll receive an email notification when an Azure resource role request is pending your approval. You can view these pending requests in PIM.


1.  Switch back to the browser you are signed in with your Gloabl Administrative account.

1.  Open **Azure AD Privileged Identity Management**.

1.  Click **Approve requests**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/6c3f71e4-2d27-4b09-a483-4c560720dc7d.png)

1.  Click the request from Isabella and click **Approve**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/30f454d8-b11d-401f-8554-74f8a19c356a.png)

1.  Enter a reason **Granted for this task"" and click **Approve**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/bfe833b9-6321-4c28-af5e-23b0fff9cbee.png)

1.  A notification appears with your approval.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/11fb2ad1-597f-4bbe-bb17-4d2c3005246e.png)

1.  Switch back to the In Private Browsing session where Isabella is signed in and click My Roles and note the status is now approved.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-3/ac133677-9cf2-4584-8a87-8134041ee321.png)

#### Exercise 2 - View audit history for Azure AD roles in PIM

You can use the Azure Active Directory (Azure AD) Privileged Identity Management (PIM) audit history to see all the role assignments and activations within the past 30 days for all privileged roles. If you want to see the full audit history of activity in your directory, including administrator, end user, and synchronization activity.


##### Task 1: View audit history

Follow these steps to view the audit history for Azure AD roles.


1.  Open **Azure AD Privileged Identity Management**.

1.  Click **Azure AD roles**.

1.  Click **Directory roles audit history**.

    Depending on your audit history, a column chart is displayed along with the total activations, max activations per day, and average activations per day.

    ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-1/a1da83d8-cee6-4afb-a233-be511e10623f.png)

    At the bottom of the page, a table is displayed with information about each action in the available audit history. The columns have the following meanings:

    | Column | Description |
    | --- | --- |
    | Time | When the action occurred. |
    | Requestor | User who requested the role activation or change. If the value is **Azure System**, check the Azure audit history for more information. |
    | Action | Actions taken by the requestor. Actions can include Assign, Unassign, Activate, Deactivate, or AddedOutsidePIM. |
    | Member | User who is activating or assigned to a role. |
    | Role | Role assigned or activated by the user. |
    | Reasoning | Text that was entered into the reason field during activation. |
    | Expiration | When an activated role expires. Applies only to eligible role assignments. |

1.  To sort the audit history, click the **Time**, **Action**, and **Role** buttons.

##### Task 2: Filter audit history

1.  At the top of the audit history page, click the **Filter** button.

    The **Update chart parameters** pane appears.

1.  In **Time range**, select a time range.

1.  In **Roles**, add checkmarks for the roles you want to view.

    ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-1/d557c321-1350-4c39-babe-43bfda4b1562.png)

1.  Click **Done** to view the filtered audit history.


success
**Results**: You have now completed this module.

info
**Congratulations**! You can now continue with your next lab by clicking the drop down menu at the top of the lab guide.

