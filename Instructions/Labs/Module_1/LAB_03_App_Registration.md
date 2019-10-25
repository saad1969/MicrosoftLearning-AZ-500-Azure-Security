### Module 1: Manage Identity and Access 


**Scenario**

Enterprise developers and software-as-a-service (SaaS) providers can develop commercial cloud services or line-of-business applications that can be integrated with Microsoft identity platform to provide secure sign-in and authorization for their services.

This quickstart shows you how to add and register an application using the App registrations experience in the Azure portal so that your app can be integrated with the Microsoft identity platform.



**Note:** To save time and simplify the course the Azure PowerShell Module and Azure CLI have already been installed in the Virtual Machine for you.


#### Exercise 1: Application Registration

##### Task 1: Register a new application using the Azure portal

1.  Sign in to the Azure portal.
1.  If your account gives you access to more than one tenant, select your account in the top right corner, and set your portal session to the Azure AD tenant that you want.
1.  In the left-hand navigation pane, select the **Azure Active Directory** service, and then select **App registrations > New registration**.
1.  When the **Register an application** page appears, enter your application's registration information:

   - **Name** - Enter: **Contoso App**
   - **Supported account types** - Select **Accounts in this organizational directory only** (Read the options below).

       | Supported account types | Description |
       |-------------------------|-------------|
       | **Accounts in this organizational directory only** | Select this option if you're building a line-of-business (LOB) application. This option is not available if you're not registering the application in a directory.<br><br>This option maps to Azure AD only single-tenant.<br><br>This is the default option unless you're registering the app outside of a directory. In cases where the app is registered outside of a directory, the default is Azure AD multi-tenant and personal Microsoft accounts. |
       | **Accounts in any organizational directory** | Select this option if you would like to target all business and educational customers.<br><br>This option maps to an Azure AD only multi-tenant.<br><br>If you registered the app as Azure AD only single-tenant, you can update it to be Azure AD multi-tenant and back to single-tenant through the **Authentication** blade. |
       | **Accounts in any organizational directory and personal Microsoft accounts** | Select this option to target the widest set of customers.<br><br>This option maps to Azure AD multi-tenant and personal Microsoft accounts.<br><br>If you registered the app as Azure AD multi-tenant and personal Microsoft accounts, you cannot change this in the UI. Instead, you must use the application manifest editor to change the supported account types. |

   - **Redirect URI (optional)** - Select **Web**, and then enter **`https://app.contoso.com`**
       - For web applications, provide the base URL of your app. For example, `http://localhost:31544` might be the URL for a web app running on your local machine. Users would use this URL to sign in to a web client application.
       - For public client applications, provide the URI used by Azure AD to return token responses. Enter a value specific to your application, such as `myapp://auth`.

1.  When finished, select **Register**.

    ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-1/2c603053-a6db-495f-a89f-2ae536c43692.png)

1.  Azure AD assigns a unique application (client) ID to your app, and you're taken to your application's **Overview** page. To add additional capabilities to your application, you can select other configuration options including branding, certificates and secrets, API permissions, and more.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-1/6b6751c6-1635-4f60-b56a-9776092d32aa.png)
 

**Results**: You have now completed this module.


**Congratulations**! You can now end the lab ready to coninue with your next module.
