

### Module 1: Manage Identity and Access 


Your corporate standards and service level agreements. In this lab, you will learn to use Azure Policy to do some of the more common tasks related to creating, assigning, and managing policies across your organization, such as:

> - Assign a policy to enforce a condition for resources you create in the future
> - Create and assign an initiative definition to track compliance for multiple resources
> - Resolve a non-compliant or denied resource
> - Implement a new policy across an organization




### Lab 6: Azure Policy

#### Exercise 1: Understanding how to create and manage policies in Azure is important for staying compliant with

##### Task 1: Assign a policy


The first step in enforcing compliance with Azure Policy is to assign a policy definition. A policy definition defines under what condition a policy is enforced and what effect to take. In this example, assign a built-in policy definition, called *Require SQL Server version 12.0*, to enforce the condition that all SQL Server databases must be v12.0 to be compliant.


1.  Launch the Azure Policy service in the Azure portal by clicking **All services**, then searching    for and selecting **Policy**.

   ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-1/359afeec-7ffd-4ab0-bc13-d21cc14d10c9.png)

1.  Select **Assignments** on the left side of the Azure Policy page. An assignment is a policy that
   has been assigned to take place within a specific scope.

   ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-1/6ae456b6-7e36-4fe8-80bf-f7da9286a5c0.png)

1.  Select **Assign Policy** from the top of the **Policy - Assignments** page.

   ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-1/7722fe4f-de2f-432c-87b9-cf6dacea8d3b.png)

1.  On the **Assign Policy** page, select the **Scope** by clicking the ellipsis and selecting either    a management group or subscription. Optionally, select a resource group. A scope determines what resources or grouping of resources the policy assignment gets enforced on. Then click **Select** at the bottom of the **Scope** page.

   This example uses the **Contoso** subscription. Your subscription may differ.

1.  Resources can be excluded based on the **Scope**. **Exclusions** start at one level lower than the level of the **Scope**. **Exclusions** are optional, so leave it blank for now.

1.  Select the **Policy definition** ellipsis to open the list of available definitions. You can  filter the policy definition **Type** to *Built-in* to view all and read their descriptions.

1.  Select **Require SQL Server version 12.0**. If you can't find it right away, type **require sql server** into the search box and then press ENTER or click out of the search box. Click **Select** at the bottom of the **Available Definitions** page once you have found and selected the policy definition.

   ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-1/6e688227-3aac-4d63-bca5-d2b74e21d940.png)

1.  The **Assignment name** is automatically populated with the policy name you selected, but you can change it. For this example, leave *Require SQL Server version 12.0*. You can also add an optional **Description**. The description provides details about this policy assignment. **Assigned by** is automatically filled based on who is logged in. This field is optional, so custom values can be entered.

1.  Leave **Create a Managed Identity** unchecked. This box _must_ be checked when the policy or initiative being assigned includes a policy with the **`deployIfNotExists`** effect. As the policy used for this tutorial doesn't, leave it blank. 

1.  Click **Assign**.

##### Task 2: Implement a new custom policy


Now that you've assigned a built-in policy definition, you can do more with Azure Policy. Next, create a new custom policy to save costs by validating that VMs created in your environment can't be in the G series. This way, every time a user in your organization tries to create VM in the G series, the request is denied.


1.  Select **Definitions** under **Authoring** in the left side of the Azure Policy page.

  ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-1/d2d13d16-9b98-4b74-98b4-3cf1130349fb.png)

1.  Select **+ Policy definition** at the top of the page. This button opens to the **Policy definition** page.

1.  Enter the following information:

   - The management group or subscription in which the policy definition is saved. Select by using
     the ellipsis on **Definition location**.

**Note**: If you plan to apply this policy definition to multiple subscriptions, the location must be a management group that contains the subscriptions you assign the policy to. The same is true for an initiative definition.


   - The name of the policy definition - *Require VM SKUs smaller than the G series*
   - The description of what the policy definition is intended to do - *This policy definition
     enforces that all VMs created in this scope have SKUs smaller than the G series to reduce
     cost.*
   - Choose from existing options (such as _Compute_), or create a new category for this policy
     definition.
   - Copy the following JSON code and then update it for your needs with:
      - The policy parameters.
      - The policy rules/conditions, in this case - VM SKU size equal to G series
      - The policy effect, in this case - **Deny**.
</br>

   Here's what the JSON should look like. Paste your revised code into the Azure portal.

   ```json
   {
       "policyRule": {
           "if": {
               "allOf": [{
                       "field": "type",
                       "equals": "Microsoft.Compute/virtualMachines"
                   },
                   {
                       "field": "Microsoft.Compute/virtualMachines/sku.name",
                       "like": "Standard_G*"
                   }
               ]
           },
           "then": {
               "effect": "deny"
           }
       }
   }
   ```

   The *field* property in the policy rule must be one of the following values: Name, Type, Location, Tags, or an alias. An example of an alias might be **`"Microsoft.Compute/VirtualMachines/Size"`**

1.  Select **Save**.

##### Task 3: Create and assign an initiative definition


With an initiative definition, you can group several policy definitions to achieve one overarching goal. An initiative evaluates resources within scope of the assignment for compliance to the included policies. 


1.  Select **Definitions** under **Authoring** in the left side of the Azure Policy page.

   ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-1/bc61ad53-44b5-4a08-81ea-b3300ffab7c6.png)

1.  Select **+ Initiative Definition** at the top of the page to open the **Initiative definition**
   page.

   ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-1/5684c6be-b134-4498-ae65-a229f9c22a9f.png)

1.  Use the **Definition location** ellipsis to select a management group or subscription to store the definition. If the previous page was scoped to a single management group or subscription, **Definition location** is automatically populated.

1.  Enter the **Name** and **Description** of the initiative.

  This example validates that resources are in compliance with policy definitions about getting secure. Name the initiative **Get Secure** and set the description as: **This initiative has been created to handle all policy definitions associated with securing resources**.

1.  For **Category**, choose from existing options or create a new category.

1.  Browse through the list of **Available Definitions** (right half of **Initiative definition**
   page) and select the policy definition(s) you would like to add to this initiative. For the **Get
   secure** initiative, add the following built-in policy definitions by clicking the **+** next to
   the policy definition information or clicking a policy definition row and then the **+ Add**
   option in the details page:

   - Require SQL Server version 12.0
   - [Preview]: Monitor unprotected web applications in Security Center.
   - [Preview]: Monitor permissive network across in Security Center.
   - [Preview]: Monitor possible app Whitelisting in Security Center.
   - [Preview]: Monitor unencrypted VM Disks in Security Center.

   After selecting the policy definition from the list, it's added under **Policies and Parameters**.

   ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-1/adc27e08-0b42-4185-b96f-23f9ab4c28fa.png)

1.  If a policy definition being added to the initiative has parameters, they're shown under the
   policy name in the **Policies and Parameters** area. The _value_ can be set to either 'Set value'
   (hard coded for all assignments of this initiative) or 'Use Initiative Parameter' (set during
   each initiative assignment). If 'Set value' is selected, the drop-down to the right of _Values_
   allows entering or selecting the value(s). If 'Use Initiative Parameter' is selected, a new
   **Initiative parameters** section is displayed allowing you to define the parameter that is set
   during initiative assignment. The allowed values on this initiative parameter can further
   restrict what may be set during initiative assignment.

   ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-1/52a09a4b-c0cb-4b2b-bcca-9ef9798721ef.png)

**Note**: In the case of some `strongType` parameters, the list of values cannot be automatically determined. In these cases, an ellipsis appears to the right of the parameter row. Clicking it  opens the 'Parameter scope (&lt;parameter name&gt;)' page. On this page, select the subscription to use for providing the value options. This parameter scope is only used during creation of the initiative definition and has no impact on policy evaluation or the scope of the initiative when assigned.


1.  Click **Save**.

##### Task 4: Assign an initiative definition

1.  Select **Definitions** under **Authoring** in the left side of the Azure Policy page.

1.  Locate the **Get Secure** initiative definition you previously created and click it. Select **Assign** at the top of the page to open to the **Get Secure: Assign initiative** page.

   ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-1/10efa0a0-1203-42a0-9298-bb811a479a12.png)

   You can also right-click on the selected row or left-click on the ellipsis at the end of the row for a contextual menu. Then select **Assign**.

   ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-1/cd06276f-1a6b-46c8-be74-4244b4a720c0.png)

1.  Fill out the **Get Secure: Assign Initiative** page by entering the following example information. You can use your own information.

   - Scope: The management group or subscription you saved the initiative to becomes the default. You can change scope to assign the initiative to a subscription or resource group within the save location.
   - Exclusions: Configure any resources within the scope to prevent the initiative assignment from being applied to them.
   - Initiative definition and Assignment name: Get Secure (pre-populated as name of initiative being assigned).
   - Description: This initiative assignment is tailored to enforce this group of policy definitions.
   - Assigned by: Automatically filled based on who is logged in. This field is optional, so custom values can be entered.
</br>

1.  Leave **Create a Managed Identity** unchecked. This box _must_ be checked when the policy or initiative being assigned includes a policy with the **`deployIfNotExists`** effect. As the policy used for this tutorial doesn't, leave it blank. 

1.  Click **Assign**.

##### Task 5: Check initial compliance

1.  Select **Compliance** in the left side of the Azure Policy page.

1.  Locate the **Get Source** initiative. It's likely still in _Compliance state_ of **Not started**. Click on the initiative to get full details on the progress of the assignment.

   ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-1/3620a5d1-1156-4042-bdcc-dd70ae088295.png)

1.  Once the initiative assignment has been completed, the compliance page is updated with the  _Compliance state_ of **Compliant**.

   ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-1/e8d7f300-1045-4e5f-9519-800239293be2.png)

1.  Clicking on any policy on the initiative compliance page opens the compliance details page for
   the policy. This page provides details at the resource level for compliance.

##### Task 6: Exempt a non-compliant or denied resource using Exclusion


Following the example above, after assigning the policy definition to require SQL server version 12.0, a SQL server created with any version other 12.0 would get denied. In this task, you walk through resolving a denied request to create a SQL server by creating an exclusion on a single resource group. The exclusion prevents enforcement of the policy (or initiative) on that resource. In the following example, any SQL server version is allowed in a single resource group. An exclusion can apply to a subscription, resource group, or you can narrow the exclusion to individual resources.


A deployment prevented by an assigned policy or initiative can be viewed in two locations:

- On the resource group targeted by the deployment: Select **Deployments** in the left side of the page, then and click on the **Deployment Name** of the failed deployment. The resource that was denied is listed with a status of _Forbidden_. To determine the policy or initiative and assignment that denied the resource, click **Failed. Click here for details ->** on the Deployment Overview page. A window opens on the right side of the page with the error information. Under **Error Details** are the GUIDs of the related policy objects.

  ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-1/d2739f4d-8302-486f-8ded-df81eedf43a9.png)

- On the Azure Policy page: Select **Compliance** in the left side of the page and click on the  **Require SQL Server version 12.0** policy. On the page that opens, you would see an increase in the **Deny** count. Under the **Events** tab, you would also see who tried the deployment that was denied by the policy.

  ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-1/8df35a06-9467-4150-8d83-cae566684eae.png)

In this example, Trent Baker, one of Contoso's Sr. Virtualization specialists, was doing required work. We need to grant Trent an exception, but we don't want the non-version 12.0 SQL servers in just any resource group. We've created a new resource group, **SQLServers_Excluded** and will now grant it an exception to this policy assignment.

##### Task 7: Update assignment with exclusion

1.  Select **Assignments** under **Authoring** in the left side of the Azure Policy page.

1.  Browse through all policy assignments and open the *Require SQL Server version 12.0* assignment.

1.  Set the **Exclusion** by clicking the ellipsis and selecting the resource group to exclude,
   *SQLServers_Excluded* in this example.

   ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-1/bfefa47e-755d-433e-ad00-43f1b8e78256.png)

**Note**:  Depending on the policy and its effect, the exclusion could also be granted to specific resources within a resource group inside the scope of the assignment. As a **Deny** effect was used in this tutorial, it would not make sense to set the exclusion on a specific resource that already exists.


1.  Click **Select** and then click **Save**.


In this section, you resolved the denied request by creating an exclusion on a single resource group.


##### Task 8: Clean up resources


Now you're done working with resources from this lab, use the following steps to delete any of the assignments or definitions created above:


1.  Select **Definitions** (or **Assignments** if you're trying to delete an assignment) under **Authoring** in the left side of the Azure Policy page.

1.  Search for the new initiative or policy definition (or assignment) you want to remove.

1.  Right-click the row or select the ellipses at the end of the definition (or assignment), and select **Delete definition** (or **Delete assignment**).


In this lab, you successfully accomplished the following tasks:

> - Assigned a policy to enforce a condition for resources you create in the future
> - Created and assign an initiative definition to track compliance for multiple resources
> - Resolved a non-compliant or denied resource
> - Implemented a new policy across an organization



**Results**: You have now completed this lab.


**Congratulations**! You can now end the lab ready to coninue with your next module.



