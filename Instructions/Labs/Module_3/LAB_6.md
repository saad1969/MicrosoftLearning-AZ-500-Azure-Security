

### Module 3: Lab 1 - Security Playbook in Azure Security Center


Security playbook is a collection of procedures that can be executed from Security Center once a certain playbook is triggered from selected alert. Security playbook can help to automate and orchestrate your response to a specific security alert detected by Security Center. Security Playbooks in Security Center are based on Azure Logic Apps, which means you can use the templates that are provided under the security category in Logic Apps templates, you can modify them based on your needs, or you can create new playbooks using Azure Logic Apps workflow, and using Security Center as your trigger.


##### Task 1: How to create a security playbook from Security Center?


Follow these steps to create a new security playbook from Security Center:


1.  Open **Security Center** dashboard.
warning
If you find that security center options are greyed out, click the getting started pane and click **Start Trial**


2.  Under **Automation & Orchestration** section in the left pane, click **Playbooks (Preview)**.

	![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500/Module-3/ceca248f-1100-445f-bed1-04c8fab24889.png)

3.  In the **Security Center - Playbooks (Preview)** page, click **Add Playbook** button.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500/Module-3/33d77576-05da-4399-9fad-d53f7c3fafe3.png)

4.  In the **Create Logic app** page, type a unique name to create your new logic app, and click **Create** button. **Create a new Resource Group with a unique name** Once it finishes creating, the new playbook will appear in the list. If it doesn't appear, click **Refresh** button. Once you see it, click on it to start editing this playbook.

	![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500/Module-3/bc28f5b0-deb4-482c-bf2c-ce8213a428b6.png)
    
5.  The **Logic App Designer** appears. Click **Blank Logic App** to create a new playbook. You can also select **Security** under the categories and use one of the templates.

	![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500/Module-3/55b53f11-0cb2-43eb-8e99-3bf8695543e2.png)

6.  In the **Search all connectors and triggers** field, type *Azure Security Center*, and select **When a response to an Azure Security Center alert is triggered**.

	![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500/Module-3/686790bd-1c78-4a29-8d28-75ba9dbd5e88.png)

7.  Now you can define what happens when you trigger the playbook. You can add an action, logical condition, switch case conditions or loops. Click **new step** to browse the list of actions that can take place on a security alert. Custom actions and code can also be trigged on an alert.

8.  Click save to save the playbook with or without a trigger action

##### Task 2: How to run a security playbook in Security Center?


You can run a security playbook in Security Center when you would like to orchestrate, obtain more information from other services, or when you would like to remediate. To access the playbooks follow these steps:


1.  Open **Security Center** dashboard.

2.  In the left pane, under **Threat Protection** click **Security alerts**.

	![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500/Module-3/36b46a0a-21e3-4f69-98fa-f830e1f4d53e.png)

3.  Click the alert that you want to investigate.

warning
**Note**: You may not have any security alerts in your lab environment, if this is the case you can refer to the screenshots to preview what alerts will look like


4.  In the top of the alert's page click **Run playbooks** button.

	![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500/Module-3/fc6105be-51dd-44d0-9cfa-f4f3b344459c.png)
    
5.  In the Playbooks page, select the playbook that you want to run, and click **Run** button. If you wish to see the playbook before triggering, you can click on it, and the designer will open.

	![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500/Module-3/179239a1-5b44-4f77-841e-6c19b4d8e432.png)

##### Task 3: History


After running the playbook, you can also access previous executions, and steps that contains more information about the status of previously executed playbooks. The history is contextualized per alert, which means that the playbook history that you see in this page is correlated to the alert that triggered this playbook.


  ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500/Module-3/e3eb8350-7641-424f-b924-e387d7e497ba.png)

1.  To see more details about the execution of a particular playbook, click on the playbook itself, and the Logic App run page appears with the entire workflow.

 ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500/Module-3/45147154-5767-4f7b-9174-e0ec58e11d35.png)

2.  In this workflow you can see the time that each task took it to be executed, and you can expand each task to see the result.

warning
**Note**: For more information on how to create your own playbook using Azure Logic App, read [Create your first logic app workflow to automate processes between cloud apps and cloud services](https://docs.microsoft.com/azure/logic-apps/logic-apps-create-a-logic-app).




**Results**: In this lab, you learned how to use playbooks in Azure Security Center.


**Congratulations**: You have now completed this lab.
