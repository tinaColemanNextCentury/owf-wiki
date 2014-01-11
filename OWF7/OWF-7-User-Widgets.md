#Widgets

#1 Overview
A widget is a lightweight, single-purpose application that offers a summary or limited view of a larger application. In OWF, a widget is a global description for a piece of Web content that can be configured by the user and displayed within a dashboard.

## Singleton Widgets
Singleton widgets allow only one instance of the widget to launch on a dashboard. (Users can open multiple instances of regular widgets on each dashboard.) If a Singleton widget is open on a dashboard and a user tries to open another instance of the widget, the open instance will move to the forefront of the screen. Administrators may make a widget a Singleton for numerous reasons. For example, preventing users from launching multiple instances per dashboard may reduce confusion, increase performance (if the widget uses a substantial amount of memory), or address another need.

## Background Widgets
Background widgets run but do not appear on a user’s dashboards. They often serve as caching and logging tools that do not have a user interface. Background widgets can be obtained from a Marketplace server or configured by an OWF administrator. Most users will not be aware that Background widgets are running in their instance of OWF. However, Background widgets will appear on the Widget Switcher. Closing them may interrupt data transfer from other widgets. Use the Widget Switcher (Alt + Shift + Q) to close Background widgets. After selecting a Background widget, a warning message will appear. To close the widget, select OK. If the Background widget is visible (an administrator has not hidden it from the Launch Menu), a user can restart it by dragging it from the Launch Menu to the dashboard. 

![Backgroun Widget Warning Message](OWFImages/OWF7/background-widget-warning.png)

<b>Figure: Background Widget Warning Message </b>


#2 Searching for Widgets
OWF provides two search options. From the Launch Menu, users can search using:

*	<b>Widget Title Search</b> - Located in the upper-right portion of the Launch Menu, this field allows users to filter the list of widgets by title. 
    > Note: A user cannot type search queries into the title search if a search query is typed into the advanced search. 

*	<b>Advanced Search</b> – Collapsed by default, the advanced search features appear when a user clicks the arrow located in the center of the left side on the Launch Menu. The Advanced Search Panel includes several searching features:
    * <b>Advanced search box</b> – Searches widgets by name. Users can type multiple search queries into the box and they will display below the Search box. To use it, press enter after entering each search term. To remove a search term, click the red circle to the right of the term. To clear the entire search, click Reset at the bottom of the panel.
  
    * <b>Groups</b> – Filter widgets by group, see the **Groups** section on the [Categorizing Widgets](https://github.com/ozoneplatform/owf/wiki/OWF-7-User-Categorizing-Widgets) page.

    * <b>Intents</b> – Clicking an intent will filter the Launch Menu to display only widgets that can send or receive that intent. For more information, see the **Widgets Intents (Widgets Launching Widgets)** section. Clicking an intent highlights it. To deselect it, click it again. This action removes the filter. 

    * <b>Tags</b> – Displays all the tags that are associated with the user’s widgets in a tag cloud formation (Tags that are used more often are bigger.). Clicking a tag will filter the Launch Menu to display only widgets that use that tag. See the **Tags** section on the [Categorizing Widgets](https://github.com/ozoneplatform/owf/wiki/OWF-7-User-Categorizing-Widgets) page.  

    * <b>Reset</b> – Clears all filters.  

## Launching Widgets
![Launch Menu](OWFImages/OWF7/launch_menu_expand.png)

<b>Figure: Launch Menu</b>

To launch a widget: First, open the Launch Menu by clicking the first button on the toolbar. Then, double-click the desired widget, select it and click the Launch button at the top of the menu or drag the widget from the Launch Menu to the dashboard. Repeat this action for each widget. Also, users can launch multiple instances of a widget unless the widget is a singleton.

The Launch Menu includes a Favorites Pane, used for quick access to widgets, and several advanced searching features. 

### Widgets Intents (Widgets Launching Widgets)
Widget Intents are the instructions for carrying out a widget’s intentions. One widget requests an action (Think of actions as verbs like view, share, edit, etc.) then another widget receives that request and performs the action. Intents build on OWF’s publish/subscribe feature by allowing users to choose the widget(s) that will use data. This binding capability enables two widgets to share data in a way that improves their function. 

For example, the NYSE Widget charts data about the stock exchange. Some users may want to view that data as a Web page. This is possible if the NYSE Widget has an intent that tells it to send data to widgets that display data in a Web format. 

> *Note: Widgets may have multiple intents associated with them. Users cannot create Widget Intents. Administrators and developers (logged in as administrators) add widget intents through the OWF interface. Developers also add the intents through widget descriptor URLs. OWF follows standard Web Intent specifications documented at [Webintents.org](http://Webintents.org "Webintents.org").*

<b> How to use intents:</b>

If a widget uses intents, the Launch Menu will pop up when a user clicks on data in that widget. The Launch Menu will display only widgets and intents that can use the data for an intended purpose (graphing, displaying, etc.). 

The Advanced Search Panel displays all the intents that are in OWF, the intent types (graphing, display, etc.) separate the widgets. Only the widgets that are associated with the specific intent are selectable. 

Widgets that use the requested intent will appear under the heading “Current Instances” or “Open a new Instance.” “Current Instances” widgets are open in your dashboard and when clicked on, are used to accept the intent. Clicking on a widget under “Open a new Instance” opens a new instance of the widget that accepts the intent data. To choose a widget:  Select it, then click Launch or double-click the widget. The data from the first widget will appear in the second widget. Checking the “Remember this decision” box beside the Launch button will cause the selected widget to automatically open the data with the selected widget until a user breaks the connection by closing the widget sending the intent or the widget receiving the it. 


[[Removing, Renaming, Reordering Widgets|OWF-7-Users-Removing-Renaming-Reordering-Widgets]]

[[Categorizing Widgets|OWF-7-User-Categorizing-Widgets]]

[[Accessing Widgets from <b>Marketplace</b>|OWF-7-Users-Accessing-Marketplace]]