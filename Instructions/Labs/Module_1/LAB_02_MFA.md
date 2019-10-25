


### Lab 2: Using Multi-Factor Authentication for Secure Access


In this module, you'll learn about securing the sign-in process through Multi-Factor Authentication (MFA). You'll learn how MFA works and the differences in implementation between on-premises and cloud scenarios. You'll also learn about using conditional access policies to provide more fine-grained control over apps and resources in your environment.

- Introducing Multi-Factor Authentication
- Implementing MFA


### Lab 2: Using Multi-Factor Authentication for Secure Access


#### Exercise 1: MFA Authentication Pilot (Require MFA for specific apps with Azure Active Directory conditional access)

##### Task 1:  Enable Azure AD Premium P2 trial and create a test user.

1.  In the Azure Portal, on the Hub menu click **Azure Active Directory**.

1.  Select **Licences**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-2/5871d4f5-5270-4fe6-af86-1de0b297736e.png)

1.  Select **All Products**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-2/1fc7d0ea-bde8-4b9b-b7c8-5e71b65c1e40.png)


1.  Click **Try / Buy**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-2/2366021e-0be7-4ad3-9984-fb7c5cb29cb7.png)

1.  Click **Azure AD Premium P2** **Free Trial**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-2/09a5459e-c9e4-410f-a64a-56e2921b2f0f.png)

1.  Click **Activate**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-2/de9f4a01-ab1c-488c-a2b6-bb0e7ada97c1.png)

1.  Return back to the Active Directory blade and note your tennant name.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-2/e2d04b65-e78b-4957-8dfa-9f171dda9c8c.png)

1.  Click **Users**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-2/37dac304-d5a4-48cd-ac56-cbd1c31edbfc.png)

1.  Click **+ New user**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-2/33efc078-a65b-4cd6-93a1-ff1d3d119940.png)

1.  Create a new user called **Isabella Simonsen** make a note of the passowrd.  The username will be `isabells@yourdomain.onmicroosft.com` (Where your domain is the teannant domain noted above).

1.  Open an In Private browsing session and Sign in to your Azure portal as Isabella Simonsenn and change the password when prompted (make a note of the new password you set).

2.  Sign out.


##### Task 2: Create your conditional access policy 


This section shows how to create the required conditional access policy. The scenario uses:

- The Azure portal as placeholder for a cloud app that requires MFA. 
- Your sample user to test the conditional access policy.  

In your policy, set:

|Setting |Value|
|---     | --- |
|Users and groups | Isabella Simonsen |
|Cloud apps | Microsoft Azure Management |
|Grant access | Require multi-factor authentication |

 
1.  Sign in to the Azure Portal..

2.  In the Azure portal, on the hub menu, click **Azure Active Directory**. 

3.  On the **Azure Active Directory** page, in the **Security** section, click **Conditional access**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-2/cb3b1a14-81b8-4039-b29b-c73235fe64eb.png)
 
4.  On the **Conditional Access** page, in the toolbar on the top, click **New Policy**.

**Note**: if this is greyed out, refresh the browser session.




5.  On the **New** page, in the **Name** textbox, type **Require MFA for Azure portal access**.



6.  In the **Assignment** section, click **Users and groups**.



7.  On the **Users and groups** page, perform the following steps:


    a. Click **Select users and groups**, and then select **Users and groups**.

    b. Click **Select**.

    c. On the **Select** page, select **Isabella Simonsen**, and then click **Select**.

    d. On the **Users and groups** page, click **Done**.

8.  Click **Cloud apps**.



9.  On the **Cloud apps** page, perform the following steps:



    a. Click **Select apps**.

    b. Click **Select**.

    c. On the **Select** page, select **Microsoft Azure Management**, and then click **Select**.

    d. On the **Cloud apps** page, click **Done**.


10.  In the **Access controls** section, click **Grant**.


11.  On the **Grant** page, perform the following steps:



    a. Select **Grant access**.

    a. Select **Require multi-factor authentication**.

    b. Click **Select**.

12.  In the **Enable policy** section, click **On**.

13.  Click **Create**.


##### Task 3: Evaluate a simulated sign-in


Now that you have configured your conditional access policy, you probably want to know whether it works as expected. As a first step, use the conditional access what if policy tool to simulate a sign-in of your test user. The simulation estimates the impact this sign-in has on your policies and generates a simulation report.  

To initialize the what if policy evaluation tool, set:

- **Isabella Simonsen** as user 
- **Microsoft Azure Management** as cloud app

 Clicking **What If** creates a simulation report that shows:

- **Require MFA for Azure portal access** under **Policies that will apply** 
- **Require multi-factor authentication** as **Grant Controls**.


1.  On the Conditional access - Policies page, in the menu on the top, click **What If**.  
 
 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-2/6d110614-efb6-4f35-97c0-c0b53424fb4b.png)

2.  Click **Users**, select **Isabella Simonsen**, and then click **Select**.



2.  To select a cloud app, perform the following steps:



    a. Click **Cloud apps**.

    b. On the **Cloud apps page**, click **Select apps**.

    c. Click **Select**.

    d. On the **Select** page, select **Microsoft Azure Management**, and then click **Select**.

    e. On the cloud apps page, click **Done**.

3.  Click **What If**.

4.  Note the result, Require MFA for Azure portal access.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-2/4938309b-e308-4f89-b6f6-1a04cb2fda8e.png)


##### Task 4: Test your conditional access policy

In the previous section, you have learned how to evaluate a simulated sign-in. In addition to a simulation, you should also test your conditional access policy to ensure that it works as expected. 

To test your policy, try to sign-in to your [Azure portal](https://portal.azure.com) using your **Isabella Simonsen** test account. You should see a dialog that requires you to set your account up for additional security verification.




#### Exercise 2: MFA Conditional Access (Complete an Azure Multi-Factor Authentication pilot roll out)


In this practice, you walk you through configuring a conditional access policy enabling Azure Multi-Factor Authentication (Azure MFA) when logging in to the Azure portal. The policy is deployed to and tested on a specific group of pilot users. Deployment of Azure MFA using conditional access provides significant flexibility for organizations and administrators compared to the traditional enforced method.

- Enable Azure Multi-Factor Authentication
- Test Azure Multi-Factor Authentication


##### Task 1: Enable Azure Multi-Factor Authentication

1.  Sign in to the Azure portal.

1.  On the Hub menu click **Active Directory**,

1.  Click **Groups** and click **+ New group**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-2/dc4c78ef-ef2c-4223-bde4-bb353d0d7e39.png)

1.  Enter the following information then click **Create**:

  * Group type; **Security**
  * Group Name: **MFA Pilot**
  * Group description: **MFA Pilot Group**
  * Membership type: **Assigned**
  * Members: Select **Isabella**
  </br>
  
  ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-2/c268bc7a-77a4-4a50-bce4-347ed494b643.png)
  
1.  Browse to **Azure Active Directory**, **Conditional access**

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-2/f851c18a-ebd9-44e2-827d-eb8879a7a7be.png)

1.  Select **New policy**

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-101T04/Module-2/32068891-d3e7-48e9-ae3c-072b59a50f7d.png)

1.  Name your policy **MFA Pilot**
1.  Under **users and groups**, select the **Select users and groups** check box
    * Select your pilot group **MFA Pilot**
    * Click **Done**
    </br>
1.  Under **Cloud apps**, select the **Select apps** radio button
    * The cloud app for the Azure portal is **Microsoft Azure Management**
    * Click **Select**
    * Click **Done**
    </br>
1.  Skip the **Conditions** section
1.  Under **Grant**, make sure the **Grant access** radio button is selected
    * Check the box for **Require multi-factor authentication**
    * Click **Select**
    </br>
1.  Skip the **Session** section
1.  Set the **Enable policy** toggle to **On**
1.  Click **Create**

##### Task 2: Test Azure Multi-Factor Authentication


To prove that your conditional access policy works, you test logging in to a resource that should not require MFA and then to the Azure portal that requires MFA.


1.  Open a new browser window in InPrivate or incognito mode and browse to **`https://account.activedirectory.windowsazure.com`**

   * Log in with the test user created as part of the prerequisites section of this article and note that it should not ask you to complete MFA.
   * Close the browser window.
   </br>
2.  Open a new browser window in InPrivate or incognito mode and browse to **`https://portal.azure.com`**

   * Log in with the test user created as part of the prerequisites section of this article and note that you should now be required to register for and use Azure Multi-Factor Authentication.
   * Close the browser window.
</br>


Prior to continuting you should remove all resources used for this lab.  To do this in the **Azure Portal** click **Resource groups**.  Select any resources groups you have created.  On the resource group blade click **Delete Resource group**, enter the Resource Group Name and click **Delete**.  Repeat the process for any additional Resource Groups you may have created.

**Failure to do this may cause issues with other labs.**




**Results** : You have now completed this lab.


