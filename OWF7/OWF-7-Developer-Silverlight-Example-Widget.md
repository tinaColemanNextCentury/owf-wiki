#   Silverlight Example

The Silverlight example shows how an ASP.Net/Silverlight website can be incorporated into OWF as a widget. It consists of four panes that are accessible via the menu at the bottom of the widget:

* The first pane contains a shouter that allows the sending of messages to other widgets within the framework.
* The second is a listener that can register eventing channels to listen on, which also keeps a running record of all messages received.
* The third pane uses Silverlight charting to track the frequency of the messages within the registered channels.
* The fourth pane uses the Preference Server API to store the user’s preferred visualization method for the third pane (pie chart or bar chart).

#1   Technologies

The following is required to build/deploy this example:

* Visual Studio 2008 SP1
* ASP.Net 3.5 or higher
* Silverlight 2 Toolkit
* Microsoft IIS or the built-in Web server bundled in Visual Studio 2008

> _Note: This example was built using the Silverlight 2 Toolkit released July 2009. Earlier versions may not have all the necessary references and thus, additional configurations may be needed for the widget to run._

#2   Building/Compilation

The Silverlight example is packaged as a Visual Studio solution (\* **.sln**) and, as per Microsoft-suggested practice, consists of two projects (\* **.prj**). One contains the Website and the other is the Silverlight code. 

1. Open the solution file and use Visual Studio to run and debug the application. By default, it will try to pick up OWF scripts on localhost.
2. Change the **OWFSilverlightDemoTestPage.aspx** and the **OWFSilverlightDemoTestPage.html** files to reflect the local OWF server: 

```html
        <script type="text/javascript" language="javascript" src="https://localhost:8443/owf/js-min/owf-widget-min.js"></script>
```

3. Replace all occurrences of `https://servername:port` with the name of the server where OWF is running, for example, `https://www.yourcompany.com:8443`. Additionally, be sure to verify that the windowname library paths point to the local installation.

#3   Known Issues
The Silverlight example uses components from the freely available **SilverlightContrib.DLLs**. A copy of the library is bundled with the example.

In Windows, browsers can display a browser-hosted Silverlight content area in either a windowed mode or a windowless mode. The default is a windowed mode. This property can be set only as an initialization parameter and is read-only for all other access models. In windowless mode, the Silverlight plugin does not have its own rendering window. Instead, the plugin content is displayed directly by the browser window. This enables Silverlight content to visually overlap and blend with HTML content if the plugin and its content both specify background transparency. HTML content can also be displayed on top of Silverlight content in windowless mode. If a Silverlight widget is still rendering incorrectly, please see the **Widget Technology Issues** section (of the [Known Issues](OWF-7-Developer—Known-Issues) page) for more details. In Macintosh environments, there is no windowed mode. The mode is always windowless regardless of the Windowless setting.