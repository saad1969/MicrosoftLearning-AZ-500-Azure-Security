### Lab 9: Azure DNS


**Scenario**

In this module, you will learn about DNS basics and specifically implementing Azure DNS. In the DNS Basics lesson you will review DNS domains, zones, record types, and resolution methods. In the Azure DNS lesson, we will cover delegation, metrics, alerts, and DNS hosting schemes. 

**Objectives**

Lessons include:

 * Azure DNS Basics
 * Implementing Azure DNS



#### Exercise 1: DNS Zones

##### Task 1: Create a DNS zone

1.  Sign in to the Azure portal
2.  On the Hub menu, navigate to **Create a resource > Networking > DNS zone** to open the **Create DNS zone** blade.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-100T04-/Module-2/1449e5a5-0c42-462d-85ce-5250befe7fd7.png)
 
4.  On the **Create DNS zone** blade enter the following values, then click **Create**:

   | **Setting** | **Value** | **Details** |
   |---|---|---|
   |**Name**|**_see details**_|The name of the DNS zone (yours must be unique) |
   |**Subscription**|_**Your subscription**_|Select a subscription to create the DNS zone in.|
   |**Resource group**|Create new: **_myResourceGroup_**|Create a resource group. The resource group name must be unique within the subscription you selected. 
   |**Location**|East US||

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-100T04-/Module-2/c809a31a-69e8-4b8a-9e34-af3283102c2b.png)

##### Task 2: List DNS zones

1.  In the Azure portal, navigate to **All services** > **Networking** > **DNS zones**.
warning
**Note:** Each DNS zone is its own resource, and information such as number of record-sets and name servers are viewable from this view. 


 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-100T04-/Module-2/e0597a7f-6ce3-4600-920a-7b049c86ed3c.png)

2.  The column **NAME SERVERS** is not in the default view. To add it, click **Edit Columns**, select **Name servers**, and then click **Apply**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-100T04-/Module-2/7ffe3313-97a7-48a1-bbf3-c5749e9876e1.png)
 
 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-100T04-/Module-2/ccf3d94b-13c9-400e-a78a-9ebb63c23e97.png)


#### Exercise 2: Manage DNS records and record sets by using the Azure portal


This exercise shows you how to manage record sets and records for your DNS zone by using the Azure portal.


##### Task 1: Add a new record to a record set

1.  Click All service and then DNS zones

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-100T04-/Module-2/e0597a7f-6ce3-4600-920a-7b049c86ed3c.png)

2.  Select the DNS zone you created in the last practice

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-100T04-/Module-2/98da9891-a8c9-4833-8627-33c851e884a4.png)
 
3.  Click **+ Record Set**.
 
 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-100T04-/Module-2/891de6f8-a94f-4cf3-a5f6-84a913c98a03.png)

4.  Enter **testrecord** for the name and **1.2.3.4** as the IP address and click **OK**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-100T04-/Module-2/0b05a02b-a44a-4215-ab67-0878dfcfc076.png)

##### Task 2: Update a record

1.  In the Overview blade for your DNS zone, select the testrecord you created.

  ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-100T04-/Module-2/91ea9c87-65de-4af0-9d74-cfc38d220602.png)
 
2.  Under IP Address add the test address of **4.3.2.1** and click **Save**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-100T04-/Module-2/751506b7-b98d-4df9-9a5b-017174723fc1.png)
 
##### Task 3: Remove a record from a record set


You can use the Azure portal to remove records from a record set. Note that removing the last record from a record set does not delete the record set.


1.  In the Overview pane for your DNS zone, select the testrecord you created.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-100T04-/Module-2/81f16418-ae72-44da-aa92-f904ac54ea33.png)

2.  Select **Delete** and click **Yes** when prompted.

  ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-100T04-/Module-2/a107ddce-81a9-4616-905d-a06e2178fc09.png)
 

**Work with NS and SOA records**

NS and SOA records that are automatically created are managed differently from other record types.

**Modify SOA records**

You cannot add or remove records from the automatically created SOA record set at the zone apex (name = "\@"). However, you can modify any of the parameters within the SOA record (except "Host") and the record set TTL.

**Modify NS records at the zone apex**

The NS record set at the zone apex is automatically created with each DNS zone. It contains the names of the Azure DNS name servers assigned to the zone.

You can add additional name servers to this NS record set, to support co-hosting domains with more than one DNS provider. You can also modify the TTL and metadata for this record set. However, you cannot remove or modify the pre-populated Azure DNS name servers.

Note that this applies only to the NS record set at the zone apex. Other NS record sets in your zone (as used to delegate child zones) can be modified without constraint.

**Delete SOA or NS record sets**

You cannot delete the SOA and NS record sets at the zone apex (name = "\@") that are created automatically when the zone is created. They are deleted automatically when you delete the zone.


You are then prompted to confirm you are wanting to delete the DNS zone. Deleting a DNS zone also deletes all records that are contained in the zone.



Prior to continuting you should remove all resources used for this lab so far.  To do this in the **Azure Portal** click **Resource groups**.  Select any resources groups you have created.  On the resource group blade click **Delete Resource group**, enter the Resource Group Name and click **Delete**.  Repeat the process for any additional Resource Groups you may have created.

**Failure to do this may cause issues with the remainder of the labs.**





**Results**: You have now completed this lab, to continue on to other labs in this module use the drop down menu at the top of the lab instructions. If this is the final lab in the module you can now safely delete the resource group created in these labs to save cost on your Azure pass subscription.
