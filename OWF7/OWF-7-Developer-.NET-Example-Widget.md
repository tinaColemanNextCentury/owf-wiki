##   .NET Example

The .NET sample widget demonstrates how a simple .NET-based Web application can be integrated into OWF. It consists of a Web page for adding eventing channels and a Web service for storing received messages.

#1   Technologies

The following is required to build/deploy this example:
* Visual Studio 2008
* ASP.Net 3.5 or higher.
* Microsoft IIS or the built-in Web server bundled in Visual Studio 2008

#2   Building/Compilation

This example is packaged as a Visual Studio solution (*.sln). 

1. Open the solution file and use Visual Studio to run and debug the application. By default, it will try to pick up OWF scripts on localhost. 
2. Change the location of the source to reflect the actual location of the OWF server. Accordingly the location of the source must be modified in the **Default.aspx** file to reflect the actual location of the OWF server: 
```html
        <script type="text/javascript" src="https://localhost:8443/owf/js/config/config.js"></script>
        <script type="text/javascript" src="https://localhost:8443/owf/js/util/error.js"></script>
        <script type="text/javascript" language="javascript" src="https://localhost:8443/owf/js-min/owf-widget-min.js"></script>
```
3. Replace all occurrences of `https://servername:port` with the name of the server where OWF is running, for example, `https://www.yourcompany.com:8443`. Additionally, be sure to verify that the windowname library paths point to the local installation.

To test that the widget works properly: 

1. Follow the walkthrough on the [Adding a Widget to OWF](OWF-7-Developer—Adding-a-Widget-to-OWF) page to create widget definitions which point to **Default.aspx**, assign the widget to a user, and then apply the widget to one of the user’s dashboards. Use the following data for widget definitions:

  **Table: Data for .NET Widget Definition**
 <table>
    <tr>
        <th>Definition</th>
        <th>Data Input Field</th>
    </tr>
    <tr>
        <td>URL</td>
        <td>http://widget-server-name:port/StockWatcher/StockWatcher.html</td>
    </tr>
    <tr>
        <td>Large Icon</td>
        <td>http://localhost:80/dotnet/images/channelListener.gif</td>
    </tr>
    <tr>
        <td>Small Icon</td>
        <td>http://localhost:80/dotnet/images/channelListenersm.gif</td>
    </tr>
    <tr>
        <td>Width</td>
        <td>500</td>
    </tr>
    <tr>
        <td>Height</td>
        <td>500</td>
    </tr>
 </table>

2. Enter the OWF and select the dashboard that contains the widget mentioned in the steps above.
3. Launch the Channel Shouter Widget and the **Default.aspx** widget mentioned above.
4. Assign a channel to the Shouter and add it to the **Default.aspx** widget. 
5. Broadcast a message with the Shouter, then search for a word from said message with the **Default.aspx** widget. The message should appear in the search results of **Default.aspx**.

#3   Known Issues

When a .NET widget is added to a dashboard which is being viewed in Internet Explorer, a debug message which reads "Failed Target Prefs Error: Timeout", is displayed. The OWF team is aware of this issue and will be addressing it in a future release.