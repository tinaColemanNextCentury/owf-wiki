# JavaScript API Reference Document

The following is a summary of the OWF JavaScript APIs. Additional information on each API is found in the JavaScript document located in the OWF Help Bundle.

[OWF]
[OWF.Chrome]
[OWF.DragAndDrop]
[OWF.Eventing]
[OWF.Intents]
[OWF.Lang]
[OWF.Launcher]
[OWF.Log]
[OWF.Metrics]
[OWF.Preferences]
[OWF.RPC]
[OWF.Util]

[Ozone.chrome.WidgetChrome]
[Ozone.dragAndDrop.WidgetDragandDrop]
[Ozone.eventing.Widget]
[Ozone.eventing.WidgetProxy]
[Ozone.lang]
[Ozone.launcher.WidgetLauncher]
[Ozone.launcher.WidgetLauncherUtils]
[Ozone.log]
[Ozone.metrics]
[Ozone.pref.PrefServer]
[Ozone.state.WidgetState]
[Ozone.state.WidgetStateHandler]
[Ozone.util]
[Ozone.util.pageLoad]


### Namespace: `OWF`
<i>Defined in:</i> `Widget.js`

<table>
    <tr>
        <th>Namespace Summary</th>
        <th></th>
    </tr>
    <tr>
        <td><b>OWF</b></td>
        <td></td>
    </tr>
     <tr>
         <th>Field Summary</th>
         <th></th>
    </tr>
    <tr>
          <td><b>OWF.relayFile</b></td>
          <td>The location of the widget relay file.</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td><b>OWF.getContainerName()</b></td>
          <td>Returns the name of the Container the Widget is in.</td>
    </tr>
    <tr>
          <td><b>OWF.getContainerUrl()</b></td>
          <td>Returns the URL of the Container the Widget is in.</td>
    </tr>
    <tr>
          <td><b>OWF.getContainerVersion()</b></td>
          <td>Returns the version of the Container the Widget is in.</td>
    </tr>
        <tr>
          <td><b>OWF.getCurrentTheme()</b></td>
          <td>Returns an object containing information on the current OWF theme.</td>
    </tr>
    <tr>
          <td><b>OWF.getDashboardLayout()</b></td>
          <td>Returns type of dashboard in which the widget is opened.</td>
    </tr>
    <tr>
          <td><b>OWF.getIframeId()</b></td>
          <td>Returns the Widget Id.</td>
    </tr>
        <tr>
          <td><b>OWF.getInstanceId()</b></td>
          <td>Returns instance GUID of the widget.</td>
    </tr>
    <tr>
          <td><b>OWF.getOpenedWidgets(callback)</b></td>
          <td>Gets all opened widgets on the current dashboard.</td>
    </tr>
    <tr>
          <td><b>OWF.getUrl()</b></td>
          <td>Returns URL of the widget.</td>
    </tr>
        <tr>
          <td><b>OWF.getVersion()</b></td>
          <td>Returns version of the widget.</td>
    </tr>
    <tr>
          <td><b>OWF.getWidgetGuid()</b></td>
          <td>Returns definition GUID of the widget.</td>
    </tr>
    <tr>
          <td><b>OWF.isDashboardLocked()</b></td>
          <td>Returns whether or not the dashboard in which the widget is opened is locked.</td>
    </tr>
        <tr>
          <td><b>OWF.notifyWidgetReady()</b></td>
          <td>This function should be called once the widget is ready and all initialization is completed.</td>
    </tr>
    <tr>
          <td><b>OWF.ready(handler, scope)</b></td>
          <td>Accepts a function that is executed when Ozone APIs are ready for use.</td>
    </tr>
</table>

### Namespace: `OWF.Chrome`
<i>Defined in:</i> `Widget.js`

<table>
    <tr>
        <th>Namespace Summary</th>
        <th></th>
    </tr>
    <tr>
        <td>OWF.Chrome</td>
        <td>This object allows a widget to modify the button contained in the widget header (the chrome).</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td><b>OWF.Chrome.addHeaderButtons(cfg)</b></td>
          <td>Adds buttons to the Widget Chrome.</td>
    </tr>
    <tr>
          <td><b>OWF.Chrome.addHeaderMenus(cfg)</b></td>
          <td>Adds menus to the Widget Chrome.</td>
    </tr>
    <tr>
          <td><b>OWF.Chrome.getTitle(cfg)</b></td>
          <td>Gets the Widget's Title from the Chrome.</td>
    </tr>
        <tr>
          <td><b>OWF.Chrome.insertHeaderButtons(cfg)</b></td>
          <td>Inserts new buttons to the Widget Chrome.</td>
    </tr>
    <tr>
          <td><b>OWF.Chrome.insertHeaderMenus(cfg)</b></td>
          <td>Inserts new menus into the Widget Chrome.</td>
    </tr>
        <tr>
          <td><b>OWF.Chrome.isModified(cfg)</b></td>
          <td>Checks to see if the Widget Chrome has already been modified.</td>
    </tr>
    <tr>
          <td><b>OWF.Chrome.listHeaderButtons(cfg)</b></td>
          <td>Lists all buttons that have been added to the widget chrome.</td>
    </tr>
        <tr>
          <td><b>OWF.Chrome.listHeaderMenus(cfg)</b></td>
          <td>Lists all menus that have been added to the widget chrome.</td>
    </tr>
    <tr>
          <td><b>OWF.Chrome.removeHeaderButtons(cfg)</b></td>
          <td>Removes existing buttons on the Widget Chrome based on itemId.</td>
    </tr>
        <tr>
          <td><b>OWF.Chrome.removeHeaderMenus(cfg)</b></td>
          <td>Removes existing menus on the Widget Chrome based on itemId.</td>
    </tr>
    <tr>
          <td><b>OWF.Chrome.setTitle(cfg)</b></td>
          <td>Sets the Widget's Title in the Chrome.</td>
    </tr>
        <tr>
          <td><b>OWF.Chrome.updateHeaderButtons(cfg)/<b></td>
          <td>Updates any existing buttons in the Widget Chrome based on the itemId.</td>
    </tr>
    <tr>
          <td><b>OWF.Chrome.updateHeaderMenus(cfg)</b></td>
          <td>Updates any existing menus in the Widget Chrome based on the itemId.</td>
    </tr>
</table>

### Namespace: `OWF.DragAndDrop`
<i>Defined in:</i> `Widget.js`

<table>
    <tr>
        <th>Namespace Summary</th>
        <th></th>
    </tr>
    <tr>
        <td><b>OWF.DragAndDrop</b></td>
        <td>The OWF.DragAndDrop object manages the drag and drop for an individual widget.</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td><b>OWF.DragAndDrop.addDropZoneHandler(cfg)</b></td>
          <td>Adds a new drop zone to be managed.</td>
    </tr>
    <tr>
          <td><b>OWF.DragAndDrop.getDragStartData()</b></td>
          <td>Returns data sent when a drag was started</td>
    </tr>
    <tr>
          <td><b>OWF.DragAndDrop.getDropEnabled()</b></td>
          <td>Returns whether the a drop is enabled (this is only true when the mouse is over a drop zone)</td>
    </tr>
        <tr>
          <td><b>OWF.DragAndDrop.isDragging()</b></td>
          <td>Returns whether a drag is in progress.</td>
    </tr>
    <tr>
          <td><b>OWF.DragAndDrop.onDragStart(callback, scope)</b></td>
          <td>Executes the callback passed when a drag starts in any widget.</td>
    </tr>
        <tr>
          <td><b>OWF.DragAndDrop.onDragStop(callback, scope)</b></td>
          <td>Executes the callback passed when a drag stops in any widget.</td>
    </tr>
    <tr>
          <td><b>OWF.DragAndDrop.onDrop(callback, scope)</b></td>
          <td>Executes the callback passed when a drop occurs in the widget.</td>
    </tr>
        <tr>
          <td><b>OWF.DragAndDrop.setDropEnabled(dropEnabled)</b></td>
          <td>Toggles the dragIndicator to indicate successful or unsuccessful drop</td>
    </tr>
    <tr>
          <td><b>OWF.DragAndDrop.setFlashWidgetId(id)</b></td>
          <td>Use this method to set flex dom element id, so that drag and drop can be enabled in flex widgets.</td>
    </tr>
        <tr>
          <td><b>OWF.DragAndDrop.startDrag(cfg)</b></td>
          <td>Starts a drag.</td>
    </tr>
</table>

### Namespace: `OWF.Eventing`
<i>Defined in:</i> `Widget.js`

<table>
    <tr>
        <th>Namespace Summary</th>
        <th></th>
    </tr>
    <tr>
        <td><b>OWF.Eventing</b></td>
        <td>The OWF.Eventing object manages the eventing for an individual widget.</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td><b>OWF.Eventing.publish(channelName, message, dest)</b></td>
          <td>Publishes a message to a given channel.</td>
    </tr>
    <tr>
          <td><b>OWF.Eventing.subscribe(channelName, handler)</b></td>
          <td>Subscribe to a named channel for a given function.</td>
    </tr>
    <tr>
          <td><b>OWF.Eventing.unsubscribe(channelName)</b></td>
          <td>Unsubscribe to a named channel.</td>
    </tr>
</table>

### Namespace: `OWF.Intents`
<i>Defined in:</i> `WidgetIntents.js`

<table>
    <tr>
        <th>Namespace Summary</th>
        <th></th>
    </tr>
    <tr>
        <td><b>OWF.Intents</b></td>
        <td></td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td><b>OWF.Intents.receive(intent, handler)</b></td>
          <td>Register to receive an Intent</td>
    </tr>
    <tr>
          <td><b>OWF.Intents.startActivity(intent, data, handler, dest)</b></td>
          <td>Starts an Intent.</td>
    </tr>
</table>

### Namespace: `OWF.Lang`
<i>Defined in:</i> `Widget.js`

<table>
    <tr>
        <th>Namespace Summary</th>
        <th></th>
    </tr>
    <tr>
        <td><b>OWF.Lang</b></td>
        <td>Provides utility methods for localization.</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td><b>OWF.Lang.getLanguage()</b></td>
          <td>Gets the language that is currently being used by OWF.</td>
    </tr>
</table>

### Namespace: `OWF.Launcher`
<i>Defined in:</i> `Widget.js`

<table>
    <tr>
        <th>Namespace Summary</th>
        <th></th>
    </tr>
    <tr>
        <td><b>OWF.Launcher</b></td>
        <td>This object is used launch other widgets.</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td><b>OWF.Launcher.getLaunchData()</b></td>
          <td>Retrieves initial launch data for this widget if it is opened by another widget.</td>
    </tr>
    <tr>
          <td><b>OWF.Launcher.launch(config, callback)</b></td>
          <td>Launches a Widget based on the config.</td>
    </tr>
</table>

### Namespace: `OWF.Log`
<i>Defined in:</i> `Widget.js`

<table>
    <tr>
        <th>Namespace Summary</th>
        <th></th>
    </tr>
    <tr>
        <td><b>OWF.Log</b></td>
        <td>Provides functions to log messages and objects.</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td><b>OWF.Log.getDefaultLogger()</b></td>
          <td>Get OWF's default logger.</td>
    </tr>
    <tr>
          <td><b>OWF.Log.getLogger(loggerName)</b></td>
          <td>Get a logger by name, if the logger has not already been created it will be created.</td>
    </tr>
    <tr>
          <td><b>OWF.Log.launchPopupAppender()</b></td>
          <td>Launch the log window pop-up, this will re-launch the window in the event it has been closed.</td>
    </tr>
        <tr>
          <td><b>OWF.Log.setEnabled(enabled)</b></td>
          <td>Enable/Disable logging for the OWF application.</td>
    </tr>
</table>

### Namespace: `OWF.Metrics`
<i>Defined in:</i> `Widget.js`

<table>
    <tr>
        <th>Namespace Summary</th>
        <th></th>
    </tr>
    <tr>
        <td><b>OWF.Metrics</b></td>
        <td></td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td><b>OWF.Metrics.logBatchMetrics(metrics)</b></td>
          <td>Logs a set of metrics to the server all at once.</td>
    </tr>
    <tr>
          <td><b>OWF.Metrics.logMetric(userId, userName, metricSite, componentName, componentId, componentInstanceId, metricTypeId, metricData)</b></td>
          <td>Basic logging capability - meant to be called by other methods which transform or validate data.</td>
    </tr>
    <tr>
          <td><b>OWF.Metrics.logWidgetRender(userId, userName, metricSite, widget)</b></td>
          <td>Log view of widget - see calls in dashboards.</td>
    </tr>
</table>

### Namespace: `OWF.Preferences`
<i>Defined in:</i> `Widget.js`

<table>
    <tr>
        <th>Namespace Summary</th>
        <th></th>
    </tr>
    <tr>
        <td><b>OWF.Preferences</b></td>
        <td>This object is used to create, retrieve, update and delete user preferences.</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td><b>OWF.Preferences.cloneDashboard(cfg)</b></td>
          <td>Copies an existing dashboard and saves it as new.</td>
    </tr>
    <tr>
          <td><b>OWF.Preferences.createOrUpdateDashboard(cfg)</b></td>
          <td>Saves changes to a new or existing dashboard.</td>
    </tr>
    <tr>
          <td><b>OWF.Preferences.deleteDashboard(cfg)</b></td>
          <td>Deletes the dashboard with the specified id.</td>
    </tr>
        <tr>
          <td><b>OWF.Preferences.deleteUserPreference(cfg)</b></td>
          <td>Deletes a user preference with the provided namespace and name.</td>
    </tr>
        <tr>
          <td><b>OWF.Preferences.doesUserPreferenceExist(cfg)</b></td>
          <td>Checks for the existence of a user preference for a given namespace and name.</td>
    </tr>
        <tr>
          <td><b>OWF.Preferences.findDashboards(cfg)</b></td>
          <td>Returns all dashboards for the logged in user.</td>
    </tr>
        <tr>
          <td><b>OWF.Preferences.findDashboardsByType(cfg)</b></td>
          <td>Returns all dashboards for the logged in user filtered by the type of dashboard.</td>
    </tr>
        <tr>
          <td><b>OWF.Preferences.findWidgets(cfg)</b></td>
          <td>Gets all widgets for a given user.</td>
    </tr>
        <tr>
          <td><b>OWF.Preferences.getCurrentUser(cfg)</b></td>
          <td>Retrieves the current user logged into the system.</td>
    </tr>
        <tr>
          <td><b>OWF.Preferences.getDashboard(cfg)</b></td>
          <td>Gets the dashboard with the specified id.</td>
    </tr>
        <tr>
          <td><b>OWF.Preferences.getDefaultDashboard(cfg)</b></td>
          <td>Gets the user's default dashboard.</td>
    </tr>
        <tr>
          <td><b>OWF.Preferences.getServerVersion(cfg)</b></td>
          <td>For retrieving the OWF system server version.</td>
    </tr>
        <tr>
          <td><b>OWF.Preferences.getUrl()</b></td>
          <td>Get the url for the Preference Server.</td>
    </tr>
        <tr>
          <td><b>OWF.Preferences.getUserPreference(cfg)</b></td>
          <td>Retrieves the user preference for the provided name and namespace.</td>
    </tr>
        <tr>
          <td><b>OWF.Preferences.getWidget(cfg)</b></td>
          <td>Gets the widget with the specified id.</td>
    </tr>
        <tr>
          <td><b>OWF.Preferences.setDefaultDashboard(cfg)</b></td>
          <td>Sets the user's default dashboard.</td>
    </tr>
        <tr>
          <td><b>OWF.Preferences.setUrl(url)</b></td>
          <td>Sets the url for the Preference Server.</td>
    </tr>
        <tr>
          <td><b>OWF.Preferences.setUserPreference(cfg)</b></td>
          <td>Creates or updates a user preference for the provided namespace and name.</td>
    </tr>
        <tr>
          <td><b>OWF.Preferences.updateAndDeleteDashboards(cfg)</b></td>
          <td>Saves changes to existing dashboards.</td>
    </tr>
        <tr>
          <td><b>OWF.Preferences.updateAndDeleteWidgets(cfg)</b></td>
          <td>Saves changes to existing widgets.</td>
    </tr>
</table>

### Namespace: `OWF.RPC`
<i>Defined in:</i> `Widget.js`

<table>
    <tr>
        <th>Namespace Summary</th>
        <th></th>
    </tr>
    <tr>
        <td><b>OWF.RPC</b></td>
        <td></td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td><b>OWF.RPC.getWidgetProxy(instanceGuid, callback)</b></td>
          <td>Gets a proxy object that contains methods exposed by other widget.</td>
    </tr>
    <tr>
          <td><b>OWF.RPC.handleDirectMessage(fn)</b></td>
          <td>Register a function to be executed when a direct message is received from another widget.</td>
    </tr>
    <tr>
          <td><b>OWF.RPC.registerFunctions(objs)</b></td>
          <td>Register one or more functions to OWF to expose to other widgets.</td>
    </tr>
</table>

### Namespace: `OWF.Util`
Defined in: `Widget.js`

<table>
    <tr>
        <th>Namespace Summary</th>
        <th></th>
    </tr>
    <tr>
        <td>OWF.Util</td>
        <td>Provides OWF utility methods for the widget developer</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td><b>OWF.Util.cloneDashboard()</b></td>
          <td>Clones dashboard and returns a dashboard cfg object that can be used to create new dashboards.</td>
    </tr>
    <tr>
          <td><b>OWF.Util.getFlashApp(id)</b></td>
          <td>This method returns flash/flex dom element from dom.</td>
    </tr>
    <tr>
          <td><b>OWF.Util.guid()</b></td>
          <td>Returns a globally unique identifier (guid).</td>
    </tr>
        <tr>
          <td><b>OWF.Util.isInContainer()</b></td>
          <td>This method informs a widget developer if their widget is running in a Container, like OWF.</td>
    </tr>
    <tr>
          <td><b>OWF.Util.isRunningInOWF()</b></td>
          <td>This method informs a widget developer if their widget is running from the OWF or from a direct URL call.</td>
    </tr>
</table>

### CLass: `Ozone.chrome.WidgetChrome`
<i>Defined in:</i> `WidgetChrome.js`

<table>
    <tr>
        <th>Class Summary</th>
        <th></th>
    </tr>
    <tr>
        <td><b>Ozone.chrome.WidgetChrome(config)</b></td>
        <td>This object allows a widget to modify the button contained in the widget header (the chrome).</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td><b>addHeaderButtons(cfg)</b></td>
          <td>Adds buttons to the Widget Chrome.</td>
    </tr>
    <tr>
          <td><b>addHeaderMenus(cfg)</b></td>
          <td>Adds menus to the Widget Chrome.</td>
    </tr>
    <tr>
          <td><b>getInstance(config)</b></td>
          <td>Retrieves Ozone.chrome.WidgetChrome Singleton instance.</td>
    </tr>
        <tr>
          <td><b>getTitle(cfg)</b></td>
          <td>Gets the Widget's Title from the Chrome.</td>
    </tr>
    <tr>
          <td><b>insertHeaderButtons(cfg)</b></td>
          <td>Inserts new buttons to the Widget Chrome.</td>
    </tr>
    <tr>
          <td><b>insertHeaderMenus(cfg)</b></td>
          <td>Inserts new menus into the Widget Chrome.</td>
    </tr>
        <tr>
          <td><b>isModified(cfg)</b></td>
          <td>Checks to see if the Widget Chrome has already been modified.</td>
    </tr>
    <tr>
          <td><b>listHeaderButtons(cfg)</b></td>
          <td>Lists all buttons that have been added to the widget chrome.</td>
    </tr>
    <tr>
          <td><b>listHeaderMenus(cfg)</b></td>
          <td>Lists all menus that have been added to the widget chrome.</td>
    </tr>
        <tr>
          <td><b>removeHeaderButtons(cfg)</b></td>
          <td>Removes existing buttons on the Widget Chrome based on itemId.</td>
    </tr>
    <tr>
          <td><b>removeHeaderMenus(cfg)</b></td>
          <td>Removes existing menus on the Widget Chrome based on itemId.</td>
    </tr>
    <tr>
          <td><b>setTitle(cfg)</b></td>
          <td>Sets the Widget's Title in the Chrome</td>
    </tr>
        <tr>
          <td><b>updateHeaderButtons(cfg)</b></td>
          <td>Updates any existing buttons in the Widget Chrome based on the itemId.</td>
    </tr>
    <tr>
          <td><b>updateHeaderMenus(cfg)</b></td>
          <td>Updates any existing menus in the Widget Chrome based on the itemId.</td>
    </tr>
</table>

### Class: `Ozone.dragAndDrop.WidgetDragAndDrop`
<i>Defined in:</i> `WidgetDragAndDrop.js`

<table>
    <tr>
        <th>Class Summary</th>
        <th></th>
    </tr>
    <tr>
        <td><b>Ozone.dragAndDrop.WidgetDragAndDrop(cfg)</b></td>
        <td>The Ozone.dragAndDrop.WidgetDragAndDrop object manages the drag and drop for an individual widget.</td>
    </tr>
        <tr>
         <th>Field Summary</th>
         <th></th>
    </tr>
    <tr>
          <td><b>dragStart</b></td>
          <td>dragStart is the name of the event when a drag is started.</td>
    </tr>
        <tr>
          <td><b>dragStop</b></td>
          <td>dragStop is the name of the event when a drag is stopped.</td>
    </tr>
        <tr>
          <td><b>dropReceive</b></td>
          <td>dropReceive is the name of the event when a drop occurs on this widget.</td>
    </tr>
        <tr>
          <td><b>version</b></td>
          <td>version number</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td><b>addCallback(eventName, cb)</b></td>
          <td>Adds a function as a callback to Drag and Drop events.</td>
    </tr>
    <tr>
          <td><b>addDropZoneHandler(cfg)</b></td>
          <td>Adds a new drop zone to be managed.</td>
    </tr>
    <tr>
          <td><b>doStartDrag(cfg)</b></td>
          <td>Starts a drag.</td>
    </tr>
        <tr>
          <td><b>getDragStartData()</b></td>
          <td>Returns data sent when a drag was started.</td>
    </tr>
    <tr>
          <td><b>getDropEnabled()</b></td>
          <td>Returns whether the a drop is enabled (this is only true when the mouse is over a drop zone).</td>
    </tr>
    <tr>
          <td><b>getInstance(cfg)</b></td>
          <td>Retrieves Ozone.dragAndDrop.WidgetDragAndDrop Singleton instance.</td>
    </tr>
        <tr>
          <td><b>init(cfg)</b></td>
          <td>Initializes the WidgetDragAndDrop object.</td>
    </tr>
    <tr>
          <td><b>isDragging()</b></td>
          <td>Returns whether a drag is in progress.</td>
    </tr>
    <tr>
          <td><b>setDropEnabled(dropEnabled)</b></td>
          <td>Toggles the dragIndicator to indicate successful or unsuccessful drop.</td>
    </tr>
</table>

### Class: `Ozone.eventing.Widget`
<i>Defined in:</i> `Widget.js`

<table>
    <tr>
        <th>Class Summary</th>
        <th></th>
    </tr>
    <tr>
        <td><b>Ozone.eventing.Widget(widgetRelay, afterInit)</b></td>
        <td>The Ozone.eventing.Widget object manages the eventing for an individual widget (Deprecated).</td>
    </tr>
        <tr>
         <th>Field Summary</th>
         <th></th>
    </tr>
    <tr>
          <td><b>Ozone.eventing.Widget.widgetRelayURL</b></td>
          <td>The location of the widget relay file.</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td><b>getInstance(afterInit, widgetRelay)</b></td>
          <td>Retrieves Ozone.eventing.Widget Singleton instance.</td>
    </tr>
    <tr>
          <td><b>getWidgetId()</b></td>
          <td>Returns the Widget Id.</td>
    </tr>
    <tr>
          <td><b>publish(channelName, message, dest, accessLevel)</b></td>
          <td>Publish a message to a given channel.</td>
    </tr>
        <tr>
          <td><b>subscribe(channelName, handler)</b></td>
          <td>Subscribe to a named channel for a given function.</td>
    </tr>
        <tr>
          <td><b>unsubscribe(channelName)</b></td>
          <td>Unsubscribe to a named channel.</td>
    </tr>
</table>

### Class: `Ozone.eventing.WidgetProxy`
<i>Defined in:</i> `WidgetProxy.js`

<table>
    <tr>
        <th>Class Summary</th>
        <th></th>
    </tr>
    <tr>
        <td><b>Ozone.eventing.WidgetProxy(wid, functions, srcId, proxy)</b></td>
        <td>Creates or updates a proxy - This is a private constructor - Do not call this directly.</td>
    </tr>
        <tr>
         <th>Field Summary</th>
         <th></th>
    </tr>
    <tr>
          <td><b>id</b></td>
          <td>Id of the Widget that this proxy represents.</td>
    </tr>
        <tr>
          <td><b>isReady</b></td>
          <td>Flag which represents if the Widget this proxy represents.</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td><b>onReady(readyListener, readyListenerScope)</b></td>
          <td>Registers a listener function to be executed when the Widget has called notifyReady.</td>
    </tr>
    <tr>
          <td><b>sendMessage(dataToSend)</b></td>
          <td>Sends a direct message to the Widget this proxy represents.</td>
    </tr>
</table>

### Class: `Ozone.lang`
<i>Defined in:</i> `ozone-lang.js`

<table>
    <tr>
        <th>Class Summary</th>
        <th></th>
    </tr>
    <tr>
        <td><b>Ozone.lang()</b></td>
        <td>Provides utility methods for localization.</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td><b>getLanguage()</b></td>
          <td>Gets the language that is currently being used by OWF.</td>
    </tr>
</table>

### Class: `Ozone.launcher.WidgetLauncher`
<i>Defined in:</i> `WidgetLauncher.js`

<table>
    <tr>
        <th>Class Summary</th>
        <th></th>
    </tr>
    <tr>
        <td><b>Ozone.launcher.WidgetLauncher(widgetEventingController</b></td>
        <td></td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th>This object is used launch other widgets.</th>
    </tr>
    <tr>
          <td><b>getInstance()</b></td>
          <td>Retrieves Ozone.eventing.Widget Singleton instance.</td>
    </tr>
    <tr>
          <td><b>launchWidget(config, callback)</b></td>
          <td>Launches a Widget based on the config.</td>
    </tr>
</table>

### Class: `Ozone.launcher.WidgetLauncherUtils`
<i>Defined in:</i> `WidgetLauncher.js`

<table>
    <tr>
        <th>Class Summary</th>
        <th></th>
    </tr>
    <tr>
        <td><b>Ozone.launcher.WidgetLauncherUtils()</b></td>
        <td>Utility functions for a widget that has been launched.</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td><b>getLaunchConfigData()</b></td>
          <td>Gets initial launch config data for this widget if it was just launched.</td>
    </tr>
</table>

### Class: `Ozone.log`
<i>Defined in:</i> `log.js`

<table>
    <tr>
        <th>Class Summary</th>
        <th></th>
    </tr>
    <tr>
        <td><b>Ozone.log()</b></td>
        <td>Provides functions to log messages and objects.</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td><b>getDefaultLogger()</b></td>
          <td>Get OWF's default logger.</td>
    </tr>
    <tr>
          <td><b>getLogger(loggerName)</b></td>
          <td>Get a logger by name, if the logger has not already been created it will be created.</td>
    </tr>
    <tr>
          <td><b>launchPopupAppender()</b></td>
          <td>Launch the log window pop-up, this will re-launch the window in the event it has been closed.</td>
    </tr>
        <tr>
          <td><b>setEnabled(enabled)</b></td>
          <td>Enable/Disable logging for the OWF application.</td>
    </tr>
</table>

### Namespace: `Ozone.metrics`
<i>Defined in:</i> `BaseMetrics.js`

<table>
    <tr>
        <th>Namespace Summary</th>
        <th></th>
    </tr>
    <tr>
        <td><b>Ozone.metrics</b></td>
        <td></td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td><b>logBatchMetrics(metrics)</b></td>
          <td>Logs a set of metrics to the server all at once.</td>
    </tr>
    <tr>
          <td><b>logMetric(userId, userName, metricSite, componentName, componentId, componentInstanceId, metricTypeId, metricData)</b></td>
          <td>Basic logging capability - meant to be called by other methods which transform or validate data.</td>
    </tr>
    <tr>
          <td><b>logWidgetRender(userId, userName, metricSite, widget)</b></td>
          <td>Log view of widget - see calls in dashboards.</td>
    </tr>
</table>    

### Class: `Ozone.pref.PrefServer`
<i>Defined in:</i> `preference.js`

<table>
    <tr>
        <th>Class Summary</th>
        <th></th>
    </tr>
    <tr>
        <td><b>Ozone.pref.PrefServer(_url)</b></td>
        <td>This object is used to create, retrieve, update and delete user preferences.</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td><b>cloneDashboard(cfg)</b></td>
          <td>Copies an existing dashboard and saves it as new.</td>
    </tr>
    <tr>
          <td><b>createOrUpdateDashboard(cfg)</b></td>
          <td>Saves changes to a new or existing dashboard.</td>
    </tr>
    <tr>
          <td><b>deleteDashboard(cfg)</b></td>
          <td>Deletes the dashboard with the specified id.</td>
    </tr>
        <tr>
          <td><b>deleteUserPreference(cfg)</b></td>
          <td>Deletes a user preference with the provided namespace and name.</td>
    </tr>
    <tr>
          <td><b>doesUserPreferenceExist(cfg)</b></td>
          <td>Checks for the existence of a user preference for a given namespace and name.</td>
    </tr>
    <tr>
          <td><b>findDashboards(cfg)</b></td>
          <td>Returns all dashboards for the logged in user.</td>
    </tr>
        <tr>
          <td><b>findDashboardsByType(cfg)</b></td>
          <td>Returns all dashboards for the logged in user filtered by the type of dashboard.</td>
    </tr>
    <tr>
          <td><b>findWidgets(cfg)</b></td>
          <td>Gets all widgets for a given user.</td>
    </tr>
    <tr>
          <td><b>getCurrentUser(cfg)</b></td>
          <td>Retrieves the current user logged into the system.</td>
    </tr>
        <tr>
          <td><b>getDashboard(cfg)</b></td>
          <td>Gets the dashboard with the specified id.</td>
    </tr>
    <tr>
          <td><b>getDefaultDashboard(cfg)</b></td>
          <td>Gets the user's default dashboard.</td>
    </tr>
    <tr>
          <td><b>getServerVersion(cfg)</b></td>
          <td>For retrieving the OWF system server version.</td>
    </tr>
        <tr>
          <td><b>getUrl()</b></td>
          <td>Get the url for the Preference Server.</td>
    </tr>
    <tr>
          <td><b>getUserPreference(cfg)</b></td>
          <td>Retrieves the user preference for the provided name and namespace.</td>
    </tr>
    <tr>
          <td><b>getWidget(cfg)</b></td>
          <td>Gets the widget with the specified id.</td>
    </tr>
        <tr>
          <td><b>setDefaultDashboard(cfg)</b></td>
          <td>Sets the user's default dashboard.</td>
    </tr>
    <tr>
          <td><b>setUrl(url)</b></td>
          <td>Sets the url for the Preference Server.</td>
    </tr>
    <tr>
          <td><b>setUserPreference(cfg)</b></td>
          <td>Creates or updates a user preference for the provided namespace and name.</td>
    </tr>
        <tr>
          <td><b>updateAndDeleteDashboards(cfg)</b></td>
          <td>Saves changes to existing dashboards.</td>
    </tr>
    <tr>
          <td><b>updateAndDeleteWidgets(cfg)</b></td>
          <td>Saves changes to existing widgets.</td>
    </tr>
</table>

### Class: `Ozone.state.WidgetState`
<i>Defined in:</i> `WidgetState.js`

<table>
    <tr>
        <th>Class Summary</th>
        <th></th>
    </tr>
    <tr>
        <td><b>Ozone.state.WidgetState(cfg)</b></td>
        <td>The Ozone.state.WidgetState object manages the two-way communication between an OWF widget and its OWF Container.</td>
    </tr>
        <tr>
         <th>Field Summary</th>
         <th></th>
    </tr>
    <tr>
          <td><b>version</b></td>
          <td>Version number.</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td><b>activateWidget(cfg)</b></td>
          <td>Activates a widget.</td>
    </tr>
    <tr>
          <td><b>addStateEventListeners(cfg)</b></td>
          <td>Adds custom state event handlers to listen to widget events.</td>
    </tr>
    <tr>
          <td><b>addStateEventOverrides(cfg)</b></td>
          <td>Adds custom state event handlers to override a widget event.</td>
    </tr>
        <tr>
          <td><b>closeWidget(cfg)</b></td>
          <td>Closes a widget.</td>
    </tr>
    <tr>
          <td><b>getInstance(cfg)</b></td>
          <td>Retrieves Ozone.state.WidgetState Singleton instance.</td>
    </tr>
    <tr>
          <td><b>getRegisteredStateEvents(cfg)</b></td>
          <td>Gets registered widget state events.</td>
    </tr>
        <tr>
          <td><b>getWidgetState(cfg)</b></td>
          <td>Gets current widget state.</td>
    </tr>
    <tr>
          <td><b>init(cfg)</b></td>
          <td>Initializes the WidgetState object.</td>
    </tr>
    <tr>
          <td><b>onStateEventReceived()</b></td>
          <td>The default callback function when an event is received.</td>
    </tr>
        <tr>
          <td><b>removeStateEventListeners(cfg)</b></td>
          <td>Removes custom state event listeners from a widget.</td>
    </tr>
    <tr>
          <td><b>removeStateEventOverrides(cfg)</b></td>
          <td>Removes custom state event listeners from a widget.</td>
    </tr>
</table>

### Class: `Ozone.state.WidgetStateHandler`
<i>Defined in:</i> `WidgetStateHandler.js`

<table>
    <tr>
        <th>Class Summary</th>
        <th></th>
    </tr>
    <tr>
        <td><b>Ozone.state.WidgetStateHandler(widgetEventingController)</b></td>
        <td>This object is used handle widget requests.</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td><b>getInstance(widgetEventingController</b></td>
          <td>Retrieves Ozone.eventing.Widget Singleton instance.</td>
    </tr>
    <tr>
          <td><b>handleWidgetRequest(config, callback)</b></td>
          <td>Handles a widget state request based on the config.</td>
    </tr>
</table>

### Namespace: `Ozone.util`
<i>Defined in:</i> `widget_utils.js`

<table>
    <tr>
        <th>Namespace Summary</th>
        <th></th>
    </tr>
    <tr>
        <td><b>Ozone.util</b></td>
        <td>Provides OWF utility methods for the widget developer.</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td><b>getFlashApp(id)</b></td>
          <td>This method returns flash/flex object from dom.</td>
    </tr>
    <tr>
          <td><b>guid()</b></td>
          <td>Returns a globally unique identifier (guid)</td>
    </tr>
    <tr>
          <td><b>hasAccess(cfg)</b></td>
          <td>Returns .</td>
    </tr>
        <tr>
          <td><b>isInContainer()</b></td>
          <td>This method informs a widget developer if their widget is running in a Container, like OWF.</td>
    </tr>
    <tr>
          <td><b>isRunningInOWF()</b></td>
          <td>This method informs a widget developer if their widget is running from the OWF or from a direct URL call.</td>
    </tr>
</table>

### Namespace: `Ozone.util.pageLoad`
<i>Defined in:</i> `pageload.js`

<table>
    <tr>
        <th>Namespace Summary</th>
        <th></th>
    </tr>
    <tr>
        <td><b>Ozone.util.pageLoad</b></td>
        <td></td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td><b>afterLoad</b></td>
          <td>Holds current date time after the onload of the widget.</td>
    </tr>
    <tr>
          <td><b>autoSend</b></td>
          <td>Enable or disable the automatic sending of loadtime.</td>
    </tr>
    <tr>
          <td><b>beforeLoad</b></td>
          <td>Holds the current date time, before the onload of the widget.</td>
    </tr>
    <tr>
          <td><b>loadTime</b></td>
          <td>Holds the load time of the widget.</td>
    </tr>
</table>
