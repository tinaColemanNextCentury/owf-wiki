# JavaScript API Reference Document

The following is a summary of the OWF JavaScript APIs. Additional information on each API is found in the JavaScript document located in the OWF Help Bundle.

* [OWF](OWF-7-JSDoc#namespace-owf)
* [OWF.Chrome](OWF-7-JSDoc#namespace-owfchrome)
* [OWF.DragAndDrop](OWF-7-JSDoc#namespace-owfdraganddrop)
* [OWF.Eventing](OWF-7-JSDoc#namespace-owfeventing)
* [OWF.Intents](OWF-7-JSDoc#namespace-owfintents)
* [OWF.Lang](OWF-7-JSDoc#namespace-owflang)
* [OWF.Launcher](OWF-7-JSDoc#namespace-owflauncher)
* [OWF.Log](OWF-7-JSDoc#namespace-owflog)
* [OWF.Metrics](OWF-7-JSDoc#namespace-owfmetrics)
* [OWF.Preferences](OWF-7-JSDoc#namespace-owfpreferences)
* [OWF.RPC](OWF-7-JSDoc#namespace-owfrpc)
* [OWF.Util](OWF-7-JSDoc#namespace-owfutil)

<br>
* [Ozone.chrome.WidgetChrome](OWF-7-JSDoc#class-ozonechromewidgetchrome)
* [Ozone.dragAndDrop.WidgetDragandDrop](OWF-7-JSDoc#class-ozonedraganddropwigetdraganddrop)
* [Ozone.eventing.Widget](OWF-7-JSDoc#class-ozoneeventingwidget)
* [Ozone.eventing.WidgetProxy](OWF-7-JSDoc#class-ozoneeventingwidgetproxy)
* [Ozone.lang](OWF-7-JSDoc#class-ozonelang)
* [Ozone.launcher.WidgetLauncher](OWF-7-JSDoc#class-ozonelauncherwidgetlauncher)
* [Ozone.launcher.WidgetLauncherUtils](OWF-7-JSDoc#class-ozonelauncherwidgetlauncherutils)
* [Ozone.log](OWF-7-JSDoc#class-ozonelong)
* [Ozone.metrics](OWF-7-JSDoc#namespace-ozonemetrics)
* [Ozone.pref.PrefServer](OWF-7-JSDoc#class-ozoneprefprefserver)
* [Ozone.state.WidgetState](OWF-7-JSDoc#class-ozonestatewidgetstate)
* [Ozone.state.WidgetStateHandler](OWF-7-JSDoc#class-ozonestatewidgetstatehandler)
* [Ozone.util](OWF-7-JSDoc#class-ozoneutil)
* [Ozone.util.pageLoad](OWF-7-JSDoc#class-ozoneutilpageload)


### Namespace: `OWF`
<i>Defined in:</i> `Widget.js`

<table>
    <tr>
        <th>Namespace Summary</th>
        <th></th>
    </tr>
    <tr>
        <td>OWF</td>
        <td></td>
    </tr>
     <tr>
         <th>Field Summary</th>
         <th></th>
    </tr>
    <tr>
          <td>OWF.relayFile</td>
          <td>The location of the widget relay file.</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td>OWF.getContainerName()</td>
          <td>Returns the name of the Container the Widget is in.</td>
    </tr>
    <tr>
          <td>OWF.getContainerUrl()</td>
          <td>Returns the URL of the Container the Widget is in.</td>
    </tr>
    <tr>
          <td>OWF.getContainerVersion()</td>
          <td>Returns the version of the Container the Widget is in.</td>
    </tr>
        <tr>
          <td>OWF.getCurrentTheme()</td>
          <td>Returns an object containing information on the current OWF theme.</td>
    </tr>
    <tr>
          <td>OWF.getDashboardLayout()</td>
          <td>Returns type of dashboard in which the widget is opened.</td>
    </tr>
    <tr>
          <td>OWF.getIframeId()</td>
          <td>Returns the Widget Id.</td>
    </tr>
        <tr>
          <td>OWF.getInstanceId()</td>
          <td>Returns instance GUID of the widget.</td>
    </tr>
    <tr>
          <td>OWF.getOpenedWidgets(callback)</td>
          <td>Gets all opened widgets on the current dashboard.</td>
    </tr>
    <tr>
          <td>OWF.getUrl()</td>
          <td>Returns URL of the widget.</td>
    </tr>
        <tr>
          <td>OWF.getVersion()</td>
          <td>Returns version of the widget.</td>
    </tr>
    <tr>
          <td>OWF.getWidgetGuid()</td>
          <td>Returns definition GUID of the widget.</td>
    </tr>
    <tr>
          <td>OWF.isDashboardLocked()</td>
          <td>Returns whether or not the dashboard in which the widget is opened is locked.</td>
    </tr>
        <tr>
          <td>OWF.notifyWidgetReady()</td>
          <td>This function should be called once the widget is ready and all initialization is completed.</td>
    </tr>
    <tr>
          <td>OWF.ready(handler, scope)</td>
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
          <td>OWF.Chrome.addHeaderButtons(cfg)</td>
          <td>Adds buttons to the Widget Chrome.</td>
    </tr>
    <tr>
          <td>OWF.Chrome.addHeaderMenus(cfg)</td>
          <td>Adds menus to the Widget Chrome.</td>
    </tr>
    <tr>
          <td>OWF.Chrome.getTitle(cfg)</td>
          <td>Gets the Widget's Title from the Chrome.</td>
    </tr>
        <tr>
          <td>OWF.Chrome.insertHeaderButtons(cfg)</td>
          <td>Inserts new buttons to the Widget Chrome.</td>
    </tr>
    <tr>
          <td>OWF.Chrome.insertHeaderMenus(cfg)</td>
          <td>Inserts new menus into the Widget Chrome.</td>
    </tr>
        <tr>
          <td>OWF.Chrome.isModified(cfg)</td>
          <td>Checks to see if the Widget Chrome has already been modified.</td>
    </tr>
    <tr>
          <td>OWF.Chrome.listHeaderButtons(cfg)</td>
          <td>Lists all buttons that have been added to the widget chrome.</td>
    </tr>
        <tr>
          <td>OWF.Chrome.listHeaderMenus(cfg)</td>
          <td>Lists all menus that have been added to the widget chrome.</td>
    </tr>
    <tr>
          <td>OWF.Chrome.removeHeaderButtons(cfg)</td>
          <td>Removes existing buttons on the Widget Chrome based on itemId.</td>
    </tr>
        <tr>
          <td>OWF.Chrome.removeHeaderMenus(cfg)</td>
          <td>Removes existing menus on the Widget Chrome based on itemId.</td>
    </tr>
    <tr>
          <td>OWF.Chrome.setTitle(cfg)</td>
          <td>Sets the Widget's Title in the Chrome.</td>
    </tr>
        <tr>
          <td>OWF.Chrome.updateHeaderButtons(cfg)/</td>
          <td>Updates any existing buttons in the Widget Chrome based on the itemId.</td>
    </tr>
    <tr>
          <td>OWF.Chrome.updateHeaderMenus(cfg)</td>
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
        <td>OWF.DragAndDrop</td>
        <td>The OWF.DragAndDrop object manages the drag and drop for an individual widget.</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td>OWF.DragAndDrop.addDropZoneHandler(cfg)</td>
          <td>Adds a new drop zone to be managed.</td>
    </tr>
    <tr>
          <td>OWF.DragAndDrop.getDragStartData()</td>
          <td>Returns data sent when a drag was started</td>
    </tr>
    <tr>
          <td>OWF.DragAndDrop.getDropEnabled()</td>
          <td>Returns whether the a drop is enabled (this is only true when the mouse is over a drop zone)</td>
    </tr>
        <tr>
          <td>OWF.DragAndDrop.isDragging()</td>
          <td>Returns whether a drag is in progress.</td>
    </tr>
    <tr>
          <td>OWF.DragAndDrop.onDragStart(callback, scope)</td>
          <td>Executes the callback passed when a drag starts in any widget.</td>
    </tr>
        <tr>
          <td>OWF.DragAndDrop.onDragStop(callback, scope)</td>
          <td>Executes the callback passed when a drag stops in any widget.</td>
    </tr>
    <tr>
          <td>OWF.DragAndDrop.onDrop(callback, scope)</td>
          <td>Executes the callback passed when a drop occurs in the widget.</td>
    </tr>
        <tr>
          <td>OWF.DragAndDrop.setDropEnabled(dropEnabled)</td>
          <td>Toggles the dragIndicator to indicate successful or unsuccessful drop</td>
    </tr>
    <tr>
          <td>OWF.DragAndDrop.setFlashWidgetId(id)</td>
          <td>Use this method to set flex dom element id, so that drag and drop can be enabled in flex widgets.</td>
    </tr>
        <tr>
          <td>OWF.DragAndDrop.startDrag(cfg)</td>
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
        <td>OWF.Eventing</td>
        <td>The OWF.Eventing object manages the eventing for an individual widget.</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td>OWF.Eventing.publish(channelName, message, dest)</td>
          <td>Publishes a message to a given channel.</td>
    </tr>
    <tr>
          <td>OWF.Eventing.subscribe(channelName, handler)</td>
          <td>Subscribe to a named channel for a given function.</td>
    </tr>
    <tr>
          <td>OWF.Eventing.unsubscribe(channelName)</td>
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
        <td>OWF.Intents</td>
        <td></td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td>OWF.Intents.receive(intent, handler)</td>
          <td>Register to receive an Intent</td>
    </tr>
    <tr>
          <td>OWF.Intents.startActivity(intent, data, handler, dest)</td>
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
        <td>OWF.Lang</td>
        <td>Provides utility methods for localization.</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td>OWF.Lang.getLanguage()</td>
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
        <td>OWF.Launcher</td>
        <td>This object is used launch other widgets.</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td>OWF.Launcher.getLaunchData()</td>
          <td>Retrieves initial launch data for this widget if it is opened by another widget.</td>
    </tr>
    <tr>
          <td>OWF.Launcher.launch(config, callback)</td>
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
        <td>OWF.Log</td>
        <td>Provides functions to log messages and objects.</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td>OWF.Log.getDefaultLogger()</td>
          <td>Get OWF's default logger.</td>
    </tr>
    <tr>
          <td>OWF.Log.getLogger(loggerName)</td>
          <td>Get a logger by name, if the logger has not already been created it will be created.</td>
    </tr>
    <tr>
          <td>OWF.Log.launchPopupAppender()</td>
          <td>Launch the log window pop-up, this will re-launch the window in the event it has been closed.</td>
    </tr>
        <tr>
          <td>OWF.Log.setEnabled(enabled)</td>
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
        <td>OWF.Metrics</td>
        <td></td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td>OWF.Metrics.logBatchMetrics(metrics)</td>
          <td>Logs a set of metrics to the server all at once.</td>
    </tr>
    <tr>
          <td>OWF.Metrics.logMetric(userId, userName, metricSite, componentName, componentId, componentInstanceId, metricTypeId, metricData)</td>
          <td>Basic logging capability - meant to be called by other methods which transform or validate data.</td>
    </tr>
    <tr>
          <td>OWF.Metrics.logWidgetRender(userId, userName, metricSite, widget)</td>
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
        <td>OWF.Preferences</td>
        <td>This object is used to create, retrieve, update and delete user preferences.</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td>OWF.Preferences.cloneDashboard(cfg)</td>
          <td>Copies an existing dashboard and saves it as new.</td>
    </tr>
    <tr>
          <td>OWF.Preferences.createOrUpdateDashboard(cfg)</td>
          <td>Saves changes to a new or existing dashboard.</td>
    </tr>
    <tr>
          <td>OWF.Preferences.deleteDashboard(cfg)</td>
          <td>Deletes the dashboard with the specified id.</td>
    </tr>
        <tr>
          <td>OWF.Preferences.deleteUserPreference(cfg)</td>
          <td>Deletes a user preference with the provided namespace and name.</td>
    </tr>
        <tr>
          <td>OWF.Preferences.doesUserPreferenceExist(cfg)</td>
          <td>Checks for the existence of a user preference for a given namespace and name.</td>
    </tr>
        <tr>
          <td>OWF.Preferences.findDashboards(cfg)</td>
          <td>Returns all dashboards for the logged in user.</td>
    </tr>
        <tr>
          <td>OWF.Preferences.findDashboardsByType(cfg)</td>
          <td>Returns all dashboards for the logged in user filtered by the type of dashboard.</td>
    </tr>
        <tr>
          <td>OWF.Preferences.findWidgets(cfg)</td>
          <td>Gets all widgets for a given user.</td>
    </tr>
        <tr>
          <td>OWF.Preferences.getCurrentUser(cfg)</td>
          <td>Retrieves the current user logged into the system.</td>
    </tr>
        <tr>
          <td>OWF.Preferences.getDashboard(cfg)</td>
          <td>Gets the dashboard with the specified id.</td>
    </tr>
        <tr>
          <td>OWF.Preferences.getDefaultDashboard(cfg)</td>
          <td>Gets the user's default dashboard.</td>
    </tr>
        <tr>
          <td>OWF.Preferences.getServerVersion(cfg)</td>
          <td>For retrieving the OWF system server version.</td>
    </tr>
        <tr>
          <td>OWF.Preferences.getUrl()</td>
          <td>Get the url for the Preference Server.</td>
    </tr>
        <tr>
          <td>OWF.Preferences.getUserPreference(cfg)</td>
          <td>Retrieves the user preference for the provided name and namespace.</td>
    </tr>
        <tr>
          <td>OWF.Preferences.getWidget(cfg)</td>
          <td>Gets the widget with the specified id.</td>
    </tr>
        <tr>
          <td>OWF.Preferences.setDefaultDashboard(cfg)</td>
          <td>Sets the user's default dashboard.</td>
    </tr>
        <tr>
          <td>OWF.Preferences.setUrl(url)</td>
          <td>Sets the url for the Preference Server.</td>
    </tr>
        <tr>
          <td>OWF.Preferences.setUserPreference(cfg)</td>
          <td>Creates or updates a user preference for the provided namespace and name.</td>
    </tr>
        <tr>
          <td>OWF.Preferences.updateAndDeleteDashboards(cfg)</td>
          <td>Saves changes to existing dashboards.</td>
    </tr>
        <tr>
          <td>OWF.Preferences.updateAndDeleteWidgets(cfg)</td>
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
        <td>OWF.RPC</td>
        <td></td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td>OWF.RPC.getWidgetProxy(instanceGuid, callback)</td>
          <td>Gets a proxy object that contains methods exposed by other widget.</td>
    </tr>
    <tr>
          <td>OWF.RPC.handleDirectMessage(fn)</td>
          <td>Register a function to be executed when a direct message is received from another widget.</td>
    </tr>
    <tr>
          <td>OWF.RPC.registerFunctions(objs)</td>
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

### CLass: `Ozone.chrome.WidgetChrome`
<i>Defined in:</i> `WidgetChrome.js`

<table>
    <tr>
        <th>Class Summary</th>
        <th></th>
    </tr>
    <tr>
        <td>Ozone.chrome.WidgetChrome(config)</td>
        <td>This object allows a widget to modify the button contained in the widget header (the chrome).</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td>addHeaderButtons(cfg)</td>
          <td>Adds buttons to the Widget Chrome.</td>
    </tr>
    <tr>
          <td>addHeaderMenus(cfg)</td>
          <td>Adds menus to the Widget Chrome.</td>
    </tr>
    <tr>
          <td>getInstance(config)</td>
          <td>Retrieves Ozone.chrome.WidgetChrome Singleton instance.</td>
    </tr>
        <tr>
          <td>getTitle(cfg)</td>
          <td>Gets the Widget's Title from the Chrome.</td>
    </tr>
    <tr>
          <td>insertHeaderButtons(cfg)</td>
          <td>Inserts new buttons to the Widget Chrome.</td>
    </tr>
    <tr>
          <td>insertHeaderMenus(cfg)</td>
          <td>Inserts new menus into the Widget Chrome.</td>
    </tr>
        <tr>
          <td>isModified(cfg)</td>
          <td>Checks to see if the Widget Chrome has already been modified.</td>
    </tr>
    <tr>
          <td>listHeaderButtons(cfg)</td>
          <td>Lists all buttons that have been added to the widget chrome.</td>
    </tr>
    <tr>
          <td>listHeaderMenus(cfg)</td>
          <td>Lists all menus that have been added to the widget chrome.</td>
    </tr>
        <tr>
          <td>removeHeaderButtons(cfg)</td>
          <td>Removes existing buttons on the Widget Chrome based on itemId.</td>
    </tr>
    <tr>
          <td>removeHeaderMenus(cfg)</td>
          <td>Removes existing menus on the Widget Chrome based on itemId.</td>
    </tr>
    <tr>
          <td>setTitle(cfg)</td>
          <td>Sets the Widget's Title in the Chrome</td>
    </tr>
        <tr>
          <td>updateHeaderButtons(cfg)</td>
          <td>Updates any existing buttons in the Widget Chrome based on the itemId.</td>
    </tr>
    <tr>
          <td>updateHeaderMenus(cfg)</td>
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
        <td>Ozone.dragAndDrop.WidgetDragAndDrop(cfg)</td>
        <td>The Ozone.dragAndDrop.WidgetDragAndDrop object manages the drag and drop for an individual widget.</td>
    </tr>
        <tr>
         <th>Field Summary</th>
         <th></th>
    </tr>
    <tr>
          <td>dragStart</td>
          <td>dragStart is the name of the event when a drag is started.</td>
    </tr>
        <tr>
          <td>dragStop</td>
          <td>dragStop is the name of the event when a drag is stopped.</td>
    </tr>
        <tr>
          <td>dropReceive</td>
          <td>dropReceive is the name of the event when a drop occurs on this widget.</td>
    </tr>
        <tr>
          <td>version</td>
          <td>version number</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td>addCallback(eventName, cb)</td>
          <td>Adds a function as a callback to Drag and Drop events.</td>
    </tr>
    <tr>
          <td>addDropZoneHandler(cfg)</td>
          <td>Adds a new drop zone to be managed.</td>
    </tr>
    <tr>
          <td>doStartDrag(cfg)</td>
          <td>Starts a drag.</td>
    </tr>
        <tr>
          <td>getDragStartData()</td>
          <td>Returns data sent when a drag was started.</td>
    </tr>
    <tr>
          <td>getDropEnabled()</td>
          <td>Returns whether the a drop is enabled (this is only true when the mouse is over a drop zone).</td>
    </tr>
    <tr>
          <td>getInstance(cfg)</td>
          <td>Retrieves Ozone.dragAndDrop.WidgetDragAndDrop Singleton instance.</td>
    </tr>
        <tr>
          <td>init(cfg)</td>
          <td>Initializes the WidgetDragAndDrop object.</td>
    </tr>
    <tr>
          <td>isDragging()</td>
          <td>Returns whether a drag is in progress.</td>
    </tr>
    <tr>
          <td>setDropEnabled(dropEnabled)</td>
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
        <td>Ozone.eventing.Widget(widgetRelay, afterInit)</td>
        <td>The Ozone.eventing.Widget object manages the eventing for an individual widget (Deprecated).</td>
    </tr>
        <tr>
         <th>Field Summary</th>
         <th></th>
    </tr>
    <tr>
          <td>Ozone.eventing.Widget.widgetRelayURL</td>
          <td>The location of the widget relay file.</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td>getInstance(afterInit, widgetRelay)</td>
          <td>Retrieves Ozone.eventing.Widget Singleton instance.</td>
    </tr>
    <tr>
          <td>getWidgetId()</td>
          <td>Returns the Widget Id.</td>
    </tr>
    <tr>
          <td>publish(channelName, message, dest, accessLevel)</td>
          <td>Publish a message to a given channel.</td>
    </tr>
        <tr>
          <td>subscribe(channelName, handler)</td>
          <td>Subscribe to a named channel for a given function.</td>
    </tr>
        <tr>
          <td>unsubscribe(channelName)</td>
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
        <td>Ozone.eventing.WidgetProxy(wid, functions, srcId, proxy)</td>
        <td>Creates or updates a proxy - This is a private constructor - Do not call this directly.</td>
    </tr>
        <tr>
         <th>Field Summary</th>
         <th></th>
    </tr>
    <tr>
          <td>id</td>
          <td>Id of the Widget that this proxy represents.</td>
    </tr>
        <tr>
          <td>isReady</td>
          <td>Flag which represents if the Widget this proxy represents.</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td>onReady(readyListener, readyListenerScope)</td>
          <td>Registers a listener function to be executed when the Widget has called notifyReady.</td>
    </tr>
    <tr>
          <td>sendMessage(dataToSend)</td>
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
        <td>Ozone.lang()</td>
        <td>Provides utility methods for localization.</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td>getLanguage()</td>
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
        <td>Ozone.launcher.WidgetLauncher(widgetEventingController</td>
        <td></td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th>This object is used launch other widgets.</th>
    </tr>
    <tr>
          <td>getInstance()</td>
          <td>Retrieves Ozone.eventing.Widget Singleton instance.</td>
    </tr>
    <tr>
          <td>launchWidget(config, callback)</td>
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
        <td>Ozone.launcher.WidgetLauncherUtils()</td>
        <td>Utility functions for a widget that has been launched.</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td>getLaunchConfigData()</td>
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
        <td>Ozone.log()</td>
        <td>Provides functions to log messages and objects.</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td>getDefaultLogger()</td>
          <td>Get OWF's default logger.</td>
    </tr>
    <tr>
          <td>getLogger(loggerName)</td>
          <td>Get a logger by name, if the logger has not already been created it will be created.</td>
    </tr>
    <tr>
          <td>launchPopupAppender()</td>
          <td>Launch the log window pop-up, this will re-launch the window in the event it has been closed.</td>
    </tr>
        <tr>
          <td>setEnabled(enabled)</td>
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
        <td>Ozone.metrics</td>
        <td></td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td>logBatchMetrics(metrics)</td>
          <td>Logs a set of metrics to the server all at once.</td>
    </tr>
    <tr>
          <td>logMetric(userId, userName, metricSite, componentName, componentId, componentInstanceId, metricTypeId, metricData)</td>
          <td>Basic logging capability - meant to be called by other methods which transform or validate data.</td>
    </tr>
    <tr>
          <td>logWidgetRender(userId, userName, metricSite, widget)</td>
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
        <td>Ozone.pref.PrefServer(_url)</td>
        <td>This object is used to create, retrieve, update and delete user preferences.</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td>cloneDashboard(cfg)</td>
          <td>Copies an existing dashboard and saves it as new.</td>
    </tr>
    <tr>
          <td>createOrUpdateDashboard(cfg)</td>
          <td>Saves changes to a new or existing dashboard.</td>
    </tr>
    <tr>
          <td>deleteDashboard(cfg)</td>
          <td>Deletes the dashboard with the specified id.</td>
    </tr>
        <tr>
          <td>deleteUserPreference(cfg)</td>
          <td>Deletes a user preference with the provided namespace and name.</td>
    </tr>
    <tr>
          <td>doesUserPreferenceExist(cfg)</td>
          <td>Checks for the existence of a user preference for a given namespace and name.</td>
    </tr>
    <tr>
          <td>findDashboards(cfg)</td>
          <td>Returns all dashboards for the logged in user.</td>
    </tr>
        <tr>
          <td>findDashboardsByType(cfg)</td>
          <td>Returns all dashboards for the logged in user filtered by the type of dashboard.</td>
    </tr>
    <tr>
          <td>findWidgets(cfg)</td>
          <td>Gets all widgets for a given user.</td>
    </tr>
    <tr>
          <td>getCurrentUser(cfg)</td>
          <td>Retrieves the current user logged into the system.</td>
    </tr>
        <tr>
          <td>getDashboard(cfg)</td>
          <td>Gets the dashboard with the specified id.</td>
    </tr>
    <tr>
          <td>getDefaultDashboard(cfg)</td>
          <td>Gets the user's default dashboard.</td>
    </tr>
    <tr>
          <td>getServerVersion(cfg)</td>
          <td>For retrieving the OWF system server version.</td>
    </tr>
        <tr>
          <td>getUrl()</td>
          <td>Get the url for the Preference Server.</td>
    </tr>
    <tr>
          <td>getUserPreference(cfg)</td>
          <td>Retrieves the user preference for the provided name and namespace.</td>
    </tr>
    <tr>
          <td>getWidget(cfg)</td>
          <td>Gets the widget with the specified id.</td>
    </tr>
        <tr>
          <td>setDefaultDashboard(cfg)</td>
          <td>Sets the user's default dashboard.</td>
    </tr>
    <tr>
          <td>setUrl(url)</td>
          <td>Sets the url for the Preference Server.</td>
    </tr>
    <tr>
          <td>setUserPreference(cfg)</td>
          <td>Creates or updates a user preference for the provided namespace and name.</td>
    </tr>
        <tr>
          <td>updateAndDeleteDashboards(cfg)</td>
          <td>Saves changes to existing dashboards.</td>
    </tr>
    <tr>
          <td>updateAndDeleteWidgets(cfg)</td>
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
        <td>Ozone.state.WidgetState(cfg)</td>
        <td>The Ozone.state.WidgetState object manages the two-way communication between an OWF widget and its OWF Container.</td>
    </tr>
        <tr>
         <th>Field Summary</th>
         <th></th>
    </tr>
    <tr>
          <td>version</td>
          <td>Version number.</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td>activateWidget(cfg)</td>
          <td>Activates a widget.</td>
    </tr>
    <tr>
          <td>addStateEventListeners(cfg)</td>
          <td>Adds custom state event handlers to listen to widget events.</td>
    </tr>
    <tr>
          <td>addStateEventOverrides(cfg)</td>
          <td>Adds custom state event handlers to override a widget event.</td>
    </tr>
        <tr>
          <td>closeWidget(cfg)</td>
          <td>Closes a widget.</td>
    </tr>
    <tr>
          <td>getInstance(cfg)</td>
          <td>Retrieves Ozone.state.WidgetState Singleton instance.</td>
    </tr>
    <tr>
          <td>getRegisteredStateEvents(cfg)</td>
          <td>Gets registered widget state events.</td>
    </tr>
        <tr>
          <td>getWidgetState(cfg)</td>
          <td>Gets current widget state.</td>
    </tr>
    <tr>
          <td>init(cfg)</td>
          <td>Initializes the WidgetState object.</td>
    </tr>
    <tr>
          <td>onStateEventReceived()</td>
          <td>The default callback function when an event is received.</td>
    </tr>
        <tr>
          <td>removeStateEventListeners(cfg)</td>
          <td>Removes custom state event listeners from a widget.</td>
    </tr>
    <tr>
          <td>removeStateEventOverrides(cfg)</td>
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
        <td>Ozone.state.WidgetStateHandler(widgetEventingController)</td>
        <td>This object is used handle widget requests.</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td>getInstance(widgetEventingController</td>
          <td>Retrieves Ozone.eventing.Widget Singleton instance.</td>
    </tr>
    <tr>
          <td>handleWidgetRequest(config, callback)</td>
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
        <td>Ozone.util</td>
        <td>Provides OWF utility methods for the widget developer.</td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td>getFlashApp(id)</td>
          <td>This method returns flash/flex object from dom.</td>
    </tr>
    <tr>
          <td>guid()</td>
          <td>Returns a globally unique identifier (guid)</td>
    </tr>
    <tr>
          <td>hasAccess(cfg)</td>
          <td>Returns .</td>
    </tr>
        <tr>
          <td>isInContainer()</td>
          <td>This method informs a widget developer if their widget is running in a Container, like OWF.</td>
    </tr>
    <tr>
          <td>isRunningInOWF()</td>
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
        <td>Ozone.util.pageLoad</td>
        <td></td>
    </tr>
    <tr>
         <th>Method Summary</th>
         <th></th>
    </tr>
    <tr>
          <td>afterLoad</td>
          <td>Holds current date time after the onload of the widget.</td>
    </tr>
    <tr>
          <td>autoSend</td>
          <td>Enable or disable the automatic sending of loadtime.</td>
    </tr>
    <tr>
          <td>beforeLoad</td>
          <td>Holds the current date time, before the onload of the widget.</td>
    </tr>
    <tr>
          <td>loadTime</td>
          <td>Holds the load time of the widget.</td>
    </tr>
</table>
