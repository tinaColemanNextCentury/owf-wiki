# Instructions
#1 Objectives
The purpose of this guide is to explain how to create a simple Widget application or integrate an existing application into the OZONE Widget Framework (OWF).

#2   Document Scope
This guide is written for software developers who want to change an existing application into an OWF-compatible widget (or widgets) or understand the APIs available to them for building widgets. 


#3   Source Code Examples

All of the code examples listed in this document can be found in the **OWF-bundle-7-GA.zip**. When unpacked or unzipped, the **OWF-bundle-7-GA.zip**. will contain a **/owf-sample-widgets.zip** which contains **.zip** files of example widgets with source code built in different technology stacks. The examples included in the distribution are detailed in the pages listed under **Example Widgets** section of the [Developer's Guide](Widget-Developer%27s-Guide-Home) page. 

#4   File Accessibility For Configuration and Development

In addition to often-modified files found in the /etc directory, OWF now delivers critical API related files outside the **.war** file for easy accessibility, as well. The directory structure is as follows:

![Configuration and Development File Locations](OWFImages/OWF7/configuration_development_file_locations.png)

**Figure: Configuration and Development File Locations**

Within the highlighted folder structure, you will find the following:

   * /etc/docs – OWF Performance Metrics .doc
   * /etc/override – Customizable override files for behavioral changes within OWF
   * /etc/tools – Executable files for the creation of certificates and theme bundles
   * /etc/widgets/css – Stylesheet with implemented drag and drop feedback
   * /etc/widgets/descriptor – Template for a widget descriptor file  
   * /etc/widget/flash-dragAndDrop -DragAndDropSupport.as that enables drag and drop in flash/flex widgets
   * /etc/widget/images – Images required for drag and drop feedback 
   * etc/widget/js – contains the following:
       * owf-widget-debug.js (OWF API for development)
       * owf-widget-min.js (OWF API for production)
       * dojo-1.5.0-windowname-only (required for Preferences API to work; previously located in the javascript directory)
       * eventing (required for Eventing API to work in IE7; previously located in the javascript directory)