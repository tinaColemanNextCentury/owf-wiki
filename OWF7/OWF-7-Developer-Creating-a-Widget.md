#Creating a Widget

## 1   Overview

Widgets in OWF are lightweight Web applications wrapped with a metadata definition that provide a description to the framework of how the widget should load. The widget metadata definition contains a number of fields including a URL, Default Name, Default Height and Default Width properties. 

OWF provides a suite of APIs that enable the widget developer to extend their Web application through the use of inter-widget communication, user preferences, and internationalization. Each API is written in JavaScript so that widgets can be built in a large variety of Web technologies.

Three key factors to keep in mind when creating a widget are:

   * OWF supports and encourages a decentralized deployment model. Widgets are not required to be deployed on the same server as OWF and can be distributed throughout the enterprise.
   * OWF is Web-technology agnostic. Widgets can be written in the JavaScript capable technology of the developer’s choice. Web enabled applications have been built in varied technologies such as JavaScript (EXTJS, Dojo), Java (JSPs, GWT, JSF, Groovy on Grails), .NET (ASP.NET, C# .NET), Scripting Languages (PHP, Perl, Ruby on Rails), and Rich UI Frameworks/Plugins (Flex, Silverlight, Google Earth Plugin, Java Applets).
   * OWF 6.0 added DOCTYPE. In most browsers, widgets will not be affected, as they will still be rendered in the mode to which they would otherwise default. However, in IE9, the rendering mode of child iframes (which is what widgets are) is affected by the rendering mode of the parent page. Therefore, widgets that do not have a DOCTYPE, and which would expect to be rendered in quirks mode, will instead be rendered in standards mode in IE9. This may impact the appearance of some widgets. Note, this is an issue existing in IE9 and not OWF. 

This document assumes that the reader has a development background and is familiar with their chosen technology stack. The walkthrough found throughout this document will focus on building a simple HTML/JavaScript Web application deployed to a Java Application Server.

## 2   Walkthrough

This walkthrough explains the process of creating a simple Announcing Clock Widget using HTML and JavaScript, bundling the widget into a Web Application Archive ( **.war** ) file and deploying that **.war** file to a server. 

> _Note: All samples can be found in **\owf-sample-widgets.zip**._

**Step 1: Create the proper directory structure**

All Web applications use a standard hierarchy of subdirectories and special files. The root of the hierarchy defines the document root of the Web Application. In this walkthrough, the root directory will be the `webapp` directory. Accordingly, create a directory named `webapp`. (OWF ships with a `webapp` directory under `\src\main` in all the sample widget’s folders.) 

All files under the `webapp` directory can be served to the client, except for files under the special directory, `WEB-INF`. Under the `webapp` directory, create a directory named `WEB-INF`. The `WEB-INF` directory houses files that are integral to the running of the Web application, but are not directly accessible from a discrete URL. 

Next, create a new file called **web.xml** in the `WEB-INF` directory. The **web.xml** is the Web application deployment descriptor that configures the Web application.

Copy and paste the following code into the **web.xml** file: 

```xml
        <?xml version="1.0" encoding="UTF-8"?>
        <Web-app version="2.4" xmlns="http://java.sun.com/xml/ns/j2ee"
                xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                xsi:schemaLocation="http://java.sun.com/xml/ns/j2ee 
                http://java.sun.com/xml/ns/j2ee/Web-app_2_4.xsd">
                <display-name>Simple Announcing Clock Widget</display-name>
        </Web-app>
```

The directory structure should read as follows:

![Directory Structure](OWFImages/OWF7/directory_structure.png)

**Figure: Directory Structure**

**Step 2: Create the Simple Announcing Clock Widget**

OWF ships with sample file found in **AnnouncingClock.html** which is located in the OWF Sample Widgets bundle under the following directory: `html-widget.zip\src\main\webapp\clock`

To create the **AnnouncingClock.html** file in the `webapp` directory instead of using the sample that ships with OWF, copy and paste the following code into the **AnnouncingClock.html** file:

```html
        <html>
        <head>
        <script type="text/javascript">
        function updateClock ( )
        {
                var currentTime = new Date ( );
                var currentHours = currentTime.getHours ( );
                var currentMinutes = currentTime.getMinutes ( );
                var currentSeconds = currentTime.getSeconds ( );
        
                // Pad the minutes and seconds with leading zeros, if required
                currentMinutes = ( currentMinutes < 10 ? "0" : "" ) + currentMinutes;
                currentSeconds = ( currentSeconds < 10 ? "0" : "" ) + currentSeconds;
        
                // Choose either "AM" or "PM" as appropriate
                var timeOfDay = ( currentHours < 12 ) ? "AM" : "PM";
        
                // Convert the hours component to 12-hour format if needed
                currentHours = ( currentHours > 12 ) ? currentHours - 12 : currentHours;
        
                // Convert an hours component of "0" to "12"
                currentHours = ( currentHours == 0 ) ? 12 : currentHours;
        
                // Compose the string for display
                var currentTimeString = currentHours + ":" + currentMinutes + ":" + currentSeconds + " " + timeOfDay;
        
                // Update the time display
                document.getElementById("clock").firstChild.nodeValue = currentTimeString; }
        </script>	
        </head>
        <body onload="updateClock(); setInterval('updateClock()', 1000 )">
          The time is: <span id='clock'>&nbsp</span>
        </body>
        </html>
```

With the addition of the .html file, the directory structure should now read as follows:

![Directory Structure with AnnouncingClock.html File](OWFImages/OWF7/directory_structure_with_announcing_clock_file.png?raw=true)

**Figure: Directory Structure with AnnouncingClock.html File**

When opened in a browser, the Announcing Clock Widget should look similar to the Figure: Simple Announcing Clock Widget, shown below.

> _Note: Use URL_ **http(s)://servername.port/DIRECTORY_FROM_STEP_2/announcing-clock/AnnouncingClock.html**.

![Simple Announcing Clock Widget](OWFImages/OWF7/simple_announcing_clock_widget.png?raw=true)

**Figure: Simple Announcing Clock Widget**

**Step 3: Create a .war file**

A **.war** file is a Web application compressed into a single file. While directories and files can be copied directly onto the Web server, it is easier and more common to use a **.war** file.

To create the **.war** file for the Announcing Clock Widget, open a command prompt and navigate to the `\webapp` directory created in the **Walkthrough** section of this page. From the directory, the following command should be run:

        jar cvf announcing-clock.war .

> _Note: The command path must contain a JDK bin folder. For example:_ `path=C:\Program Files\Java\jdk1.6.0_18\bin;%PATH%` 

**Step 4: Deploy the .war file to the Server**

The deployment method used depends on the Web application server. For the prepackaged OWF Tomcat server, the process is as simple as copying the **.war** file into the `apache-tomcat-7.0.21\webapps` directory on the Web application server. In the event that a particular application server has different requirements, the appropriate Java application server documentation should be consulted for information on how the **.war** file should be deployed. 

> _Note: To create a sample widget using Jetty, an additional context file needs to be added to the `\jetty-6.1.11\contexts` folder. For this clock example, create a **clock-context.xml** with the following data:_

```xml
        <?xml version="1.0"  encoding="ISO-8859-1"?>
        <!DOCTYPE Configure PUBLIC "-//Mort Bay Consulting//DTD Configure//EN" "http://jetty.mortbay.org/configure.dtd">
        <Configure class="org.mortbay.jetty.webapp.WebAppContext">
            <Set name="contextPath">/announcing-clock</Set>
            <Set name="war">
            <SystemProperty name="jetty.home" default="."/>/webapps/AnnouncingClock.war</Set>
        </Configure>
```

#3   Additional Considerations

##Utility JS API

The JavaScript Utility API is provided to allow the widget developer to determine whether or not the widget is running inside OWF. This is useful if the widget needs to render differently or have different defaults depending on whether or not it is running internal or external to OWF. For instance, if a widget is supposed to turn on logging when running inside OWF, the widget developer can use the JavaScript Utility API to determine this.

> _Note: In some previous versions of OWF, a widget launched outside of OWF would spawn an error in an alert window. Now, a widget can be launched and used outside OWF. And while certain features, both specific and critical to OWF, such as the launch of security alert windows, widget preferences, and widget eventing, will not operate outside OWF, the error alert window will not launch, provided the widget URL is NOT appended with `owf=true`. Moreover, APIs can often throw exceptions which can make a widget fail to load._

While originally defined in `js\util\widget_utils.js`, the interface object now resides within the `Ozone.util` namespace. The entire namespace has been included in the OWF Widget JS bundles (both debug and min) for convenience. 

<b>Table: OWF.Util JSDoc entry</b>

<table border="1">
  <tr>
    <th>Namespace</th> 
    <th> Summary</th>
  </tr>
  <tr>
    <td>OWF.Util</td>
    <td>Provides OWF utility methods for widget developers</td>
  </tr>
<tr>
    <th>Method</th>
    <th>Summary</th>
</tr>
  <tr>
    <td>OWF.Util.cloneDashboard()</td>
    <td>Clones dashboard and returns a dashboard cfg object that can be used to create new dashboards.</td>
  </tr>
  <tr>
    <td>OWF.Util.getFlashApp(id)</td>
    <td>This method returns flash/flex dom element from dom.</td>
  </tr>
  <tr>
    <td>OWF.Util.guid()</td>
    <td>Returns a globally unique identifier (guid).</td>
  </tr>
 <tr>
    <td>OWF.Util.isInContainer()</td>
    <td>This method informs a widget developer if their widget is running in a Container, like OWF.</td>
  </tr>
 <tr>
    <td>OWF.Util.isRunningInOWF()</td>
    <td>This method informs a widget developer if their widget is running from the OWF or from a direct URL call.</td>
  </tr>
</table>

##Widget Best Practices

Due to the complexity of the OWF APIs, a widget’s ability to signal that it is ready to communicate with other widgets provides a helpful tool for developers. This ready signal is typically sent after the widget has subscribed to channels, registered RPC functions and Intents, etc. Starting with OWF 6, there is a standard way for widgets to signal this ready status.

In order to signal that it is ready, a widget calls `OWF.notifyWidgetReady()` after it is finished setting up any communication mechanisms. The OWF Development Team recommends that any widget that uses OWF APIs makes the call. However, widgets that use the [Widget Intents API](OWF-7-Developer-Widget-Intents-API)’s receive method must make this call. 

##OWF Bundled JavaScript

All required OWF JavaScript is now minified and bundled into one JavaScript file, found in `apache-tomcat-7.0.21\webapps\owf.war\js-min`. This will shield widget developers from future changes or upgrades to the underlying JavaScript files. This file can be included in a local **.war** file and referenced from a relative URL, helping make widgets less dependent on a specific instance of OWF. In the absence of said **.war** file, the minified bundle may be included from the location below: 

```javascript
    <script type="text/javascript" src="https://servername:port/owf/js-min/owf-widget-min.js"></script>
```

###Debug Version of the OWF Bundled JavaScript

A debug version of OWF Bundled JavaScript is also provided. Developers can find **owf-widget-debug.js** and **owf-widget-min.js** in `apache-tomcat-7.0.21\webapps\owf.war\js-min`. The files are not minified and are useful for debugging. The version of OWF Bundled JavaScript may be included from the location below:

```javascript
        <script type="text/javascript" src="https://servername:port/owf/js-min/owf-widget-debug.js"></script>
```

> _Note: As a best practice, developers should include the file in the local **.war** file and referenced from a relative URL; this helps make the widget’s **.war** file less dependent on a specific OWF instance._

###Full Listing of JavaScript files

It is recommended that developers use the OWF bundled JavaScript file. However, to aid in development a full list of all JavaScript files included in the bundle is below:

```javascript
        <script type="text/javascript" src="https://servername:port/owf/js-lib/dojo-1.5.0-windowname-only/dojo/owfdojo.js.uncompressed.js "></script>
        <script type="text/javascript" src="https://servername:port/owf/js/util/pageload.js"></script>
        <script type="text/javascript" src="https://servername:port/owf/js/util/version.js"></script>
        <script type="text/javascript" src="https://servername:port/owf/js/util/util.js"></script>
        <script type="text/javascript" src="https://servername:port/owf/js/util/guid.js"></script>
        <script type="text/javascript" src="https://servername:port/owf/js/components/keys/HotKeys.js"></script>
        <script type="text/javascript" src="https://servername:port/owf/js/components/keys/KeyEventSender.js"></script>
        <script type="text/javascript" src="https://servername:port/owf/js/lang/ozone-lang.js"></script>
        <script type="text/javascript" src="https://servername:port/owf/js/lang/DateJs/globalization/en-US.js"></script>
        <script type="text/javascript" src="https://servername:port/owf/js/util/transport.js"></script>
        <script type="text/javascript" src="https://servername:port/owf/js/util/widget_utils.js"></script>
        <script type="text/javascript" src="https://servername:port/owf/js-lib/shindig/util.js"></script>
        <script type="text/javascript" src="https://servername:port/owf/js-lib/shindig/json.js"></script>
        <script type="text/javascript" src="https://servername:port/owf/js-lib/shindig/rpc.js"></script>
        <script type="text/javascript" src="https://servername:port/owf/js-lib/shindig/pubsub.js"></script>
        <script type="text/javascript" src="https://servername:port/owf/js-lib/log4javascript/log4javascript.js"></script>
        <script type="text/javascript" src="https://servername:port/owf/js/util/log.js"></script>
        <script type="text/javascript" src="https://servername:port/owf/js/pref/preference.js"></script>
        <script type="text/javascript" src="https://servername:port/owf/js/eventing/Widget.js"></script>
        <script type="text/javascript" src="https://servername:port/owf/js/intents/WidgetIntents.js"></script>
        <script type="text/javascript" src="https://servername:port/owf/js/chrome/WidgetChrome.js"></script>
        <script type="text/javascript" src="https://servername:port/owf/js/dd/WidgetDragAndDrop.js"></script>
        <script type="text/javascript" src="https://servername:port/owf/js/launcher/WidgetLauncher.js"></script>
        <script type="text/javascript" src="https://servername:port/owf/js/state/WidgetStateHandler.js"></script>
        <script type="text/javascript" src="https://servername:port/owf/js/state/WidgetState.js"></script>
        <script type="text/javascript" src="https://servername:port/owf/js/eventing/WidgetProxy.js"></script>
        <script type="text/javascript" src="https://servername:port/owf/js/kernel/kernel-client.js"></script>
        <script type="text/javascript" src="https://servername:port/owf/js/metrics/BaseMetrics.js"></script>
        <script type="text/javascript" src="https://servername:port/owf/js/widget/Widget.js"></script>
        <script type="text/javascript" src="https://servername:port/owf/js/widget/widgetInit.js"></script>
```

Replace all occurrences of `https://servername:port` with the name of the server where OWF is running, for example, `https://www.yourcompany.com:8443`. 

##OWF Bundled JavaScript and Dojo

The OWF bundled JavaScript file includes a custom build of the Dojo JavaScript Toolkit. This custom build of Dojo remaps `dojo` to `owfdojo`. This allows widget developers to include their own version of Dojo using the default `dojo` namespace. In addition, if Dojo from the previous OWF bundled JavaScript file is in use, `owfdojo` must be used or a custom version of Dojo must be imported. 