#   Widget Launcher API
#1   Overview

The Widget Launcher API allows one widget to send data to another widget. It is possible that one of the widgets sending or receiving the data does not have a user interface. Those widgets can be configured as background widgets (explained in the OWF Administrator’s Guide). 

This walkthrough will go through the process of using the Widget Launcher API by describing Channel Listener and Channel Shouter example widget behavior. Channel Listener and Channel Shouter are widgets that are included with OWF. In the walkthrough below, Channel Listener and Channel Shouter widgets work together to demonstrate both the Eventing and the Widget Launcher APIs. **The widget launching functionality is commented out by default. For this walkthrough, include that section of the code.** 

> _Note: An additional Widget Launcher exercise is available in the **Overview - Adding the Widget Launcher** section of the [Additional Walkthroughs](OWF-7-Developer-Additional-Walkthroughs) page._

Channel Listener allows the user to subscribe to channels by entering the channel name into a text box and pressing the ![Add Channel](OWFImages/OWF7/add_channel_61x16.png) button on the widget. The widget will then display any messages which are broadcast on the channels to which it is subscribed. Channel Shouter allows the user to publish messages to specific channels by entering both the name of a specific channel as well as the message text into text boxes and pressing the ![Broadcast](OWFImages/OWF7/broadcast_47x16.png) button. 

To demonstrate the Widget Launcher API, if a user only has a Channel Shouter on their dashboard, any message sent by the Channel Shouter will launch the Channel Listener. Once launched, the Channel Listener will be listening to the same channel and display the messages which get broadcast by the Channel Shouter. 

#2   Walkthrough

**Step 1: Import the Correct JavaScript Files**

The **ChannelListener.gsp** and **ChannelShouter.gsp** use the maximum JavaScript import list. However, the minimum required include list needed to use the Widget Launcher API is described in the **Required Includes** section. 

**Step 2:**

The Widget Launcher API functionality is commented out by default. To use the sample, include the code in **ChannelShouter.gsp**.

**Step 3: Wrap the JavaScript that requires the WidgetLauncher API in the OWF.ready function**

The Widget Launcher API requires the use of Eventing. See **ChannelShouter.gsp** for example:

        …
        OWF.ready(shoutInit);
        …

**Step 4: Get the ID for the Widget to be Launched**

To launch a widget, the developer must know the widget’s GUID. This walkthrough determines the widget’s GUID by querying the preferences API using the `findWidgets` function shown below. This function retrieves a list of all widgets that a user has access to, including widget names and GUIDs. If the name of the widget is known, it is easy to find the appropriate GUID, which can be saved as a preference. The following code is searching for a widget named Channel Listener. In the code shown below, the widget to be launched is named, Channel Listener. 

```javascript
        …
        var scope = this;
        shoutInit = owfdojo.hitch(this, function() {
                OWF.Preferences.findWidgets({
                     searchParams: {
                            widgetName: ‘Channel Listener’
        		},
        		onSuccess: function(result) {
        			scope.guid = result[0].id;
        		},
        		onFailure: function(err) { /* No op */
        		} });
        …
```

See the section, **Alternative Ways to Find a Widget’s GUID**, for alternative ways to find a widget’s GUID.
 
**Step 5: Add Code to Launch the Widget**

To launch the widget, use the `launch` function on the `OWF.Launcher` object that was created as a result of `OWF.ready`. The `launch` function takes a JavaScript configuration object which has four attributes: `guid`, `launchOnlyIfClosed`, `title` and `data`.
 
* `guid` is the unique ID of the widget to be opened. 
* `LaunchOnlyIfClosed` is a Boolean flag which decides if a new widget should always be opened (`false`) or if the widget to be opened is already present on a dashboard, to simply restore said widget (`true`). 
* `title` is a string that will replace the widget’s title when launched.
* `data` is a string representing an initial set of data to be sent only if a new widget is opened. 

The data which is going to be sent must be passed as a string. In the example below, the data to be sent is a JavaScript object with two attributes – `channel` and `message`. Next, this object must be converted into a JSON string. This is accomplished by using the `OWF.Util.toString` utility function. 

> _Note: If the widget to be launched is already on the dashboard, the `data` will not be sent._ 

```javascript
            shout = owfdojo.hitch(this, function () {
            var channel = document.getElementById('InputChannel').value;
            var message = document.getElementById('InputMessage').value;
    
            if (channel != null && channel != ‘’) {
    …
	    	if (scope.guid != null && typeopf scope.guid == ‘string’) {
	    		var data = {
		    		channel: channel,
		    		message: message
                };
                Var dataString = OWF.Util.toString(data);
                OWF.Launcher.launch({
                	guid: scope.guid,
                	launchOnlyIfClosed: true,
			    	title: 'Channel Listener Launched',
        	        data: dataString
                }, function(response)
    …
        	}
          }
        }
```

**Step 6: Retrieve the Initial Data Inside the Launched Widget**

Once a widget has been launched, the widget may need to retrieve the initial set of data from the previous step. This is accomplished by using the `OWF.Launcher.getLaunchData()` function. This function will return the initial data from the previous step. In the ChannelListenerPanel.js code sample below, the data retrieved is a JSON string. This string is then parsed into a JavaScript object by using the `OWF.Util.parseJson`function. In **ChannelListenerPanel.js** the initial data sent is a channel to start listening on (`data.channel`), and an initial message to display on that channel (`data.message`).

```javascript
        …
                    render: function() {
                     var launchConfig = OWF.Launcher.getLaunchData();
                     if (launchConfig != null) {
                      var data = OWF.Util.parseJson(launchConfig);
                      if (data != null) {
                        scope.subscribeToChannel(data.channel);
                        scope.addToGrid(null,data.message,data.channel);
                      }
                     }
                    },
        …
```

#3   Additional Considerations
##Required Includes

Here is the complete list of scripts needed to successfully use this API:

```javascript
        <link href="../css/dragAndDrop.css" rel="stylesheet" type="text/css">
        <script type="text/javascript" src="https://servername:port/owf/js-min/owf-widget-min.js"></script>
        <script type="text/javascript">
              //The location is assumed to be at /<context>/js/eventing/rpc_relay.uncompressed.html if it is not set
              //OWF.relayFile = '/<context>/js/eventing/rpc_relay.uncompressed.html';
        </script>
```

Replace all occurrences of `https://servername:port` with the name of the server where OWF is running, for example, `https://www.yourcompany.com:8443`. Replace all occurrences of `<context>` with the root context of your Web application.

##Alternative Ways to Find a Widget’s GUID
###Storing the Widget’s GUID as a Preference

An alternative way to determine which widget to launch is to store the GUID as a preference in the database using the Preference API. The OWF Administration tools can be used to find the GUID of any widget. For the Channel Shouter/Channel Listener example, Channel Listener’s GUID can be found by editing the Channel Listener Widget using the Widget Editor. This will bring up a dialog that displays the GUID. The GUID should be saved under a newly created preference. The widget can then retrieve that GUID and save it to a local variable to be used later.

```javascript
         …
        var scope = this;
        shoutInit = owfdojo.hitch(this, function() {
                OWF.Preferences.getUserPreference({
                    	namespace: 'owf.widget.ChannelShouter,
                   	name: 'guid_to_launch',
                    	onSuccess: function(result) {
        			scope.guid = result.value;
                    	},
        		onFailure: function(err) { /* No op */
        		} 
        });
        …
```

###Using the Universal Name to Find the Widget

Another way to determine which widget to launch is to search using its Universal Name. This can be done by querying the Preferences API using the `getWidget` function and passing to it the widget’s Universal Name. This retrieves the specified widget’s configuration details, including its GUID.

```javascript
        …
        var scope = this;
        shoutInit = owfdojo.hitch(this, function() {
                OWF.Preferences.getWidget({
                    	universalName: 'org.owfgoss.owf.examples.NYSE',
                    	onSuccess: function(result) {
                                 scope.guid = result.guid;
                    	},
                        onFailure: function(err) { /* No op */
                        } 
        });
        …
```

> _Note: A widget’s Universal Name is defined in its descriptor file. See the **Creating Descriptor Files for Widgets** section (on the [Adding a Widget to OWF](OWF-7-Developer-Adding-a-Widget-to-OWF) page)  for details on descriptor files._

##Using Regular Expression to change a Widget’s Title

The `launchWidget` function also accepts a `titleRegex` property. This property will be used as a replacement regular expression to alter the title. This allows the current widget title to be changed in complex ways. The example below appends text to the widget’s title when it is launched.

```javascript
      …
            OWF.Launcher.launch({
              guid: this.guid_EditCopyWidget,

              //$1 represents the existing title.  the value of newtitle will be appended
              title: '$1 - ' + newtitle,
      
              //this regex matches all text in the existing title and captures it into a group
              titleRegex: /(.*)/,

              launchOnlyIfClosed: false,
              data: dataString
            }, this.launchFailureHandler);
        …
  ```