
### Module 1: Manage Identity and Access 

### Lab 8: Subscriptions


**Scenario**

Occasionally, a need arises for transferring a subscription from an owner to an Azure AD tenant. In order to transfer a subscription from a Azure AD owner to another subscription you need access to another subscription. If you do not have access to multiple subscriptions,
at this time just review the process outlined below.


#### Exercise 1: Transfer Azure subscriptions between Azure AD tenants

##### Task 1: To transfer the ownership of an Azure subscription

1.  Sign in at the Azure Account Center as the account admin.

2.  Select the subscription to transfer.

3.  Verify that your subscription is eligible for self-serve transfer by checking the Offer and Offer ID against the supported offers list.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-1/a22b9ef9-e1e0-42ee-ba01-e7806d6baaec.png)
 
4.  Select **Transfer subscription**.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-1/9609e809-9eb4-4909-a44d-b23d0756e553.png)

5.  Specify the recipient.

**Note**: If you transfer a subscription to a new Azure AD tenant, all role assignments in RBAC61 will be permanently deleted from the source tenant and not migrated to the target tenant.


 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-1/27a1d1a4-0779-4403-86e5-203dabdeddb9.png)

6.  The recipient automatically gets an email with an acceptance link.
7.  The recipient selects the link and follows the instructions, including entering their payment information

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-1/fd57efa4-b461-4946-bbf7-286f043cb767.png)

8.  Azure completes the subscription transfer.

 At this point, billing ownership of the Azure subscription, would be transfer to the new subscription.


**Results**: You have now completed this module.


**Congratulations**! You can now end the lab ready to coninue with your next module.

