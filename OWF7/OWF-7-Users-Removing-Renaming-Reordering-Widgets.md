#Removing, Renaming and Reordering Widgets

#1 Removing Widgets

Users can remove any directly assigned widgets from their instance of OWF. This action will not delete the widget from OWF, it will only delete the widget for that user. Only administrators can delete widgets from the system. 

To delete a widget from a user’s instance of OWF:

1. Click the Settings button on the toolbar. Then click Widgets to launch the Widget Settings window.

2. From the Widget Settings window, select a widget and check the Delete checkmark. Click OK. This removes a widget from a user’s Launch Menu and their instance of OWF. If a deleted widget is needed at a later date, it can only be restored by an administrator or added from Marketplace (if the widget is available there). 

> _Note: Widgets which are pending approval cannot be deleted from the widget settings window. Users cannot delete widgets that have been given to them through a group assignment._

## Hiding/Showing Widgets in the Launch Menu

By default, all widgets that are assigned to a user are visible in that user’s Launch Menu unless an administrator hid the widget from view. 

This feature is meant to reduce clutter, hiding widgets from the Launch Menu will NOT remove them from a user’s instance of OWF. 

To hide a widget from the Launch Menu:

1. From the toolbar, click the Settings button and then choose Widget to open the Widget Settings window.

2. From the Widget Settings Window, uncheck the Show checkbox and click OK. The widget will be hidden from the Launch Menu but still associated with the user. 

### Showing Widgets in the Launch Menu

To show a widget in the Launch Menu: 

1. From the toolbar, click the Settings button then choose Widgets to open the Widget Settings window.
2. From the Widget Settings window, check the Show checkbox for a specific widget, click any other row, and then click OK. After refreshing, the widget will be visible in the Launch Menu. 

### Reordering Widgets in the Launch Menu

To reorder widgets in the Launch Menu’s main panel or Favorites Pane:

1. Open the Launch Menu by clicking the Launch Menu button on the toolbar. 
2.	Switch to the icon view using the Toggle buttons in the upper-right corner of the Launch Menu.
3.	Click a widget then drag it left, right, up or down. Release the mouse to complete the move.  

#2 Customizing and Categorizing Widgets

##Renaming Widgets

To change the name of a widget:

1. From the toolbar, click the   button, then choose Widgets to open the Widget Settings window.
2. Click on the title of a widget, which will open an editable field.
3. Type a new title for that widget.
4. To save the change, press enter on the keyboard and click OK. 
   > _Note: If a user clicks OK while the editable field is active, changes in that field may not be saved._ 

   Until the change is saved and applied to the Launch Menu, a red triangle will appear in the upper-left corner of the widget title: 
 
The custom widget titles only appear for the authenticated user’s instance of OWF (The title will not change system-wide). Also, the new title will only apply on widgets that are launched after the title change. To rename widgets that are open on a dashboard, the user must close the widget and reopen it.

##Renaming a Widget Instance on a Dashboard

It is possible for a dashboard to have multiple instances of the same widget open at the same time (unless the widget is a Singleton, see the **Singleton Widgets** section found on the [User Widgets](OWF-7-User-Widgets). Accordingly, a user may want to rename one or more instances of that widget. The title for each instance of an open widget on a dashboard is customizable per instance.
The widget title can be edited by double-clicking the widget title in the widget header. The title will change to an input field where the user can modify it. Pressing enter on the keyboard or clicking anywhere on the dashboard will save the new title for the current instance. Regardless of the number of times the widget appears on the dashboard, the change will only impact that single widget.

![Renaming a Widget](OWFImages/OWf7/renaming_widget.png)

<b> Figure: Renaming a Widget </b>

###Reverting to default name of Widgets
To restore the default name of a widget, open the Widget Settings window by clicking the Settings button in the toolbar and then choosing Widgets. Then, right-click a widget and choose Reset Title. The widget will return to its default name. 
 
![Restoring Default Image Name](OWFImages/OWF7/restoring_widget_name.png)

<b> Figure: Restoring Default Widget Name</b>

To revert all custom named widgets (this does not apply to widgets that are open on the dashboard) to their default names, right-click on any widget on the manage widgets screen, select reset all titles and click OK. 