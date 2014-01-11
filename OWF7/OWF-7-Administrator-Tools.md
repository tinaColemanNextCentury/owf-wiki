# Administrator Tool
Administration tools, located by clicking the Administration button on the toolbar, allow an administrator to manage widgets, groups, stacks, users and group dashboards. If Administrators use the Marketplace Approvals Widget, it will appear here by default. 


![Administration Window](OWFImages/OWF7/admin_window.png)

**Figure: Administrator Tools**

#1 Administrative Managers
The administration managers are used to create, edit and delete users, groups, widgets and group dashboards as well as approve listings imported from Marketplaces. While each manager has specific fields that relate to the manager’s specific purpose, some of the functions operate identically in each manager. For example, the search feature in the User Manager functions exactly like the search feature in the Widget Manager. Accordingly, search is explained only once in this section. 

Also, this document no longer contains definitions regarding basic information that general users should understand. If a topic can be easily defined by Google, it has been removed from this guide. The following section offers a general overview of the administrative managers and their use. 

The manager information is broken into sub-sections: 

* Panel 
* Management buttons
* Search bar and pagination toolbar

##Manager Panel

![Users Manager Panel](OWFImages/OWF7/user_manager_panel.png)

**Figure: Users Manager Panel**

The dashboard, widget, group, stack and user managers open to similar panel views. The panel view described in this section applies to all five managers. 

The Panel View:

* Allows the user to create, edit, delete or view an entry.

* Displays the number of users/groups/widgets/dashboards/stacks associated with the specific entry. 

> _Note: When viewing the widget count, only the widgets that a user requests or receives from an administrator appear in the overall count. Widgets associated through groups will NOT appear in the widget count._

* Offers a view of the first fifty results in alphabetical order. Additional results can be viewed using the pagination as described in **Manager Widgets—Pagination** section found on this page. To reduce the number of displayed results, use the search bar, described in the **Manager Widgets—Search** section.
 
From the panel, an administrator can:

* **Sort** - Most of the columns in the panel can be sorted in ascending or descending order by clicking on the triangle to the right of the column header and selecting a sorting option. 
* **Hide/Show columns** - Columns can be hidden or shown by hovering over a column header, clicking the triangle that will appear, hovering over the columns menu option, and un-checking the columns to be hidden.
* **Reorder columns** - Columns can be reordered by clicking (and holding) a column header down and then dragging it to the desired position.
* **Multiple selection** - Entries can be selected for bulk operations by holding down the CTRL button while clicking multiple entries. The delete, edit, activate and deactivate buttons will perform bulk operations on all selected entries.
* **View the information panel** - To display more information about the entry, single-click the row to open the information panel on the right. 

###Management Buttons: Create/Delete

Administrators use the manager widgets to create and delete users, widgets, groups, group dashboards and stacks. Differences between the five managers are referenced in sub-bullets.
 
* ![Create Button](OWFImages/OWF7/create_button.png) - Launches the editor widget. From the editor, an administrator can create a new user/widget/group/group dashboard/stack (depending on which editor the administrator launches) and assign related data to the new entry. 

    * When creating a new entry, only the Properties tab will be active until the administrator saves the user/widget/group/group dashboard/stack via the Apply button.

* ![Delete Button](OWFImages/OWF7/delete_button.png) - Deletes selected entries. Some user/widget/group/group dashboard/stack rules apply:
    * Deleting a <b>group</b> does not delete the users or widgets assigned to the group. It only deletes the pairing of users with widgets in the group. 
    * Deleting a <b>widget</b> removes it from a user’s Launch Menu and the groups to which it was assigned. 
    * Deleting a <b>group dashboard</b> removes it from the group. Individual users can continue to use their copy of the dashboard. However, the user’s individual copy will no longer have the option to restore to the group dashboard as described on the [Creating Group Dashboards](OWF-7-Administrator-Creating-Group-Dashboards) page. 
    * Deleting a <b>stack</b> removes it from the users and groups. Dashboards and widgets that are associated with the stack will also be deleted. 

###Management Buttons: Edit
* ![Edit Button](OWFImages/OWF7/edit_button.png) - Clicking Edit on any administrative manager will launch the respective user/widget/group/group dashboard/stack editor, allowing an administrator to edit the entry. 

> _Note: If an administrator launches the editor widgets in a fit dashboard, the editor widgets will “float” on top of the dashboard. Additional dashboard layout information is found in the [User’s Guide](User%27s-Guide-Home)._  

![Tabs on the User Editor](OWFImages/OWF7/widgets_tab_on_user_editor_450px.png)

**Figure: Widgets Tab on the User Editor**

From the editor widget, administrators can create, edit and delete data assigned to users/widgets/groups/group dashboards/stacks. The following table alphabetically lists editable fields found in the editor widgets. Split Edit button features, located in the manager widgets, are also listed. The last column of the table describes the location of each field. 

<br><b>Table: Edit Button and Editor Widget Fields Table</b>

<table>
  <tr>
   <th>Field</th>
   <th>Purpose</th>
   <th>Location</th>
  </tr>
  <tr>
    <td>Activate/Deactivate</td>
    <td>Users in active groups have full access to their group-assigned widgets. Users in a deactivated group will not have access to any of the widgets which are assigned to them via the deactivated group. When a group becomes deactivated it will appear gray. <br> *Note: If a user is in Group A and Group B and each group has Widget 1 assigned to it, the user will still have access to Widget 1 if Group A is deactivated and Group B is activated. Additionally, if the user has widget access outside of a group’s distribution, the user will not lose access to the widget, even if they lose group access.*</td>
   <td>Group Manager (under the split Edit button); “Active” checkbox in the Group Editor, Properties Tab</td>
  </tr>
  <tr>
   <td>Background</td>
   <td>Some widgets do not have user interfaces. These widgets are often used to cache or log data. If a widget is set to run in the background, it will not appear in the dashboard foreground. However, it will appear in the Widget Switcher (Alt + Shift + Q). Also, it will appear on the user’s Launch Menu if the “visible” menu flag (described in this table) is turned on.</td>
   <td>Widget Editor, Properties Tab</td>
  </tr>
  <tr>
   <td>Container Icon URL</td>
   <td>Defines the location of the icon which appears in widget chrome at 24x24 pixels.</td>
   <td>Widget Editor, Properties Tab</td>
  </tr>
  <tr>
   <td>Copy To Group</td>
   <td>Allows an administrator to copy dashboards to selected groups via the add groups window. Once a dashboard is added to a group, every member of that group will receive their own copy of that dashboard.</td>
   <td>User Editor, Dashboards Tab, split Edit button</td>
  </tr>
  <tr>
   <td>Default Tags</td>
   <td>Specifies the default tags (comma separated, if needed) that facilitate widget categorization. Default tags cannot be deleted by the user; however, users can add additional tags to widgets in their instance of OWF. Default Tags are superseded by grouped widgets, which are explained on the [Grouping Widgets](OWF-7-Administrator-Grouping-Widgets) page.</td>
   <td>Widget Editor, Properties Tab</td>
  </tr>
  <tr>
   <td>Definition</td>
   <td>A required field in a dashboard that contains the JSON configuration of a dashboard.</td>
   <td>Dashboard Editor, Properties Tab</td>
  </tr>
  <tr>
   <td>Export</td>
   <td>Administrators can export stacks to other users as a descriptor URL. Additional information about stack descriptor URLs is available in the Developer’s Guide.</td>
   <td>Stack Editor, split Edit button</td>
  </tr>
  <tr>
   <td>Display Name</td>
   <td>The group name which will appear in grids and tables throughout administrator views.</td>
   <td>Group Editor, Properties Tab</td>
  </tr>
   <td>GUID</td>
   <td>A unique 32-character alpha-numeric code for a particular named widget. If “Widget A” is launched 5 times, all 5 widgets will share the same `widgetGuid` property.</td>
   <td>All Editor Widgets, Properties Tab</td>
  </tr>
  <tr>
   <td>Height</td>
   <td>Defines the launch height of the widget in pixels. Up and down arrows to the right of the field can be used to modify the overall height.</td>
   <td>Widget Editor, Properties Tab</td>
  </tr>
  <tr>
   <td>Intents</td>
   <td>Widget intents build on OWF’s publish/subscribe functionality by allowing users to choose the widget that will use its data. Intents explain the intention for the widget. This binding capability enables two widgets to enhance each other’s functionality. <br> *Note: Only developers can modify intents via the widget’s descriptor file; instructions are available in the OWF Developer’s Guide.*</td>
   <td>Widget Editor, Intents Tab</td>
  </tr>
  <tr>
   <td>Launch Menu Icon URL</td>
   <td>Defines the location of the icon which appears in the Launch Menu (at 128 x 128 pixels), provided the “visible” menu flag (mentioned below) is checked.</td>
   <td>Widget Editor, Properties Tab</td>
  </tr>
  <tr>
   <td>Remove</td>
   <td>Separates the selected user/group/widget/dashboard/stack from the selected entry. This does not delete the user/group/widget/dashboard/stack from the system. It only removes the assignment to the selected entry.</td>
   <td>All Editors</td>
  </tr>
  <tr>
   <td>Singleton</td>
   <td>Designates whether a widget can only have one instance launched per dashboard.</td>
   <td>Widget Editor, Properties Tab</td>
  </tr>
  <tr>
   <td>Universal Name</td>
   <td>A value that can be used as a widget’s global identifier across all instances of OWF. This differs from a widget GUID which is unique to a specific installation.</td>
   <td>Widget Editor, Properties Tab</td>
  </tr>
  <tr>
   <td>URL</td>
   <td>Defines the location of the web application to which the widget icon will link. This is a required field.</td>
   <td>Widget Editor, Properties Tab</td>
  </tr>
  <tr>
   <td>URL Name</td>
   <td>A unique stack name/identifier appended to the end of the Stack URL. This is a required field.</td>     
   <td>Stack Editor, Properties Tab</td>
  </tr>
  <tr>
   <td>User Management</td>
   <td>Defines whether or not the group is an automatic group, being populated and maintained by external sources. This value cannot be modified once the group has been created.</td>
   <td>Group Editor, Properties Tab</td>
  </tr>
  <tr>
   <td>Version</td>
   <td>Displays the version number of the listing. This is completely user-driven and is for informational purposes.</td>
   <td>Widget Editor, Properties Tab</td>
  </tr>
  <tr>
   <td>Visible</td>
   <td>Dictates whether a listing will show in a user’s Launch Menu. This cannot be overridden by the user.</td>
   <td>Widget Editor, Properties Tab</td>
  </tr>
  <tr>
   <td>Widget Type</td>
   <td>A drop-down menu for selecting the widget type which determines where the widget will be located. Only standard widgets appear in the Launch Menu. Administration widgets will appear under the Administration button on the toolbar. Widgets set to type Marketplace will appear under the Marketplace button on the toolbar. Metric widgets appear under the Metric button on the toolbar. <br> *Note: Instructions explaining how to associate OWF with a Metrics Service are found in the OWF Configuration Guide.*</td>
   <td>Widget Editor, Properties Tab</td>
  </tr>
  <tr>
   <td>Width</td>
   <td>Defines the launch width of the widget in pixels. Up and down arrows to the right of the field can be used to modify the overall width.</td>
   <td>Widget Editor, Properties Tab</td>
  </tr>
</table>

#2   Manager Widgets—Search 
![Search Box](OWFImages/OWF7/search_box.png) - Reduces the entries displayed in the panel to entries containing the specified word or characters entered in the search bar. Clicking the X button will clear the filter and display all entries in the panel. Clicking the search magnifying glass button will apply the search and display the filtered results in the panel.

> _Note: This is a full-text search and it is NOT case-sensitive._

##Manager Widgets -- Pagination

![Management Widget Pagination Toolbar](OWFImages/OWF7/manager_widgets_pagination_toolbar.png)

**Figure: Management Widget Pagination Toolbar**

* ![Pagination Buttons](OWFImages/OWF7/pagination.png) - Navigates between pages of results displayed in the search results panel.
* ![Refresh Button](OWFImages/OWF7/refresh_button.png) - Refreshes the results in the search results panel, maintaining the current filtering and sorting options.
* ![Displaying Listing Results Information](OWFImages/OWF7/numbering.png) - Displays the number of results being shown against the overall total in the system.

#3 Widget Approval

By default, widgets are automatically added to a user’s Launch Menu when the user adds them from Marketplace. The widgets will be available for use immediately.  However, administrators can configure OWF to store widgets in a pending state until they are approved by an administrator. In that case, widgets will not be available to users until an administrator approves them.

> _Note: Find instructions for enabling the Widget Approvals feature and adding the Approvals Widget in the OWF Configuration Guide._ 

To approve pending widgets, an administrator must navigate to the Approvals Widget by clicking the Administration button on the toolbar and then selecting Approvals. 

![Marketplace Approvals](OWFImages/OWF7/mp_approvals_button.png)

**Figure: Marketplace Approvals**

The Approvals Widget will open, which lists all the widgets pending approval. The list can be sorted by Widget or Requesting User. 

![Approvals Widget](OWFImages/OWF7/approvals_widget.png)

**Figure: Approvals Widget**

To approve or reject widgets:

1. Check the checkbox to the left of a pending widget or widgets.
> _Note: Widgets must be approved or rejected for each user. Approving a widget for one user will not approve it for another._

2. Click Approve or Reject at the bottom of the window.
3.	After approving the widget, it will appear in the requesting user’s Launch Menu. If a widget is rejected, it will be removed from the Approvals Widget. 

##Approving Required Widgets

A Marketplace listing can require other Marketplace listings. For example, if a user requests Widget A and it requires Widget B, the user automatically requests Widgets A and B. This relationship is further explained in the OWF [User’s Guide](User%27s-Guide-Home). 

If the instance of OWF allows users to bypass the pending approval process, those users will immediately receive all requested Marketplace widgets along with any required widgets that they need. 

In the Approvals Widget, an administrator has two ways to identify that a Marketplace listing requires other Marketplace listings. When a listing is selected: 

* The details section of the listing will display: <b>Requires Widgets: true</b> 
* Its requirements will appear below the listing details

Both identifiers are highlighted in the following example:

![Required Widget Identifiers](OWFImages/OWF7/required_widget.png)

**Figure: Required Widget Identifiers**

If an administrator approves a widget that requires other widgets, the required widgets will be automatically approved.