#   Widget Intents API
#1   Overview

The Widget Intents API allows widgets to tell the OWF container information about the data they can send and receive. The container then uses this information to allow users to select which widgets they want to use together.

This walkthrough will go through the process of using the Widget Intents API by describing the sample Intents widgets’ behavior. The following three sample intents widgets are included in the **OWF-bundle-7-GA.zip**:

* **NYSE Widget** - displays data from the New York Stock Exchange.
* **HTML Viewer Widget** - displays HTML (or text) in tabs.
* **Stock Chart** - plots current stock prices on a graph.

In the following walkthrough, these three widgets work together to demonstrate the Widget Intents API. 

To demonstrate the Widget Intents API:

1. Sign in to the OWF Interface and open the NYSE Widget.
2. Click on a company name. The Launch Menu will open, displaying only widgets that include viewing html/text intents. (Developers can bypass this step with the instructions found in the section **Intent Launching Data**.
3. Launch the HTML Viewer Widget. Information about the selected company will appear in a tab.  
4. To graph data, go back to the NYSE Widget and select a checkbox to the left of a company name. 
5. Click the View Current Prices button at the bottom of the widget. The Launch Menu will open, displaying only widgets that include graphing intents. 
6. Launch the Stock Chart Widget. Information about the selected company will appear on the chart. 

#2   Walkthrough

This section explains the necessary requirements for using Widget Intents: 

**Step 1: Import the correct JavaScript files**

The following list of scripts are required to use the widget intents API: 

```html
        <link href="../css/dragAndDrop.css" rel="stylesheet" type="text/css">
        <script type="text/javascript" src="https://servername:port/owf/js-min/owf-widget-min.js"></script>
        <script type="text/javascript">
              //The location is assumed to be at /<context>/js/eventing/rpc_relay.uncompressed.html if it is not set
              //OWF.relayFile = '/<context>/js/eventing/rpc_relay.uncompressed.html';
        </script>
```

Replace all occurrences of `https://servername:port` with the name of the server where OWF is running. For example, `https://www.yourcompany.com:8443`. Replace all occurrences of `<context>` with the root context of the Web application.

The previous scripts handle intents functionality. The **NYSE.gsp**, **HTMLViewer.gsp** and **StockChart.gsp**  use several additional JavaScript files to showcase their functionality.

**Step 2: Wrap the JavaScript that requires the Widget Intents API in the `OWF.ready` function**

The Widget Intents API requires the use of Eventing. For an example, see **NYSE.gsp**:

        …
        OWF.ready(init);
        …

**Step 3: Set up a widget to send and receive intents**

Use the Widget Editor in the user interface to add, edit or remove widget intents, see the **Creating Descriptor Files for Widgets** section found on the [Adding a Widget to OWF](OWF-7-Developer-Adding-a-Widget-to-OWF) page. Sending an Intent should be tied to a user-generated action such as clicking a button or link. The handler for that action should call the `OWF.Intents.startActivity` method. This method takes three arguments:

1. The first argument is **an Intent**. An Intent is simply an object describing an action and a data type. The action should be a verb describing what the user is trying to do (i.e. plot, pan, zoom, view, graph, etc.). The data type should describe what type of data is being acted upon. The data type format is described in the **Recommended Intents Data Type Conventions** section. 
2. The second argument is **an object containing the data** that the intent is sending. The format of the data depends solely on how the receiving widget is expecting to receive it.
3. The third argument is **a callback function** that is executed once the receiving widget is selected. This callback will receive information about the receiving widget. That information can be used to access the receiving widget directly.

The example below displays an intent that graphs a stock price. Once a receiving widget is selected, the graph is continuously updated with fluctuating stock prices.

```javascript
        …
           OWF.Intents.startActivity(
              {   
                 action:'Graph',
                 dataType:'application/vnd.owf.sample.price'
              },
              {
                 data: data
              },
              function (dest) {
                 //dest is an array of destination widget proxies
                 if (dest.length > 0) {
                    Ext.Array.each(dest, function(datum, index, dataRef) {
                       var json = Ext.JSON.decode(datum.id);
                       var widgetId = json.id;
                       var proxy = datum.id;
                       if (_tm) { _tm.reset(widgetId, proxy, symbols) ;}
                    });
                 }
                 else {
                    // alert('Intent was canceled');
                 }
              }					                
           );
        …
```

Use the Widget Editor in the user interface to add, edit or remove widget intents, see the **Creating Descriptor Files for Widgets** section found on the [Adding a Widget to OWF](OWF-7-Developer-Adding-a-Widget-to-OWF) page. Any widget can receive an Intent by calling the `OWF.Intents.receive` method. This method takes two arguments: 

1. The first argument is **an Intent**. An Intent is simply an object describing an action and a data type. The action should be a verb describing what the user is trying to do (i.e. plot, pan, zoom, view, graph, etc.). The data type should describe what type of data is being acted upon. 
 
2. The second argument, **a function** that is executed once an Intent is received, receives information about the sending widget. That information can be used to access the sending widget directly. It will also receive the intent and the data.
 
The example below uses Intents to plot a stock price on the graph:

```javascript
        …
           OWF.Intents.receive(
              {
                 action: 'Graph',
                 dataType: 'application/vnd.owf.sample.price'
              },
              function (sender, intent, data) {
                 doPlot(data.data);
              }
           );
        …
```

#3   Additional Capabilities
##WidgetProxy on Ready

WidgetProxy objects have an onReady method which tells the caller if the widget that is represented by the proxy is ready to communicate [i.e., If it has called `OWF.notifyWidgetReady()`]. The `onReady` method takes a callback function as its only parameter. If the widget represented by the proxy is already ready, the callback is fired immediately. Otherwise, it is fired once the represented widget calls `notifyWidgetReady`. Also, `WidgetProxy` objects have a boolean `isReady` property that states whether they are ready.

Example `onReady` code:

        var widgetProxy = OWF.RPC.getWidgetProxy(id);
        widgetProxy.onReady(function() { console.log("Other widget is ready!"); });

##Intent Launching Data

To identify if a widget was launched using an intent, use the Widget Launcher API. If the widget was launched by an intent, the function `OWF.Launcher.getLaunchData()` will return a JSON string with the value `intents:true` as its launch data.

##Send an Intent to a known set of Widgets

The Intents API may be used to directly send an Intent to a set of widgets without invoking the Launch Menu. The `startActivity` function  accepts a destination array of `WidgetProxy` objects. If this array is specified the intent will be sent only to those widgets. `WidgetProxies` may be obtained by using the Widget RPC API or by using a previous `startActivity` call.
  
Example code:

```javascript
        …
           Var dest = //Array of Widget Proxies obtained earlier
           OWF.Intents.startActivity(
              {   
                 action:'Graph',
                 dataType:'application/vnd.owf.sample.price'
              },
              {
                 data: data
              },
              function (dest) {
                 //dest is an array of destination widget proxies
                 if (dest.length > 0) {
                    Ext.Array.each(dest, function(datum, index, dataRef) {
                       var json = Ext.JSON.decode(datum.id);
                       var widgetId = json.id;
                       var proxy = datum.id;
                       if (_tm) { _tm.reset(widgetId, proxy, symbols) ;}
                    });
                 }
                 else {
                    // alert('Intent was canceled');
                 }
              },
              dest					                
           );
        …
```

#4   Additional Considerations
##Recommended Intents Data Type Conventions

Data types are stored as strings in the database. However, the success of Intents relies heavily on the ability to share data types between widgets. To facilitate this, OWF follows the MIME type naming conventions as recognized by the [Internet Assigned Numbers Authority (IANA)](http://www.iana.org/assignments/media-types) and [Webintents.org](http://webintents.org/#specification). All OWF developers should use the intents provided by these organizations to create their own intents. It is also strongly recommended that custom MIME types use the `application/vnd.owf.<datatype>` naming convention.