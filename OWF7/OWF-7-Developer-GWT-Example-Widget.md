#  GWT Example

The GWT sample demonstrates how a Google Web Toolkit widget can be integrated in OWF. The standard [GWT stockwatcher tutorial application](https://developers.google.com/web-toolkit/doc/latest/tutorial/gettingstarted) has been modified so that it can perform the following:

* When adding and removing stocks, it will broadcast a message on the **stockwatcher** channel.
* Persist all the current stocks into one User Preference named `STOCK_LIST`.
* On initial load, retrieve User Preference named `STOCK_LIST` if available for user and load symbols into grid.

#1   Technologies

* A Java JDK installation of 1.6 or higher.
* GWT 1.6 (tested with GWT 1.6.4.).
* Apache ANT 1.7 or higher OR the latest version of Eclipse with the GWT toolkit plugin.
* A J2EE container such as Tomcat, Jetty or JBoss.

#2   Building/Compilation

In order to build the GWT sample widget, execute the following steps:

1. Extract **/gwt-widget.zip** into a new directory.
2. Ensure that the Environment Variable `GWT_HOME` is set to the correct location — the installation of GWT.
3. Open a command prompt and navigate to the directory created in Step 1.
4. Modify the location of the source in the **StockWatcher.html** file to reflect the actual location of the OWF server:

```html
        <script type="text/javascript" language="javascript" src="https://localhost:8443/owf/js-min/owf-widget-debug.js"></script>
```

 > _Note: Directions on how to add an environment variable for Windows XP at [http://support.microsoft.com/kb/310519](http://support.microsoft.com/kb/310519)._

5. Type ANT. The resulting **StockWatcher.war** file will be in the target directory and can be deployed to the widget server.
6. By default, the widget looks for the framework JavaScripts on localhost. Replace all occurrences of `https://servername:port` with the name of the server where OWF is running, for example, `https://www.yourcompany.com:8443`. 

To test that the widget properly publishes data, do the following:

1. Follow the walkthrough on the [Adding a Widget to OWF](OWF-7-Developer-Adding-a-Widget-to-OWF) page to create widget definitions which point to **stockwatcher.html**, assign the widget to a user and then apply the widget to one of the user’s dashboards. Use the following data for widget definitions:

  **Table: Data for GWT Widget Definition**

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
    <td>http://widget-server-name:port/StockWatcher/images/stockwatch.gif</td>
  </tr>
  <tr>
    <td>Small Icon</td>
    <td>http://widget-server-name:port/StockWatcher/images/stockwatchsm.gif</td>
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

2. Enter the OWF and select the dashboard which contains the widgets mentioned in the steps above.
3. Launch the Listener Widget and the StockWatcher .NET Widget.
4. Add the **stockwatcher** channel to the Listener Widget.
5. When stocks are added or removed from the widget, the listener will display the appropriate information. 

#3   Known Issues

There are no known issues at this time.