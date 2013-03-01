#  Adding a Widget to OWF

#1   Overview

OWF provides a Widget Manager, located by clicking the Administration button on the toolbar in the application. Administrators can use the manager to create widget descriptor files and add widget definitions to OWF. The manager allows an administrator to complete the widget definition or edit the descriptor URL in the user interface, then OWF maps the widget to users in the system. Once a widget definition has been created and mapped to a user, it will then be added to the user’s Launch Menu or toolbar depending on the widget type. 

Due to the fact that a widget definition actually points to the URL of a lightweight Web application, an administrator is not required to update widget definitions unless the location of the widget changes.

#2   Walkthrough

##Creating Descriptor Files for Widgets

Developers can save the widget information in the descriptor file and then share that file with administrators. This allows administrators to import widget data instead of typing entries for each field. The administrator simply enters a URL and the widget's information is automatically retrieved from a descriptor file that a developer maintains. Administrators can change properties in the widget definition once it has been added to OWF. However, an administrator’s changes will only affect their deployment of OWF, unless the administrator exports those changes to the Web-accessible location where the descriptor URLs are stored. 

Descriptor URLs offer several benefits. They reduce the risk of typing errors when entering widget data into the OWF interface. They allow for several installations of OWF to easily share widget information via the descriptor file. In addition, descriptor files can contain a universal name which is a developer-generated, custom identifier that can be used to identify the widget across multiple OWF instances.   

To create a widget descriptor URL, follow these instructions:

1. Sign in to OWF as an administrator. 
2. Click the Administration button on the toolbar and select Widgets to open the Widget Manager. 
3. Click Create to open the Widget Editor.
4. Click “Don’t have a descriptor URL?”
Populate the mandatory fields in the widget definition and click Apply. 

 > _Note: For more information about specific entry fields, please see the Administrator’s Guide._

5. OPTIONAL: Add the capability to send widget intents. An Intent is simply an object describing an action and a data type. Sending an Intent should be tied to a user-generated action such as clicking a button or link. (If the widget does not require an intent, skip this step.) 
Starting in OWF 7, developers should use the Widget Editor to add and edit widget intents. 

   A. To add an intent, select the Intents tab in the Widget Editor and click Create. 

   B. Populate the following fields:

       i. **Action** - The Action should be a verb describing what the user is trying to do (i.e. plot, pan, zoom, view, graph, etc.). 

  > _Note: Intents are NOT case sensitive._

       ii. **Data Type** - The Data Type is an object containing the data that the intent is sending. It describes what type of data is being acted upon. The data type format is described in the section entitled **Recommended Intents Data Type Conventions** located on the [Widget Intents API](https://github.com/ozoneplatform/owf/wiki/OWF-7-Developer-Widget-Intents-API) page. 
        The format of the data depends solely on how the sending or receiving widget is expecting to use the data. For example, “ `application/vnd.owf.sample.price` ” tells the NYSE Widget’s how to display price. 

       iii. **Send** – Checked by default, this field identifies if the widget can send intents.

       iv. **Receive** –This field identifies if the widget can receive intents. 

   C. Click OK.
6. Return to the Widget Manager:

   A. Select the new widget.

   B. Click the split Edit button, then select Export from the drop-down menu.

7. Enter a File Name (this will be the name of the HTML descriptor file) and click OK.
8. Save the file to a Web-accessible location like a directory where widget data is stored.
9. Return to the OWF user interface and open the Widget Manager. Select the new widget, and click Edit. 
10. From the Widget Editor, enter the new Descriptor URL location, click Load, then, click Apply. 

> _Note: From the Widget Editor, administrators can edit the widget descriptor URL. However, those changes will not change the “master” copy of the descriptor unless they replace the descriptor file stored at the Web-accessible location referenced above._

##Sharing Widget Descriptor Files 

There are two ways to share widget descriptors:

1. **Export the file** – To obtain an exportable HTML file, select the widget in the Widget Manager, click the split edit button and select Export.  Exporting the widget descriptor URL only sends a copy of the file. The administrator will not receive future updates to that file that is stored on the Web-accessible location. 
2. **Share the widget descriptor location** - Sending a link to the widget descriptor file that is stored on a Web-accessible location will enable the administrator to receive updates to the widget descriptor URL by clicking Load, then Apply in the Widget Editor.  