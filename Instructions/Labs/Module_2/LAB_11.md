
### Module 2: Lab 11: On-Prem to Azure Connections - VPN Gateways and Tunnelling

##### Task 1: Deploy a Virtual Appliance.


In this task you will create a Sophos XG Virtual Appliance which will emulate an on-premises device.  The layout of this is depicted in the digaram below


 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-4/8763cb44-ad54-4cbc-b9ae-69bbd7ec13c1.png)

1.  Open PowerShell and run the following command.

 ```powershell
start https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FGoDeploy%2FAZ300%2Fmaster%2Fxg-azure-master%2FmainTemplate.json
 ```
 
1.  Login to the portal if required.

1.  On the Custom deployment enter or select the following details:

 | Setting | Value |
 |---|---|
 | Resource Group | _Create New_ **OnPremRG** |
 | Location | **Southeast Asia** |
 | Admin Password | **Pa55w.rd1234** |
 | Public IP DNS | _Enter a unique name_ |
 | Storage Name | _Enter a unique name_ |
 
1.  Scroll to the bottom of the blade and click the check box next to  I agree to the terms and conditions..... and click **Purchase**. 
 
##### Task 2: Create a Resource Group and VNet.


In this task you will create a Virtual Machine and a Virtual Network inside a new Resource group which will be use to connect to your emulated On-Prem environment.


1.  Login to your Azure Portal **`https://portal.azure.com`**

1.  Click **Create a resource** > **Networking** > **Virtual Network**

1.  Change the values in the **Create virtual network** blade change the values tobe the same as the output below:

  - **Name** S2S_RG-vnet
  - **Address space** 172.17.0.0/16
  - **Resource group** Create New: S2S_RG
  - **Location**: East US
  - **Subnet address range** 172.17.0.0/24
</br> 

1.  Click **Create**.

warning
**Note:**  You can continue to the next task without having to wait for the deployment to complete.



##### Task 2: Create a Gateway Subnet and a Virtual network Gateway.


In this tak you will Create a Gateway Subnet and a Virtual network Gateway which will enable you to create a connection between On-Prem and your Azure VNet.



1.  In the Azure Portal click **Resource Groups** on the Hub Menu.
 
1.  Click the **S2S_RG** resource group that has been created for you.

1.  In the S2S_RG Resource Group blade click the **S2S_RG-vnet**.

1.  On the  **S2S_RG-vnet** menu click **Subnets**.

1.  Click **+ Gateway subnet**.  
warning
**Note:** You need to create a Gateway subnet in order for the Gateway machines to reside in.  All the routing is done by the Azure Software Defined Networking.


1.  Leave the default options on the **Add subnet** blade and click **OK**.

1.  Click **+ Create a resource**.

1.  Search for Virtual Network Gateway and select **Virtual network gateway**.

1.  Click **Create**.

1.  On the **Create virtual network gateway** blade enter the following information:

  - **Name**: S2S-GW
  - **Name**: (US) East US
  - **Gateway type**: VPN
  - **VPN Type**: Route-based
  - **SKU**: Basic
  - **Virtual network**: Select the S2S_RG-vnet (this was created earlier when you deployed the VM)
  - **Public IP address**: (Create New) Name: S2S-GW-PIP
</br>

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-4/f9bd3419-03d2-45af-8687-bec0e91e350e.png)

1.  Click **Review + create** then on the summary screen click **Create**
warning
**Note:**  The gateway may take upto 45 minutes to deploy, although. in most cases it is much quicker.  Monitor this by clicking on the Bell Icon. You can continue to the next task whilst the Gateway is deploying.


##### Task 3: Configure the Sophos virtual appliance.

1.  On the Azure Portal Hub menu click **Resource Groups**.

1.  Select the **OnPremRG** Resource Group.

1.  Select the **PublicIP** Resource.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-4/64fc9ff7-fe7b-470f-8878-75cf47998eb9.png)

1.  Make a note of the assigned Public IP address.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-4/04b472c8-0dda-49ca-bfec-c17e7dccbe83.png)

1.  Open a new browser session and navigate to https://x.x.x.x:4444 (where x.x.x.x is the public IP address you noted above).

1.  Depending on your browser there may be different options to proceed with the connection.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-4/feb25db5-f673-4770-a0cd-9ba708348153.png)

1.  Log into the Firewall with the following credentials:

 - Admin
 - Pa55w.rd1234
 
1.  Accept the licence agreement.

1.  On the Register your firewall page click **I don't have a a serial number (start a trial)** and select **I do not want to register now** then click **Continue**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-4/64ed9492-b974-4ae1-9fb8-235aed04dd2e.png)

1.  On the Warning pop up click **Continue**.

1.  Return back to the Azure Portal.  Open the **S2S_RG** Resource Group and select the **S2S-GW-PIP** Public IP and make a note of it.
warning
**Note**: This is your Public IP you will connect your Sophos virtual applicabce to via IPSec VPN.


 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-4/e509a5ce-25ce-449f-b1ae-0b920d311106.png)
 
1.  Return back to the Sophos Portal.

1.  Go to **VPN > IPsec Connections**, select **Add **and configure the following settings:

 **General Settings Section:**

  - **Name**: On_Prem_to_Azure

  - **IP Version**: IPv4.

  - **Activate on Save:** Selected.
  
  - **Create firewall rule:** Selected.

  - **Description**: Site to Site connection from On Prem to Azure VNet.

  - **Connection Type**: Site-to-Site.

  - **Gateway Type**: Respond Only.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-4/78d2bfc4-fe0b-4d17-bcea-b34f39ae2456.png)

 **Encryption Section**:

  - **Policy**: Microsoft Azure.

  - **Authentication Type**: Preshared Key.

  - **Preshared Key**: 123456789

  - **Repeat Preshared Key**: 123456789

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-4/21cd1353-039c-460c-bea1-01a592e26013.png)

 **Gateway Settings Section**:

  - **Listening Interface**: Leave the default.

  - **Gateway Address**: Input the public IP of the Azure VPN gateway noted earlier.

  - **Local ID**: IP Address.

  - **Remote ID**: IP Address.

  - **Local ID**: Enter the public IP of the on-premises Sophos XG Firewall.

  - **Remote ID**: Input the public IP of the Azure VPN gateway that you noted earlier.

  - **Local Subne**t: Enter the local subnet of 10.0.0.0 /16 (255.255.0.0)
</br>
  ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-4/67ff0b5c-295c-4700-a093-173314ecda63.png)

  - **Remote Subnet**: Enter the remote subnet 172.17.0.0 /16 (255.255.0.0)
</br>
    ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-4/2daffd7a-e994-450a-b204-79a2b087dbba.png)

1.  **Advanced**: leave the default settings.

1.  Upon clicking **Save**, the IPsec connection is activated.

**Note**: Do not click on the button under the **Connection** column as it will override the configuration settings set on the IPsec connection (**Gateway type: Respond only**). This is to avoid issues since Azure must initiate the tunnel.




##### Task 4: Creating Azure connection.


In this task you will create a connection on your Azure Gateway to the On-Prem firewall and establish the connection.


1.  Click on **Resource Groups** on the **Hub Menu**.

2.  Select the **S2S_RG** Resource Group. 
 
1.  Select your **S2S-GW** Gateway. 

1.  Click **Connections** from the S2S-GW menu.

1.  Click **Add**.

1.  Enter the following information in the **Add connection** blade.

  - **Name:** GWConnection
  - **Connection type:** Site-to-site (IPSec)
  - **Virtual Network Gateway:** S2S-GW
</br>
1.  Click the **Local network gateway**

1.  Click **Create new**.

1.  Enter the following information in the **Create local network gateway** blade:

  - **Name:** OnPremGW
  - **IP address:** _Enter your IP address of your Sophos on prem firewall you recorded earlier_
  - **Address space:** 10.0.0.0/16  _(Note:  This is the IP range of your On-Prem servers)_
</br> 
 
1.  Click **OK**.

2.  In the **Shared key (PSK)** box enter `123456789` then click **OK**.
warning
**Note:**  This key is just for this lab.  In the real world you would use something with greater complexity.


1.  Refresh the page and the connection should be established.
warning
**Note:**  It may take 30 seconds to establish the connection.

 
 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-4/7e42342c-3f07-4fcc-a4a8-31f229cf8084.png)



Prior to continuting you should remove all resources used for this lab.  To do this in the **Azure Portal** click **Resource groups**.  Select any resources groups you have created.  On the resource group blade click **Delete Resource group**, enter the Resource Group Name and click **Delete**.  Repeat the process for any additional Resource Groups you may have created.

**Failure to do this may cause issues with other labs.**
  


**Results**: You have now completed this lab.
