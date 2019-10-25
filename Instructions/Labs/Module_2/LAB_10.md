


### Module 2: Lab 10 - Load Balancer


**Note**: Throughout this lab ensure you select **East US** as the Region/Location for all resources.



**Scenario**

In this module, you will learn about three ways to distribute network traffic: Azure Load Balancer, Azure Traffic Manager, and Azure Application Gateway. The Azure Load Balancer delivers high availability and network performance to your applications. The Azure Traffic Manager allows you to control the distribution of user traffic to your service endpoints. The Azure Application Gateway is a web traffic load balancer that enables you to manage traffic to your web applications. 

**Lessons include:**

- Azure Load Balancer
- Azure Traffic Manager 
- Azure Application Gateway


#### Excerise 1: Distributing Network Traffic using a Standard Load Balancer


In this section, you create a public load balancer that helps load balance virtual machines. Standard Load Balancer only supports a Standard Public IP address. When you create a Standard Load Balancer, and you must also create a new Standard Public IP address that is configured as the frontend (named as *LoadBalancerFrontend* by default) for the Standard Load Balancer. 


##### Task 1: Create a public load balancer

1.  On the top left-hand side of the screen, click **Create a resource** > **Networking** > **Load Balancer**.  

2.  In the **Create load balancer** page, enter or select the following information, accept the defaults for the remaining settings, and then select **Review + create**:

    | Setting                 | Value                                              |
    | ---                     | ---                                                |
    | Subscription               | Select your subscription.    |
    |Resource group | Select **Create new**, and then type myResourceGroupLB    |
    | Name                   | *myLoadBalancer*                                   |
    | Region           | Select **East US**.                          |
    | Type          | Public                                        |
    | SKU           | Standard                          |
    | Public IP address | Select **Create new** and type *myPublicIP* in the name box.  |
    | Availability zone               | **Zone-redundant**    |
    
  ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500/Module-2/3fa605c9-2858-462c-ba83-9cf603cc6458.png)

1.  On the Validation screen click **Create**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500/Module-2/457d881a-00a6-42f3-9ca1-f7ccb29d5a93.png)


##### Task 2: Create a virtual network

1.  On the top left-hand side of the screen click **+ Create a resource** > **Networking** > **Virtual network** and enter these values for the virtual network:
    - **myVnet** - for the name of the virtual network.
    - **10.0.0.0/16** - for the Address space
    - **myResourceGroupLB** - for the name of the existing resource group
    - **myBackendSubnet** - for the subnet name.
    - **10.0.0.0/24** - for the Subnet Address range
    </br>

2.  Click **Create** to create the virtual network.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T02/Module-3/1d322f71-c554-4926-a7ac-66ec6e710fd8.png)

##### Task 3: Create virtual machines

1.  On the top left-hand side of the screen, click **Create a resource** > **Compute** > **Windows Server 2019 Datacenter** and enter these values for the virtual machine:
          
    - **myResourceGroupLB** - for **Resource group**, select *myResourceGroupLB* from the drop down menu.
    - **myVM1** - for the name of the virtual machine.  
    - **localadmin** - for the **Username**
    - **Pa55w.rd1234** - for the **Password**
    - **HTTP (80) & RDP (3389)** - for the inbound port rules.
</br>

1.  Click the Networking Tab and under Public IP click **Create new**.  Name the IP Address **myPIP1** and click the **Standard SKU** then click **OK**.
warning
**Note**: If you do not select the Standard SKU here you will have problems later in the lab.


 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500/Module-2/f1180ec9-d718-42cd-a0f2-4fe177dc69b2.png)

2.  Select the **Management** Tab and ensure all radio buttons are **Off**.

1.  Click **Review + create** then click **Create**.

7.  Repeat the steps above to create a second VM, called ***myVM2*** using _**myPIP2**_ for the new Public IP address. 
 
##### Task 4: Install IIS

1.  Click **All resources** in the left-hand menu, and then from the resources list click **myVM1** that is located in the *myResourceGroupLB* resource group.

2.  On the **Overview** page, click **Connect** to RDP into the VM.
3.  Log into the VM with username *localadmin*.
4.  Open PowerShell and run the following command to install IIS.

 ```powershell
Install-WindowsFeature Web-Server
 ```

7.  Repeat steps 1 to 4 for the virtual machine *myVM2*.

##### Task 5: Create load balancer resources


In this section, you  configure load balancer settings for a backend address pool and a health probe, and specify a load balancer rule.



##### Task 5: Create a backend address pool


To distribute traffic to the VMs, a backend address pool contains the IP addresses of the virtual (NICs) connected to the load balancer. Create the backend address pool *myBackendPool* to inlcude *VM1* and *VM2*.


1.  Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.

2.  Under **Settings**, click **Backend pools**, then click **Add**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T02/Module-3/63bd32a1-dda5-4e5f-b5a5-1ddc614f836d.png)

3.  On the **Add a backend pool** page, do the following:
   - For name, type *myBackendPool*, as the name for your backend pool.
   - For **Virtual network**, select *myVNet*.
   - Add *myVM1* and *my VM2* under **Virtual Machine** along with their corresponding IP addresses, and then select **Add**.
    - Click **OK**.
</br>
3.  Check to make sure your load balancer backend pool setting displays both the VMs **VM1** and **VM2**.

##### Task 6: Create a health probe

warning
To allow the load balancer to monitor the status of your app, you use a health probe. The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks. Create a health probe *myHealthProbe* to monitor the health of the VMs.


1.  Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.
2.  Under **Settings**, click **Health probes**, then click **Add**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T02/Module-3/bb6018e1-d06e-4302-9312-cb5d143c0509.png)

3.  Use these values to create the health probe:
    - *myHealthProbe* - for the name of the health probe.
    - **HTTP** - for the protocol type.
    - *80* - for the port number.
    - */* - for the URI path. 
    - *15* - for number of **Interval** in seconds between probe attempts.
    - *2* - for number of **Unhealthy threshold** or consecutive probe failures that must occur before a VM is considered unhealthy.
</br>
 
 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T02/Module-3/ac59e555-10b4-4b39-8baa-833ca8423cf2.png)


4.  Click **OK**.


##### Task 7: Create a load balancer rule


A load balancer rule is used to define how traffic is distributed to the VMs. You define the frontend IP configuration for the incoming traffic and the backend IP pool to receive the traffic, along with the required source and destination port. Create a load balancer rule *myLoadBalancerRuleWeb* for listening to port 80 in the frontend *FrontendLoadBalancer* and sending load-balanced network traffic to the backend address pool *myBackEndPool* also using port 80. 


1.  Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.
2.  Under **Settings**, click **Load balancing rules**, then click **Add**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T02/Module-3/3aeb3cdb-321e-43bc-b60d-c647e324464b.png)


3.  Use these values to configure the load balancing rule:
    - *myHTTPRule* - for the name of the load balancing rule.
    - **TCP** - for the protocol type.
    - *80* - for the port number.
    - *80* - for the backend port.
    - *myBackendPool* - for the name of the backend pool.
    - *myHealthProbe* - for the name of the health probe.
    </br>
    
  ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T02/Module-3/be74d319-24db-41f6-8269-bf2bc166da02.png)  
    
4.  Click **OK**.
    
##### Task 8: Test the load balancer

1.  Find the public IP address for the Load Balancer on the **Overview** screen.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T02/Module-3/812c63ec-274d-44c8-8971-85d06d73cfb9.png)
  
2.  Copy the public IP address, and then paste it into the address bar of your browser. The default page of IIS Web server is displayed on the browser.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T02/Module-3/1b9f9311-3c0a-4948-be50-2753793daafc.png)

1.  Notice the IIS default page loads.

1.  In the Azure Portal click on **Virtual Machines** in the hub menu.  Select myVM1 and in the **Overview** blade click **Stop** and confirm **Yes**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T02/Module-3/2b2d4ebb-cb1c-4268-bc7e-d35016939646.png)
 
1.  Wait until the myVM1 Virtual Machine has stopped then go back to the browser tab with the load lanancer public IP and click refresh to confirm myVM2 is continuing to service the requests and the load balancer is functioning as expected.

### Load Balancer ARM Deployments

##### Task 1: Deploy an ARM template 


This template allows you to create 2 Virtual Machines under a Load balancer and configure a load balancing rule on Port 80. This template also deploys a Storage Account, Virtual Network, Public IP address, Availability Set and Network Interfaces. In this template, we use the resource loops capability to create the network interfaces and virtual machines


1.  In a new tab in your browser, navigate to the following URL https://aka.gd/2E2MAjh

1.  Click **Deploy to Azure**

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T02/Module-3/11cd7771-c51a-4b7c-a136-0f4e6b8144df.png)

1.  On the tmplate blade that opens, enter the following details:

  - Resource group:  myResourceGroupLB
  - Admin Username:  localadmin
  - Admin Password:  Pa55w.rd1234
</br>
1.  Click **I agree....** and click **Purchase**.



##### Task 1: Create an application gateway


A virtual network is needed for communication between the resources that you create. Two subnets are created in this example: one for the application gateway, and the other for the backend servers. You can create a virtual network at the same time that you create the application gateway.


1.  First you need to create a subnet for the Application Gateway to reside in.  Click **Virtual networks** on hub menu and select **myVNet**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T02/Module-3/8f5071b8-44fe-4784-80be-d0e18b4124d5.png)
 
1.  Click **Subnets** and click **+ Subnet**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T02/Module-3/7a9dc542-366f-4ff5-ad55-b02ef6d10408.png)
 
1.  Enter **myAppGWSubnet** as the name and click **OK**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T02/Module-3/049edc61-7b59-4b99-aa93-73059c1cace1.png)

1.  Click **Create a resource** found on the upper left-hand corner of the Azure portal.

2.  Click **Networking** and then click **Application Gateway** in the Featured list.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T02/Module-3/da98c1b3-7426-4572-b420-7145a8ddd567.png)

1.  Enter these values for the application gateway:

    - *myAppGateway* - for the name of the application gateway.
    - *myResourceGroupLB* - select the already existing Resource Group.
</br>
    
    ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T02/Module-3/dc3c7f4e-3124-4e96-8ad5-644eff987fa4.png)

2.  Accept the default values for the other settings and then click **OK**.

1.  Click **Choose a virtual network**, click **myVNet**

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T02/Module-3/04c2ba6d-470d-4085-a25d-c9c7d67a74e0.png)

7.  Under **Frontend IP configuration** ensure **IP address type** is set to **public**, and under **Public IP address**, ensure **Create new** is selected. Type ***myAGPublicIPAddress*** for the public IP address name. Accept the default values for the other settings and then click **OK**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T02/Module-3/e7492c26-60b3-4155-8345-e4e532bc02ed.png)

1.  Review the settings on the summary page, and then click **OK** to create the virtual network, the public IP address, and the application gateway. It may take several minutes for the application gateway to be created. Wait until the deployment finishes successfully before moving on to the next section.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T02/Module-3/900b2379-9695-43bb-97e3-9d6eb443380d.png)

##### Task 2: Add backend servers


In this example, you will use the two virtual machines that you created in the first practice for the application gateway. 


1.  Click **All resources**, and then click **myAppGateway**.
4.  Click **Backend pools**. A default pool was automatically created with the application gateway. Click **appGatewayBackendPool**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T02/Module-3/d3e5a49f-896e-49e7-b03b-6f19026e5d14.png)

5.  Under **Targets**, click **IP address or FQDN** select **Virtual machine**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T02/Module-3/45841473-b3b2-4c24-a98e-5bcd413d1be6.png)

6.  Under **Virtual Machine**, add myVM1 and myVM2 virtual machines and their associated network interfaces.

    ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T02/Module-3/d54fce32-621a-470b-afe0-be37e69fcbf0.png)

6.  Click **Save**.

##### Task 3: Test the application gateway

1.  Find the public IP address for the application gateway on the Overview screen. Click **All resources** and then click **myAGPublicIPAddress**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T02/Module-3/a9298154-ab45-4f49-a0ff-5f70e2a42cbf.png)
 
2.  Copy the public IP address, and then paste it into the address bar of your browser.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-300T02/Module-3/3ca8fb6e-abe9-4953-8dcd-7376b07810d1.png)


Prior to continuting you should remove all resources used for this lab.  To do this in the **Azure Portal** click **Resource groups**.  Select any resources groups you have created.  On the resource group blade click **Delete Resource group**, enter the Resource Group Name and click **Delete**.  Repeat the process for any additional Resource Groups you may have created.

**Failure to do this may cause issues with the next Practice.**
    


**Results**: You have now completed this lab.



You can now end the lab ready to coninue with your next lab.


