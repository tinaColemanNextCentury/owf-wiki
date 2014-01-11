# Creating and Editing User Content

Creating and editing users, widgets, groups, group dashboards and stacks is explained in this section. This includes adding widgets/groups/group dashboards/stacks to user profiles through the User Editor. OWF also allows administrators to add users to widgets/groups/dashboards/stacks through the Users tab on the respective editor widgets. These examples are described in the sections entitled **Adding Widgets to a User Profile** and **Adding Users to a Widget**, both found on this page.

#1 Creating Users

Administrators have the ability to create new user profiles, edit existing user information and add widgets/groups/dashboards/stacks to user profiles.

To create a new user profile:

1.	Click the ![Administration Button](OWFImages/OWF7/administration_button.png) button on the toolbar. 
2.	Choose the Users button to open the User Manager.
3.	Click on the Create button, opening the User Editor. 
4.	Enter the user’s information. Mandatory fields (User Name and Full Name) are denoted with a red asterisk. More information about these fields is found in the Edit Button and Editor Widget Fields Table.
5.	 When complete, click Apply. This will activate the additional tabs in the User editor. 
6.	To add widgets, groups, dashboards or stacks to a user account, proceed to the instructions in either the **Adding Widgets to a User Profile** or **Adding Users to a Widget** sections. 

> _Note: Administrators do not create or maintain user passwords in the OWF interface. Security and authentication are addressed in the OWF Configuration Guide._ 

## Adding Widgets to a User Profile

The following instructions describe how to add widgets to a user account using the Widgets tab found in the User Manager. Administrators can follow this basic formula to add groups, dashboards and stacks to user profiles via the Groups, Dashboards or Stacks tabs in the User Editor widget. When assignments are complete, all of the data applied to the user profile will be instantly available.

To add widgets to a user’s account:

1. Click the ![Administration Button](OWFImages/OWF7/administration_button.png) button on the toolbar.
2. Click the Users button to open the User Manager.
3. From the manager, select a User. Then, click Edit to open the User Editor.
4. Click the Widgets tab at the top of the editor. Widgets that are already associated with the user will display in the window.  
5. To add widgets, click the Add button. A modal window will display all widgets available to that user. Select a widget, then, click the OK button. The widget will be automatically added to the list of widgets on the user’s Widget tab. 

##Adding Users to a Widget

Another way to give users access to widgets is to add users to widget profile via the Widget Editor. Again, administrators can use this general procedure to add users to groups, dashboards and stacks through the Users tabs in the respective editors. When completed, close the editor window and the data will be updated automatically to the user profile.

To add users to widget profiles:

1. Click the ![Administration Button](OWFImages/OWF7/administration_button.png) button on the toolbar.
2. Click the Widgets button to open the Widget Manager.
3. From the manager, select a widget. Then, click Edit to open the Widget Editor.
4. Click the Users tab at the top of the editor. Users that are already associated with the widget will display in the window.  
5. To add users, click the Add button. A modal window will display all users available to that widget. Select a user, then, click the OK button. The user will be automatically added to the list of users on the widget’s Users tab and the widget will be available to the user’s instance of OWF. 

##Editing User Properties 
To edit existing user content:

1.	Click the ![Administration Button](OWFImages/OWF7/administration_button.png) button on the toolbar, select Users to open the User Manager. 
2.	From the manager, select the user account that needs to be updated and click Edit. 
3.	Update data on the Properties tab and click Apply. Update each field, then click Apply. For definitions of less common fields, see the Edit Button and Editor Widget Fields Table.

This procedure is also used when editing the properties of widgets, groups, group dashboards and stacks. To edit the content, click on Administration button on the toolbar and click on the open the respective manager and click Edit to open up the editor. Make changes in the Properties tab and click Apply.

##User Preferences 

![User Preferences](OWFImages/OWF7/preferences_tab.png)

**Figure: Preferences Tab**

Widgets use preferences to store data. Preferences include widget location on the screen, launching instructions, etc. A preference value can be created and saved any time a widget performs an action. Once that preference is saved to the database, it will appear on the preferences tab in the User Editor. The Preferences tab serves as a table of known preferences. From the tab, administrators can view, create, edit and delete preferences. However, from the Preferences tab, the administrator cannot configure a widget to use a preference. For a widget to respond to preferences, the widget must be configured via the Preference API. 

If a widget is configured to use preferences, they can be used to define screen location, widget interaction, etc. For example, the guid_to_launch preference is a useful eventing tool. Administrators can use it to make a tracking widget launch a map widget. For example, in Figure 10: Preferences Tab, the guid_to_launch preference causes the User Manager to launch a copy of the Widget Editor. 

The Preferences tab includes the following fields: 

* <b>Preference Name</b> - The preference name is referred to as the “key” for the preference item. It lists the name of the preference as dictated by the widget or OWF. If the widget uses preferences, OWF will add the preference name to the table on the Preference tab whenever the action that is associated with the preference is performed. 
* <b>Namespace</b> - The namespace is the identifier for the widget or system category. Generally these identifiers will describe general functionality for a widget or set of widgets.
* <b>Value</b> - Stored inside of the preference, values house the data that the preference uses. An example could be the actual widget GUID value that the preference will use to launch a widget. This is a string value but developers can use JSON or REST URIs as the preference value.

![Preferences Dialog](OWFImages/OWF7/preferences_dialog.png)

**Figure: Preferences Dialog**
