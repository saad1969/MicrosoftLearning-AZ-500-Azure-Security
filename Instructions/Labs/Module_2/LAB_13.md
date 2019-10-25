### Module 2 - Implement Platform Protection 

#### Lab 13 -  Secure Admin Access 


SSH is an encrypted connection protocol that allows secure sign-ins over unsecured connections. SSH is the default connection protocol for Linux VMs hosted in Azure. Although SSH itself provides an encrypted connection, using passwords with SSH connections still leaves the VM vulnerable to brute-force attacks or guessing of passwords. A more secure and preferred method of connecting to a VM using SSH is by using a public-private key pair, also known as SSH keys.

- The public key is placed on your Linux VM, or any other service that you wish to use with public-key cryptography.

- The private key on you local system is used by an SSH client to verify your identity when you connect to your Linux VM. Protect this private key. Do not share it.

- Depending on your organization's security policies, you can reuse a single public-private key pair to access multiple Azure VMs and services. You do not need a separate pair of keys for each VM or service you wish to access.

Your public key can be shared with anyone, but only you (or your local security infrastructure) should possess your private key.


##### Task 1: Create SSH keys with PuTTYgen

1.  Open a browser and navigate to the following URL:

 ```cli
http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html 
 ```

1.  Download and install the **Putty Installer**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-2/c4b6d531-fe4d-4772-b1ee-ee090ba10fd6.png)

1.  Click **Start** and navigate to **PuTTYgen**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-2/59ecec37-45bf-4152-86e1-dbd70b95bf6f.png)

1.  Click Generate. By default PuTTYgen generates a 2048-bit SSH-2 RSA key.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-2/e4f4dc22-cc25-4a26-8cbc-3f96b455a705.png)

1.  Move the mouse around in the blank area to provide randomness for the key.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-2/3b9baef9-b0fb-4145-8f2f-a08db0fb2e6c.png)

1.  After the public key is generated, optionally enter and confirm a passphrase. You will be prompted for the passphrase when you authenticate to the VM with your private SSH key. Enter **Pa55w.rd1234** as the passphrase.
warning
Without a passphrase, if someone obtains your private key, they can log in to any VM or service that uses that key. We recommend you create a passphrase. However, if you forget the passphrase, there is no way to recover it.


1.  The public key is displayed at the top of the window. You can copy this entire public key and then paste it into the Azure portal or an Azure Resource Manager template when you create a Linux VM. Save the public key to a new folder on the root of the **C:** drive called **CERT** of LON-CL1, name the file **public**:

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-2/70aaec3a-d9c1-47a3-b050-5e9896479c20.png)

2.  Save the private key to the same location but with the filename **private**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-2/03c50964-1107-4f2e-83c6-d2838d98f3e3.png)
 
1.  Highlight and copy the public key from the top window.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-2/b9895b82-1c18-415a-8377-6f7ec5ed1284.png)

##### Task 2: Create a Linux virtual machine in the Azure portal

1.  Navigate back to the **Azure Portal**.

1.  Choose **Create a resource** in the upper left corner of the Azure portal.

1.  In the search box above the list of Azure Marketplace resources, search for and select **Ubuntu Server 18.04 LTS** by Canonical, then choose **Create**.

1.  In the **Basics** tab, under **Project details**, make sure the correct subscription is selected and then choose the **Resource group** *myResourceGroup*. 

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-2/261de7a5-cb6d-4fb7-9511-385e5fc57a3c.png)

1.  Under **Instance details**, type *myVM-Linux* for the **Virtual machine name** and choose *East US* for your **Region**. Leave the other defaults.
 
 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-2/ccbd79d4-835b-4c86-ac89-aa000f82a05d.png)

1.  Under **Administrator account**, select **SSH public key**, type the user name **localadmin**, then paste your public key into the text box. Remove any leading or trailing white space in your public key.

   ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-2/71882e46-be70-4f60-8c51-6c460d5bdbf5.png)

1.  Under **Inbound port rules** > **Public inbound ports**, choose **Allow selected ports** and then select **SSH (22)** and **HTTP (80)** from the drop-down. 

	![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-2/8127bfae-daa6-41c7-8328-dd4c7c5ce785.png)

1.  Click the **Management** tab and select **Off** for all options.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-2/43940bc4-82f7-450b-a82d-ecf419f22104.png)

1.  Leave the remaining defaults and then select the **Review + create** button at the bottom of the page.

1.  On the **Create a virtual machine** page, you can see the details about the VM you are about to create. When you are ready, select **Create**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-2/77787c14-ff95-4d1d-ae62-af89080a7598.png)
warning
It will take a few minutes for your VM to be deployed. When the deployment is finished, move on to the next section. 



##### Task 3: Connect to your VM


One way to make an SSH connection to your Linux VM from Windows is to use an SSH client. This is the preferred method if you have an SSH client installed on your Windows system, or if you use the SSH tools in Bash in Azure Cloud Shell. If you prefer a GUI-based tool, you can connect with PuTTY.  In this task you will use PuTTY.


1.  In the **Azure Portal Hub Menu** click **Virtual Machines** then select your **myVM-Linux** machine.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-2/b77587f2-1616-4b2e-8148-1d92a1d6c59c.png)

1.  In the Overview blade, note down or copy the **Public IP Address** of your virtual machine.
warning
**Note:** Your public IP will be different to what is shown in the screenshot.


 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-2/72033a56-5b3b-4ea9-8bac-efcde5be8380.png)

1.  on **LON-CL1** start **PuTTy** by clicking the start menu and searching for PuTTY.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-2/a5c89add-64dc-4135-a4d9-c66475881bb4.png)

2.  Type in or paste in your Public IP Address of your Linuix Azure Linux VM:

    ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-2/759d0e69-edb5-443c-af81-886490cd8e00.png)

3.  Select the **Connection** > **SSH** > **Auth** category. Browse to and select your PuTTY private key (.ppk file):

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-2/01235096-60e0-463b-8728-71329e9aab7f.png)   

4.  Click **Open** to connect to your VM.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-2/21163eaf-11f7-486d-8c8c-d3710f837323.png)

5.  Click **Yes** to continue on the pop up.

1.  On the `login as` screen enter **localadmin** and press **Enter**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-2/8666a384-c176-43bd-a00a-91ceae77e9bc.png)
 
1.  You are now logged into the Linux VM hosted in Azure.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T01/Module-2/ec7fa23d-eb58-49e2-b9d6-c962bba1dac2.png)


**Results**: You have now completed this Lab.



You can now continue with your next lab by clicking the drop down menu at the top of the lab guide.
