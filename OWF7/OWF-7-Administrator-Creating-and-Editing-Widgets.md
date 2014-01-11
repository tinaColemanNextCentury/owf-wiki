This page explains how administrators can create and edit widgets. 
#1 Creating Widgets

Administrators can **create**, **edit**, **delete**, **import** and **export** widgets. There are two ways to create a widget: importing widget data with a descriptor URL or manually entering widget data. Imported widget data is editable through the Widget Editor (see the **Editing Existing Widget Content** section). 

To create a widget, the administrator must complete several mandatory fields in the Widget Editor. Information about each widget data field is found in the Edit Button and Editor Widget Fields Table. For example, the Widget Type field is useful for separating widgets on a user’s toolbar. Only Standard widgets will appear in the Launch Menu. Administration widgets will appear under the Administration button on the toolbar. Widgets set to type Marketplace will appear under the Marketplace button on the toolbar. Metric widgets will appear under the Metric button on the toolbar.

To create a widget:	

1.	Click the ![Administration Button](OWFImages/OWF7/administration_button.png) button on the toolbar.
2.	Click the Widgets button to open the Widget Manager.
3.	From the manager, click the Create button to open the Widget Editor.
4.	From here, there are two ways to create widgets:

    A. **Import a descriptor URL** — Enter a descriptor URL and click Load. For more information about descriptor URLs see section **Widget Descriptor URL**.

    B. **Manually enter data** — If a descriptor URL is not available, click the “Don’t have a descriptor URL?” link and complete the required fields on the Properties tab. Remember that the Widget Type will dictate the location of the widget. For more information about specific entry fields, see the Edit Button and Editor Widget Fields Table. 

5.	Click Apply. This will unlock the Users, Groups and Intents tabs on the Widget Editor. Select each tab and click the Add button to add users, groups and intents to the widget. Information about adding Intents to a widget is in the section **Creating Widget Intents**.
6.	Refresh OWF. The new widget will appear under the respective toolbar button. For more details about connecting to Marketplace(s), see [Connecting to Marketplace](OWF-7-Administrator-Connecting-to-Marketplace).

#Creating Widget Intents

Widget intents are the instructions for carrying out a widget’s intentions. Intents are comprised of an Action (graph, view, edit, etc.), a Data Type (html, text, image, etc.) and a Send/Receive request. If widgets have identical Action and Data Types, then the widgets that send intents can communicate with the widgets that receive intents. For example, the New York Stock Exchange (NYSE) widget sends an intent to graph (Action) daily stock data (Data Type). The Stock Chart widget, having an intent with the same Action and Data Type, receives this request and graphs the data. This binding capability enables the two widgets to enhance each other’s functionality. Administrators can add, edit and delete widget intents, however, a developer or someone with experience using intents is more likely to perform these tasks.

> _Note: Find instructions about using intents in the OWF User’s Guide and instructions about creating intents in the OWF Developer’s Guide. OWF follows standard Web Intent specifications documented at [Webintents.org](http://webintents.org/#specification "Webintents.org")._

To add intents to a widget:
 
1.	Click ![Administration Button](OWFImages/OWF7/administration_button.png) button on the toolbar, select Widgets to open the Widget Manager.
2.	From the manager, select the widget to be updated and click Edit. 
3.	Click the Intents tab. Click Create to open the Create Intent widget.
4.	Complete the fields, required fields are marked with an asterisk.
    * <b>Action</b> - The Action field is the instruction the intent will make (ex. graph or view). 
    * <b>Data Type</b> - The Data Type field indicates the data that the intent is passing from widget to widget (ex. text/html). 
    * <b>Send/Receive</b> - This tells the widget to send or receive the widget intent. 
5.	Click OK. The intent has been added to the widget and will be displayed in the Intents tab in the Widget Editor.

##Widget Descriptor URL
Descriptor URLs allow an administrator to create widgets without entering the widget's information manually. The administrator simply enters a URL and the widget's information is automatically retrieved from a descriptor file from a Web-accessible location. Starting with OWF 7, widgets created with a descriptor URL are editable in the Widget Editor. 

Descriptor URLs offer several benefits. They reduce the risk of typing errors when entering widget data. They allow for several installations of OWF to easily share widget information via the descriptor file.

#2 Editing Existing Widget Content

To edit existing widget content:

1.	Click  ![Administration Button](OWFImages/OWF7/administration_button.png)  on the toolbar, select Widgets to open the Widget Manager. 
2.	From the manager, select a widget and click Edit. 
3.	Edit the widget data on the Properties tab and click Apply. For definitions of less common widget data fields, see the Edit Button and Editor Widget Fields Table.

Users and groups assigned to the widget will receive the widget data changes automatically.

##Updating and Editing Widget Descriptor Data
Starting in OWF 7, administrators can update and edit the widget descriptor data within the OWF interface. Updating the widget descriptor data retrieves the latest data in the widget’s descriptor file which is saved in a Web-accessible location. Changes made to the widget prior to the update are lost once the update is performed. 

To update the widget descriptor data:

1.	Click ![Administration Button](OWFImages/OWF7/administration_button.png) button on the toolbar, select Widgets to open the Widget Manager. 
2.	From the manager, select a widget and click Edit. 
3.	Click Load. The Widget Editor will automatically refresh and display the most recent widget descriptor data. 
4.	Click Apply.
 
Administrators can edit their copy of the widget descriptor data by following the steps outlined in the **Editing Existing Widget Content** section. Descriptor data changes are sharable after the administrator exports the widget and saves the descriptor file in a Web-accessible location. Individuals who already have access to this widget will have to update their copy of the widget’s descriptor data in order to see the widget changes in their OWF instance.

##   Editing Widget Intents
It is recommended that a developer, or an individual experienced with using intents, edits the widget intents.

To edit widget intents:

1.	Click ![Administration Button](OWFImages/OWF7/administration_button.png) button on the toolbar, select Widgets to open the Widget Manager.
2.	From the manager, select a widget and click Edit. 
3.	Click the Intents tab, select an intent and click Edit.
4.	Once changes have been made, click OK. OWF will automatically update the widget data.
5.	Close the Widget Editor.

Users assigned to this widget will see the changes automatically. 

To delete widget intents:

1.	Click ![Administration Button](OWFImages/OWF7/administration_button.png) button on the toolbar, select Widgets to open the Widget Manager.
2.	From the manager, select a widget and click Edit.
3.	Click the Intents tab, select an intent and click Delete.

#3   Exporting Widgets
Starting with OWF 7, administrators can export and save widget data as a descriptor file. An administrator needs to host the widget descriptor file in a Web-accessible location to make the file sharable with other administrators that have access to this location. This process is intended to provide a means for administrators from different OWF instances to add/receive identical widgets.

To export a widget:

1.	Click the ![Administration Button](OWFImages/OWF7/administration_button.png) button on the toolbar.
2.	Click on the Widgets button to open the Widgets Manager.
3.	Select the widget to export. Click the arrow on the right of the split Edit button and choose Export.
4.	Enter a File Name that describes the widget, this will become the title of the HTML descriptor file. Then click OK.
> _Note: If the widget was created by a descriptor file, the File Name field will be pre-populated with the descriptor file name._ 

5.	Save the widget descriptor HTML file on a Web-accessible server. 