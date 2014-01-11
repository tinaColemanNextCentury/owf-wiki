#Dashboards
##1 Overview

In simple terms, a dashboard is a screen where a user can dictate (for the most part) which widgets to load, which layouts to use, and the arrangement of the widgets within the specified layouts. Users can include multiple layouts on one dashboard using the Dashboard Designer. 

Once saved, each time a specific dashboard loads, the screen and widget layout maintain the same look and feel as the last time the dashboard was accessed by a specific user. Dashboards and their respective configurations are limitless; a user can have any number of dashboards, all of which render and function independently. 

The Group Dashboard feature provides identical dashboards for each member of a group. Each group member can customize their instance of a pre-configured dashboard. Stack Dashboards also provide identical dashboards for each person who receives a stack. Those dashboards can also be customized. Both group dashboards and stack dashboards can be restored to their default states.  

## 2 Dashboard Layouts and Configurations 

OWF provides a set of standard layout options for organizing and displaying widgets in a browser window. Descriptions and instructions for adding widgets to the five layouts are explained in the following sections. If a dashboard has more than one layout, users can resize the sections by dragging the divider between them. 

> _Note: Background widgets do not appear on OWF dashboards. These widgets will often interact with other widgets and can be used for caching and logging._

###Accordion Dashboard Layouts 

<b>Accordion dashboard layouts </b>display widgets in equal horizontal panes. When a widget is added to the dashboard, all the widgets are resized to display equally in the OWF window. The OWF window does not scroll. Each individual widget (as shown below) will scroll using its own scroll bar. 

![Accordion Dashboard Layout](OWFImages/OWF7/accordion.png)

<b>Figure: Accordion Dashboard Layout </b>

###Desktop Dashboard Layouts

Desktop dashboard layouts, similar to the desktop on most personal computers, allow the user to open widgets from the Launch Menu and place widgets freely in the window and minimize them on a taskbar. 

![Desktop Dashboard Layout](OWFImages/OWF7/desktop_dashboard.png)
<br><b>Figure: Desktop Dashboard Layout</b>

###Portal Dashboard Layouts

<b> Portal dashboard layouts </b>comprise a column-oriented layout that organizes widgets of varying heights. Each new widget loads above the first one on the screen. The user drags a dividing bar to specify widget height. The widgets and the OWF window scroll. 

![Portal Dashboard Layout](OWFImages/OWF7/portal_dashboard.png)

<b>Figure: Portal Dashboard Layout</b>

###Tabbed Dashboard Layouts
<b>Tabbed dashboard layouts</b> display one widget per screen. Like browser tabs, the tabs at the tob of the screen switch from one widget to another. 

![Tabbed Dashboard Layout](OWFImages/OWF7/tabbed_dashboard.png)

<b>Figure: Tabbed Dashboard Layout</b>

###Fit Dashboard Layouts

<b>Fit dashboard layouts</b> allow a user to place a single widget on the screen.  A launched widget shows no border or chrome and will occupy the full size of the available framework. Think of it like making a PowerPoint presentation fullscreen within the designated OWF window. If a user wishes to launch an additional widget, they will be notified that the initial widget will be replaced by the new one.

> _Note: Some widgets are automatically launched by other widgets. In these cases, the widgets will “float” on top of the dashboard._

![Fit Dashboard Layout](OWFImages/OWF7/fit_dashboard.png)

<b>Figure: Fit Dashboard Layout</b>

###Group Dashboards

Group Dashboards allow members of a group to have identical copies of a dashboard. These dashboards are assigned to a group by an administrator. A user can customize their instance of the Group Dashboard. Those changes will ONLY affect that user’s instance of the dashboard. For information about restoring a dashboard to the current default Group Dashboard see the **Restoring Dashboard** section.

> _Note: If a Group Dashboard is deleted by an administrator, the users’ copies of that dashboard will remain available to each user. However, the ability to restore that dashboard will be removed because it will no longer be a Group Dashboard._

###Stack Dashboards
A stack is a collection of dashboards and widgets. Users who receive a stack receive identical copies of the dashboards that are included in the stack. The dashboards are assigned to the stack by an administrator. A user can customize or delete their instance of the stack’s dashboards. Those changes will ONLY affect that user’s instance of the dashboards. For information about restoring a dashboard to the current default Group Dashboard see the **Restoring Dashboard** section.

> _Note: If a Stack or its dashboard are deleted by an administrator, the users’ copies of the stack, including its dashboards and widgets, will disappear._ 

##3 Launching/Switching Dashboards

After a user creates and saves a dashboard, a link to that dashboard will appear as one of the choices under the Switcher button on the toolbar.

![Switcher](OWFImages/OWF7/switcher.png)

<b>Figure: Switcher</b>

To launch a saved dashboard:

1. Click the Switcher button on the toolbar.
2. Select the desired dashboard. It will automatically open.

##4 Creating Dashboards

To create a new dashboard:

1. Click the Switcher button on the toolbar to open it.
2. Click the + to open the Create Dashboard window.
3. Give the dashboard a Title. 
    > _Note: The Dashboard cannot be saved until it is named._
4. Provide an optional Description.
5. Optionally, a user can select from the following radio buttons:
    * Create from existing and select the dashboard layout from the drop-down selector.
    * Import a dashboard by browsing to and importing a saved JSON configuraiton file.
6. Click OK. This will load the Dashboard Designer.
7. In the Dashboard Designer, select layouts and divisions for the dashboard.
8. Click Save, the new dashboard will open. To add widgets, open the Launch Menu and Launch widgets.

###Dashboard Designer
![Dashboard Designer](OWFImages/OWF7/dashboard_designer.png)

<b>Figure: Dashboard Designer</b>

The Dashboard Designer provides the following tools:
####Dividers
When using the Dashboard Designer, there are two ways to divide the dashboard into sections: 

* ![Horizontal Divider](OWFImages/OWF7/horizontal_db_divider.png)-- Horizontal Dividers can be used to divide the dashboard (or sub-sections of the dashboard) into upper and lower panes.
* ![Vertical Divider](OWFImages/OWF7/vertical_db_divider.png) -- Vertical Dividers can be used to divide the dashboard (Or sub-sections of the dashboard) into left and right-side panes

####Dashboard Layout Types

There are currently five types of dashboard layouts. During the design process, any of the dashboard layouts can comprise a whole dashboard or a section of a dashboard:

* ![Accordion Icon](OWFImages/OWF7/accordion_icon.png) -- Accordion Layout. See **Accordion Dashboard Layouts** for more details.

* ![Desktop Icon](OWFImages/OWF7/desktop_icon.png) -- Desktop Layout. See **Desktop Dashboard Layouts** for more details.

* ![Portal Icon](OWFImages/OWF7/portal_icon.png) -- Portal Layout. See **Portal Dashboard Layouts** for more details.

* ![Tabbed Icon](OWFImages/OWF7/tabbed_icon.png) -- Tabbed Layout. See **Tabbed Dashboard Layouts** for more details.

* ![Fit Icon](OWFImages/OWF7/fit_icon.png) -- Fit Layout. See **Fit Dashboard Layouts** for more details.

##5 Using the Dashboard Designer

The following walkthrough will explain how to build a new dashboard with Accordion, Desktop and Tabbed Dashboard Layout sections:

1. Click the Switcher button on the toolbar to open the Switcher.
2. Click the + button to open the Create Dashboard window.
3. Give the dashboard a Title:
 > _Note: The Dashboard cannot be saved until it has been named._
       * a. Provide an optional Description.
       * b. Optionally, a user can select from the following radio buttons:

           * i. Create from existing and select the dashboard layout from the drop-down selector.
           * ii. Import a dashboard by browsing to and importing a saved JSON configuration file. 
4.	Click OK.
5.	Drag a Horizontal Divider onto the Dashboard Designer; the screen will divide.
6. Drag the Vertical Divider onto the upper level of the designer. The screen should mirror the image below:

![Divided Dashboard Designer](OWFImages/OWF7/divided_db_designer.png)

<b>Figure: Divided Dashboard Designer</b>

The dashboard is now divided into multiple sections. Each section can be further divided, or can have a dashboard layout dragged into it. To resize sections, drag the Divider between them or type a different value into one of the section’s screen percentage box. The related pane will automatically adjust. At any point during the dashboard creation, it can be saved, reset or cancelled.

When a section of the dashboard is clicked, it will be surrounded in a solid border. Its partner sections of the dashboard will highlight in a broken line. These combined sections (solid red border and broken red border) equal 100 percent of a viewing area.

In the image above, the right-side partner is surrounded by a solid red line. The left-side partner is surrounded by a broken red border. Together, they equal 100 percent of the upper pane of the dashboard.

> _Note: A user can also use pixels values instead of a percentage value when they need to make a more precise cell size. In the image above, a user would be able to make either of the dashboard sections an exact number, 250px, for example.  When this happens, its partner presents the label “variable.”  Entering a number and using a P or a PX will designate pixels._

Next, the user can drag dashboard layout type icons into each section of the dashboard.

![Dashboard Designer with Layout Icons](OWFImages/OWF7/db_designer_with_icons.png)

<b>Figure: Dashboard Designer with Layout Icons</b>

In the image above, each section of the dashboard has a layout type icon in place.
The upper-left section contains the Accordion layout icon and has changed to a red background. The upper-right section contains the Desktop layout icon and has changed to a yellow background. The lower section is a Tabbed layout and has changed to a blue background. Each individual section allows for the layout of widgets in accordance with the properties of the layout icon. Once the layout icons are in place, the user can save the dashboard. After saving the dashboard, it will launch automatically. It can also be launched from the Switcher by using the Switcher button. Individual dashboard sections can now be populated from the Launch Menu.

* <b>Reset</b> -- Clears the modifications to the dashboard.
* <b>Lock/Unlock</b> -- Use this button to restrict changes to the dashboard layout and the widgets displayed on it. When the dashboard is locked, widgets cannot be added or removed and sections cannot be edited, however, the layout of a locked dashboard is still editable.
* <b>Save</b> -- Saves the dashboard, closes it and launches it.
* <b>Cancel</b> -- Cancels changes made since the last Save or since entering the designer.

###Importing a Dashboard
To import a dashboard:

1.	Click the Switcher button on the toolbar to open the Switcher.
2.	Select the + button to open the Create Dashboard window.
3.	From the radio buttons, select: Import.
4.	Browse to and select a saved JSON dashboard file.
5.	Click OK. 

> _Note: Due to the dashboard redesign in OWF 6, OWF 7 will only accept imported dashboard files from OWF 6 or 7._

##6   Customizing Dashboard
Use the Dashboard Designer to assign layouts to sections of a dashboard. To add widgets to the dashboard:

1.	Click the Switcher button on the toolbar to open the Switcher, select a dashboard to modify.
2.	Open the Launch Menu and add widgets from the menu to the dashboard. To add widgets to a dashboard using keyboard navigation, see **Launch Menu Navigation** section on the [Keyboard Navigation](OWF-7-Users-Keyboard-Navigation). 

###Changing a Dashboard Layout
If a user has set up a specific dashboard with all the widgets they need, but they would like to see the widgets displayed in a different layout, they can easily switch layouts.
To change a dashboard layout:

1.	Click the   button on the toolbar to open the Switcher, click the Manage button.
2.	Select a Dashboard and then click the Edit button below the dashboard.
3.	The Edit Dashboard window will open. After reviewing or modifying the Title and Description fields, click OK. 
4.	The Dashboard Designer window will launch. From there, the layout can be changed. 
5.	Click Save.

> _Note: While all widgets will be present in the new dashboards, specific ordering of widgets will differ based on the dashboard layout(s)._

###Renaming a Dashboard
To rename a dashboard:

1.	Click the Switcher button on the toolbar to open the Switcher, click the Manage button.
2.	Select a dashboard and click the Edit button below the dashboard.
3.	Change the dashboard Title. 
4.	Click OK.
5.	The Dashboard Designer window will launch. From the right-navigation panel, click Save.

##7   Managing Dashboards
Starting with OWF 7, users can Create, Edit, Delete and Share dashboards from the Switcher. To Edit, Delete or Share dashboards, open the Switcher (Alt + Shift + C), tab to the Manage button and press enter. This activates editing capabilities for each dashboard as shown below in the Administration Dashboard:

![Manage Settings in the Switcher](OWFImages/OWF7/manage_settings_in_switcher.png)

<b>Figure: Manage Settings in the Switcher</b>

The Manage button allows users to:

* ![Share icon](OWFImages/OWF7/Share_icon.png) - Share the dashboard JSON files 
* ![Restore icon](OWFImages/OWF7/Restore_icon.png) - Restore a dashboard to its default state. 
* ![Edit icon](OWFImages/OWF7/Edit_icon.png) - Edit existing dashboards (Edits include adding panels and layout types on a dashboard as well as changing the dashboard title and description). 
* ![Delete icon](OWFImages/OWF7/Delete_icon.png) - Delete dashboards.

###Sharing a Dashboard

The share feature allows a user to send their dashboard configuration (this includes the dashboard layout and the widgets that are on it) to another user. 

To share a dashboard: 

1.	Click the Switcher button on the toolbar to open the Switcher, click the Manage button. 
2.	Select a dashboard. The editing options will appear below the dashboard. 
3.	Select the Share button. This action saves a JSON copy of the dashboard to the location where the user’s downloads are stored (frequently the computer desktop or a downloads folder in My Documents). 
4.	Send the JSON file to another user. They can find instructions for adding the file to their instance of OWF in the **Importing a Dashboard** section.

> _Note: Due to updates, OWF will not accept imported files created in versions earlier than OWF 6._  

###Restoring a Dashboard

Every member of a group receives an identical copy of a Group Dashboard. Similarly, dashboards nested within stacks are identical copies of the dashboards associated with the stack. From their instance of OWF, a user can customize their version of the dashboards. The restore feature allows the user to cancel their customizations and returns the dashboard to its current default state. If the default group or stack dashboard changed after it was added to a user’s instance of OWF, the current default state of the dashboard may be different than the one that originally appeared in the user’s Switcher.

> _Note: If a group dashboard is deleted by an administrator, a user’s copy of that dashboard will NOT be deleted. However, the restore feature will no longer be available for the dashboard. If a stack or its dashboard is deleted by an administrator, a user’s copy of that stack, including its widgets and dashboards, will be deleted._

To restore a dashboard to its current default state:

1.	Click the Switcher button on the toolbar to open the Switcher, click the Manage button. 
2.	Select the dashboard and click the Restore button below the dashboard.
3.	The dashboard will return to its <i>current default state</i>.

###Editing a Dashboard
The edit dashboard option allows users to change a dashboard’s name, layout, description and position within the Edit Dashboard window. 

To edit a dashboard:

1.	Click the Switcher button on the toolbar to open the Switcher, click the Manage button. 
2.	Select a Dashboard and then click the Edit button below it. 
3.	The Edit Dashboard will open. 
    * a.	Update the Title or Description
    * b.	Click OK, this will load the Dashboard Designer, see the **Dashboard Designer** section for instructions. 
4.	Make changes then click the Save button. 

###Deleting a Dashboard

To delete a dashboard:

1.	Click the Switcher button on the toolbar to open the Switcher, click the Manage button.
2.	Select a Dashboard and then click the Delete button below it. 
3.	A warning message will appear.
4.	 Click OK.

> _Note: Users cannot delete group dashboards or individual stack dashboards from their OWF instance._
