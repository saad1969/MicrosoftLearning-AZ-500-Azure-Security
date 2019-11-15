# Module 3: Lab 1 - Security Playbook in Azure Security Center


Security playbook is a collection of procedures that can be executed from Security Center once a certain playbook is triggered from selected alert. Security playbook can help to automate and orchestrate your response to a specific security alert detected by Security Center. Security Playbooks in Security Center are based on Azure Logic Apps, which means you can use the templates that are provided under the security category in Logic Apps templates, you can modify them based on your needs, or you can create new playbooks using Azure Logic Apps workflow, and using Security Center as your trigger.


### Task 1: How to create a security playbook from Security Center?


Follow these steps to create a new security playbook from Security Center:


1.  Open **Security Center** dashboard.

If you find that security center options are greyed out, click the getting started pane and click **Start Trial**


2.  Under **Automation & Orchestration** section in the left pane, click **Playbooks (Preview)**.

       ![Screenshot](../Media/Module-3/2323824c-6d1e-49e2-8049-ab853a302af7.png)

	

3.  In the **Security Center - Playbooks (Preview)** page, click **Add Playbook** button.

     ![Screenshot](../Media/Module-3/76956e55-61a4-4e89-a938-03b57325b5b2.png)

 

4.  In the **Create Logic app** page, type a unique name to create your new logic app, and click **Create** button. **Create a new Resource Group with a unique name** Once it finishes creating, the new playbook will appear in the list. If it doesn't appear, click **Refresh** button. Once you see it, click on it to start editing this playbook.

      ![Screenshot](../Media/Module-3/b9f20273-106c-41f3-8d3e-799f3c637954.png)
    
5.  The **Logic App Designer** appears. Click **Blank Logic App** to create a new playbook. You can also select **Security** under the categories and use one of the templates.

    ![Screenshot](../Media/Module-3/3b7e96eb-1e6f-405a-b7ac-152bcbf9da88.png)

6.  In the **Search all connectors and triggers** field, type *Azure Security Center*, and select **When a response to an Azure Security Center alert is triggered**.

    ![Screenshot](../Media/Module-3/9f827605-40d1-483e-9669-dadb68008dbf.png)

7.  Now you can define what happens when you trigger the playbook. You can add an action, logical condition, switch case conditions or loops. Click **new step** to browse the list of actions that can take place on a security alert. Custom actions and code can also be trigged on an alert.

8.  Click save to save the playbook with or without a trigger action

### Task 2: How to run a security playbook in Security Center?


You can run a security playbook in Security Center when you would like to orchestrate, obtain more information from other services, or when you would like to remediate. To access the playbooks follow these steps:


1.  Open **Security Center** dashboard.

2.  In the left pane, under **Threat Protection** click **Security alerts**.

    ![Screenshot](../Media/Module-3/1c9a473b-0090-4a9c-9c30-eda15623fe37.png)

3.  Click the alert that you want to investigate.


**Note**: You may not have any security alerts in your lab environment, if this is the case you can refer to the screenshots to preview what alerts will look like


4.  In the top of the alert's page click **Run playbooks** button.

    ![Screenshot](../Media/Module-3/47a7f035-517e-4773-bbeb-48e09bb4f618.png)
    
5.  In the Playbooks page, select the playbook that you want to run, and click **Run** button. If you wish to see the playbook before triggering, you can click on it, and the designer will open.

    ![Screenshot](../Media/Module-3/7d97e181-042d-4091-9d59-e32fe9ea5bdf.png)

### Task 3: History


After running the playbook, you can also access previous executions, and steps that contains more information about the status of previously executed playbooks. The history is contextualized per alert, which means that the playbook history that you see in this page is correlated to the alert that triggered this playbook.

   ![Screenshot](../Media/Module-3/7cd8ebd7-8eb9-432e-85de-6b3e1c23a402.png)

1.  To see more details about the execution of a particular playbook, click on the playbook itself, and the Logic App run page appears with the entire workflow.

     ![Screenshot](../Media/Module-3/9c88adfc-7634-4b4d-bf86-570415b2789d.png)

2.  In this workflow you can see the time that each task took it to be executed, and you can expand each task to see the result.


**Note**: For more information on how to create your own playbook using Azure Logic App, read [Create your first logic app workflow to automate processes between cloud apps and cloud services](https://docs.microsoft.com/azure/logic-apps/logic-apps-create-a-logic-app).




**Results**: In this lab, you learned how to use playbooks in Azure Security Center.

