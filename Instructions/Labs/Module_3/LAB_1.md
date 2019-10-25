

### Module 3: Lab 1 - Azure Monitor


Azure Monitor maximizes the availability and performance of your applications and services by delivering a comprehensive solution for collecting, analyzing, and acting on telemetry from your cloud and on-premises environments. It helps you understand how your applications are performing and proactively identifies issues affecting them and the resources they depend on.

In this lab you will configure Azure Monitor to:

- Collect data from an Azure virtual machine.
- Use Application Insights to monitor your website.



 
#### Exercise 1: Collect data from an Azure virtual machine with Azure Monitor


Azure Monitor can collect data directly from your Azure virtual machines into a Log Analytics workspace for detailed analysis and correlation. Installing the Log Analytics VM extension for Windows and Linux allows Azure Monitor to collect data from your Azure VMs. This exercise shows you how to configure and collect data from your Azure Linux or Windows VMs using the VM extension with a few easy steps.  


##### Task 1: Deploy an Azure VM to monitor.

1.  Open the Azure Cloud Shell and run the following two commands to create a Resource Group and Azure VM that you will use to monitor:

 ```powershell
New-AzResourceGroup -Name myResourceGroup -Location EastUS
 ```

 ```powershell
New-AzVm -ResourceGroupName "myResourceGroup" -Name "myVM" -Location "East US" -VirtualNetworkName "myVnet" -SubnetName "mySubnet" -SecurityGroupName "myNetworkSecurityGroup" -PublicIpAddressName "myPublicIpAddress" -OpenPorts 80,3389
 ```

1.  When prompted for credentials enter **LocalAdmin** as the User and use the password **Pa55w.rd1234**

##### Task 2: Create a workspace

1.  In the Azure portal, select **All services**. In the list of resources, type **Log Analytics**. As you begin typing, the list filters based on your input. Select **Log Analytics workspaces**.

    ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-3/f6033b13-e9b6-4540-a966-d78cb78abc2a.png)

2.  Select **Create**, and then select choices for the following items:

   * Provide a name for the new **Log Analytics workspace**, such as *myWorkspaceDemo*.  
   * Select a **Subscription** to link to by selecting from the drop-down list if the default selected is not appropriate.
   * For **Resource Group**, select **myResourceGroup** which is the Resource Group that contains the VM you created in Task 1.
   * Select the **EastUS** as the location. 
   * Leave the pricing Tier as **Per Gb (2018)**
  
        ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-3/0c9a364f-4950-4178-bf6e-eeb696c60477.png)

3.  After providing the required information on the **Log Analytics workspace** pane, select **OK**.  

1.  While the information is verified and the workspace is created, you can track its progress under **Notifications** from the menu. 

##### Task 2: Enable the Log Analytics VM Extension


For Windows and Linux virtual machines already deployed in Azure, you install the Log Analytics agent with the Log Analytics VM Extension. Using the extension simplifies the installation process and automatically configures the agent to send data to the Log Analytics workspace that you specify. The agent is also upgraded automatically when a newer version is released, ensuring that you have the latest features and fixes. Before proceeding, verify the VM is running otherwise the process will fail to complete successfully. 
 

1.  In the Azure portal, select **All services** found in the upper left-hand corner. In the list of resources, type **Log Analytics**. As you begin typing, the list filters based on your input. Select **Log Analytics workspaces**.

2.  In your list of Log Analytics workspaces, select **myWorkspaceDemo** created earlier.
warning
**Note**: The name of your workspace may be differnent to **myWorkspaceDemo**.


3.  On the left-hand menu, under Workspace Data Sources, select **Virtual machines**.  

4.  In the list of **Virtual machines**, select a virtual machine you want to install the agent on. Notice that the **Log Analytics connection status** for the VM indicates that it is **Not connected**.

5.  In the details for your virtual machine, select **Connect**. The agent is automatically installed and configured for your Log Analytics workspace. This process takes a few minutes, during which time the **Status** shows **Connecting**.

6.  After you install and connect the agent, the **Log Analytics connection status** will be updated with **This workspace**.

##### Task 3: Collect event and performance of a Windows VM.


Azure Monitor can collect events from the Windows event logs or Linux Syslog and performance counters that you specify for longer term analysis and reporting, and take action when a particular condition is detected. Follow these steps to configure collection of events from the Windows system log and Linux Syslog, and several common performance counters to start with.  


1.  On the Log Analytics workspaces blade, select **Advanced settings**.

    ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-3/c55891c0-6631-4b63-9b39-b67b611ccdcf.png)

2.  Select **Data**, and then select **Windows Event Logs**.

3.  You add an event log by typing in the name of the log.  Type **System** and then select the plus sign **+**.

4.  In the table, check the severities **Error** and **Warning**.

5.  Select **Save** at the top of the page to save the configuration.

6.  Select **Windows Performance Data** to enable collection of performance counters on a Windows computer.

7.  When you first configure Windows Performance counters for a new Log Analytics workspace, you are given the option to quickly create several common counters. They are listed with a checkbox next to each.

    ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-3/7d7955a2-6c43-4586-8b43-858187f0ddb4.png)

    Select **Add the selected performance counters**.  They are added and preset with a ten second collection sample interval.
  
8.  Select **Save** at the top of the page to save the configuration.


##### Task 4: View data collected


Now that you have enabled data collection, lets run a simple log search example to see some data from the target VMs.  


1.  In the selected workspace, from the left-hand pane, select **Logs**.

2.  On the Logs query page, type `Perf` in the query editor and select **Run**.

    ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-3/9bd00154-931d-44de-9dd7-1054a1a984e6.png)

    For example, the query in the following image returned 10,000 performance records. Your results will be significantly less due to the VM having only being ran for a few minutes.

    ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-3/bd6b6f4a-4557-40b5-bc97-78ed3d39d997.png)

#### Exercise 2: Monitor Websites with Azure Monitor Application Insights


With Azure Monitor Application Insights, you can easily monitor your website for availability, performance, and usage. You can also quickly identify and diagnose errors in your application without waiting for a user to report them. Application Insights provides both server-side monitoring as well as client/browser-side monitoring capabilities.

This exercise guides you through adding the open source Application Insights JavaScript SDK which allows you to understand the client/browser-side experience for visitors to your website.


##### Task 1: Enable Application Insights


Application Insights can gather telemetry data from any internet-connected application, running on-premises or in the cloud. Use the following steps to start viewing this data.


1.  Select **Create a resource** > **Management tools** > **Application Insights**.

   A configuration box appears; use the following table to fill out the input fields.

    | Settings        | Value   | 
   | ------------- |-----|
   | **Name**      | Enter a Globally Unique Value |
   | **Resource Group**     | mySResourceGroup |
   | **Location** | East US |

2.  Click **Create**.

##### Task 2: Create an HTML file

1.  On your local computer, create a file called ``hello_world.html``. For this example the file will be placed on the root of the C: drive at ``C:\hello_world.html``.
2.  Copy the script below into ``hello_world.html``:

    ```html
    <!DOCTYPE html>
    <html>
    <head>
    <title>Azure Monitor Application Insights</title>
    </head>
    <body>
    <h1>Azure Monitor Application Insights Hello World!</h1>
    <p>You can use the Application Insights JavaScript SDK to perform client/browser-side monitoring of your website. To learn about more advanced JavaScript SDK configurations visit the <a href="https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md" title="API Reference">API reference</a>.</p>
    </body>
    </html>
    ```

##### Task 3: Configure App Insights SDK

1.  Select **Overview** > **Essentials** > Copy your application's **Instrumentation Key**.

   ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-3/a0fede27-c532-47a8-bf95-3bb8d0e7c1ac.png)

2.  Add the following script to your ``hello_world.html`` before the closing ``</head>`` tag:

   ```javascript
    <script type="text/javascript">
      var sdkInstance="appInsightsSDK";window[sdkInstance]="appInsights";var aiName=window[sdkInstance],aisdk=window[aiName]||function(e){function n(e){t[e]=function(){var n=arguments;t.queue.push(function(){t[e].apply(t,n)})}}var t={config:e};t.initialize=!0;var i=document,a=window;setTimeout(function(){var n=i.createElement("script");n.src=e.url||"https://az416426.vo.msecnd.net/scripts/b/ai.2.min.js",i.getElementsByTagName("script")[0].parentNode.appendChild(n)});try{t.cookie=i.cookie}catch(e){}t.queue=[],t.version=2;for(var r=["Event","PageView","Exception","Trace","DependencyData","Metric","PageViewPerformance"];r.length;)n("track"+r.pop());n("startTrackPage"),n("stopTrackPage");var s="Track"+r[0];if(n("start"+s),n("stop"+s),n("setAuthenticatedUserContext"),n("clearAuthenticatedUserContext"),n("flush"),!(!0===e.disableExceptionTracking||e.extensionConfig&&e.extensionConfig.ApplicationInsightsAnalytics&&!0===e.extensionConfig.ApplicationInsightsAnalytics.disableExceptionTracking)){n("_"+(r="onerror"));var o=a[r];a[r]=function(e,n,i,a,s){var c=o&&o(e,n,i,a,s);return!0!==c&&t["_"+r]({message:e,url:n,lineNumber:i,columnNumber:a,error:s}),c},e.autoExceptionInstrumented=!0}return t}(
      {
         instrumentationKey:"INSTRUMENTATION_KEY"
      }
      );window[aiName]=aisdk,aisdk.queue&&0===aisdk.queue.length&&aisdk.trackPageView({});
   </script>
   ```

3.  Edit ``hello_world.html`` and add your instrumentation key.

4.  Open ``hello_world.html`` in a local browser session. This will create a single pageview. You can refresh your browser to generate multiple test page views.

##### Task 4: Start monitoring in the Azure portal

1.  You can now reopen the Application Insights **Overview** page in the Azure portal, where you retrieved your instrumentation key, to view details about your currently running application. The four default charts on the overview page are scoped to server-side application data. Since we are instrumenting the client/browser-side interactions with the JavaScript SDK this particular view doesn't apply unless we also have a server-side SDK installed.

2.  Click on ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-3/0efb57d4-1a8e-4c2c-a51c-30518de777f5.png) Application Map icon  **Analytics**.  This opens **Analytics**, which provides a rich query language for analyzing all data collected by Application Insights. To view data related to the client-side browser requests run the  following query:

    ```json
    // average pageView duration by name
    let timeGrain=1s;
    let dataset=pageViews
    // additional filters can be applied here
    | where timestamp > ago(15m)
    | where client_Type == "Browser" ;
    // calculate average pageView duration for all pageViews
    dataset
    | summarize avg(duration) by bin(timestamp, timeGrain)
    | extend pageView='Overall'
    // render result in a chart
    | render timechart
    ```

   ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-3/34852766-5fa9-4bf8-9767-1c5232d6d41e.png)

3.  Go back to the **Overview** page. Click on **Browser** from under the **Investigate** header, then select **Performance**  Here you find metrics related to the performance of your website. There is also a corresponding view for analyzing failures and exceptions in your website. You can click **Samples** to drill into individual transaction details. From here, you can access the end-to-end transaction details.

   ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-3/ac4b1422-f812-468a-a161-839e70ed7498.png)

4.  To begin exploring the user behavior analytics tools, from the main Application Insights menu select **Users** under the **Usage** header. Since we are testing from a single machine, we will only see data for one user. For a live website, the distribution of users might look as follows:

     ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-3/66d53c66-ea0a-4c01-a2ab-c26369e8c9e2.png)

5.  If we had instrumented a more complex website with multiple pages, another useful tool is [**User Flows**](../../azure-monitor/app/usage-flows.md). With **User Flows** you can track the pathway visitors takes through the various parts of your website.

   ![Screenshot](https://godeployblob.blob.core.windows.net//labguideimages/AZ-500---VML---v2-Sept-2019/Module-3/1aa4e690-ae3c-4ff5-b3b1-7cca80a5a7b1.png)

1.  Leave all resources.  You will use these in a future lab.


**Results**: In this lab, you learned how to monitor resources with Azure Monitor.


**Congratulations**: You have now completed this lab.
