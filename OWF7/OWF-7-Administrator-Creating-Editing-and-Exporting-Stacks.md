## Creating Stacks
Stacks are a collection of dashboards assigned to multiple OWF users and groups. Administrators have the ability to **create**, **edit**, **delete** and **export** stacks. 

Creating, editing and deleting a stack is similar to creating, editing and deleting other features in OWF. Stacks are exported as descriptor files, for instructions see the **Exporting Stacks** section. There are several reasons why an administrator may want to share an exported stack. For example, an administrator at Branch A may create a Human Resources Stack. Since this stack is beneficial to everyone at the company, the administrators at other branches may want to use it. Export allows the administrator at Branch A to easily send the stack to administrators from other OWF instances.

From a user’s standpoint:

* Users can **customize**, **restore** and **delete** any stack assigned to them. Those changes will ONLY affect that user’s copy of the stack. Like group dashboards, users can return their stack to the current state of the stack by clicking the ![Restore](OWFImages/OWF7/Restore_icon.png) button (found by clicking Manage on the Switcher, then choosing a stack). 
* If a stack is deleted by an administrator, the user will no longer have a copy of the stack and the dashboards and widgets included in the stack.
* Users cannot delete individual stack dashboards.
* If an administrator changed the stack and the content of its dashboards after it was added to a user’s instance of OWF, the current state of the stack may be different than the one that originally appeared on the user’s Switcher. 

To create a stack:

1.	Click the ![Administration Button](OWFImages/OWF7/administration_button.png) button on the toolbar.
2.	Click on the Stacks button to open the Stacks Manager. Click Create to make a new stack.
3.	From here there are two ways to create stacks:

    A. <b>Import from descriptor URL</b> - Enter a stack descriptor URL and click Load. For more information about stack descriptor URLs see the **Stack Descriptor URL** section.

    B. <b>Manually enter data</b> - If a descriptor URL is not available, click the “Don’t have a stack descriptor?” link and complete the fields on the Properties tab. For more information about specific entry fields, see the Edit Button and Editor Widget Fields Table. 

4. 	Click Apply. This will unlock the Groups, Dashboards, Users and Widgets tabs. 

 > _Note: The Widgets tab in the Stacks Editor is for informational purposes only. It displays the widgets available in the stack based on the associated users, groups and dashboards._

5.	To add an existing dashboard, select the Dashboards tab in the Stacks Editor. Click the Add button. Select a dashboard, then click OK. This method also works for adding users and groups via the Users and Groups tabs in the Stacks Editor.
6.	Close the Stacks Editor. 

 > _Note: Adding an existing dashboard to a stack creates a copy of the dashboard that appears in the Switcher under the same name as the original dashboard. To avoid the confusion of having two dashboards in the Switcher with the same name, administrators are advised to rename stack dashboards._


###Stack Descriptor URL
Like widgets, stacks can be created via a descriptor URL. When stacks are created with a stack descriptor URL, OWF automatically retrieves the stack data from a descriptor file saved in a Web-accessible location. Descriptor URLs allow an administrator to quickly create stacks that have been prepopulated with dashboards and widgets. 

Stack descriptor URLs offer several benefits. They can bundle large amounts of stack data (ex. dashboard and widget JSON) into an HTML file. Descriptor URLs allow several installations of OWF to share the same stack information. 

###Editing Stacks
To edit existing stack content:

1.	Click the ![Administration Button](OWFImages/OWF7/administration_button.png) button on the toolbar, select Stacks to open the Stacks Manager. 
2.	From the manager, select a stack and click Edit. 
3.	Edit the stack data and click Apply. 

Users and groups assigned to the stack will receive the stack data changes when the stack is restored via the Switcher.

Administrators can edit the order dashboards appear in a stack. 
To reorder a stack dashboard:

1. Go to the Stack Editor and click the Dashboards tab.
2. Select a dashboard.  
3. Click the up or down arrow to change the dashboard’s position. 

Users assigned to the stack will see the changes in their Switcher when they log in to OWF or, if they are already signed in, when they Restore the stack.

![Reorder Stack Dashboard](OWFImages/OWF7/reorder_stack_dashboard.png)

**Figure: Reorder Stack Dashboard**

####Updating and Editing Stack Descriptor Data
Administrators who create a stack via a descriptor URL can update and edit the imported stack descriptor data within the OWF interface. Updating the stack descriptor data will retrieve the latest data stored in the stack’s descriptor file. Any changes made to the stack prior to the update are lost.

To retrieve the latest stack descriptor data:

1.	Click the ![Administration Button](OWFImages/OWF7/administration_button.png) button on the toolbar, select Stacks to open the Stack Manager. 
2.	From the manager, select a stack and click Edit. 
3.	Click Load. The Widget Editor will automatically refresh and display the most recent widget descriptor data. 
4.	Click Apply. 

Administrator can edit their copy of the stack by following the steps outlined in the **Editing Stacks** section.

###Exporting Stacks
Administrators have the ability to export and save stack data as a descriptor file. An administrator or developer must host the descriptor file in a Web-accessible location to share the file with other administrators. Sharing a stack descriptor URL allows administrators on different OWF systems to have a copy of the same stack.

To export a stack:

1.	Click the ![Administration Button](OWFImages/OWF7/administration_button.png) button on the toolbar.
2.	Click the Stacks button to open the Stacks Manager.
3.	Click the arrow on the right of the split Edit button and choose Export.
4.	Enter a File Name, then click OK.
5.	Move the stack descriptor HTML file to a Web-accessible location, like a shared wikis or company Intranet sites. 
6.	Share the descriptor file URL with other OWF administrators.

> _Note: Administrators are advised not to edit the stack descriptor file once exported from OWF. Modifying a stack’s descriptor file may introduce code errors that are difficult to identify and will prevent the user from creating the stack._
