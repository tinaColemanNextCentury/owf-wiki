#   Widget State API
#1   Overview

This walkthrough will discuss the process of using the Widget State API by describing the Event Monitor example widget behavior. The Widget State API (and Event Monitor Widget, included with OWF) allows a widget to be notified whenever various events occur to itself or to other widgets. The widget then has the opportunity to react to/interact with the event. Some events that may be responded to include resize events, minimize events, close events, etc. The Widget State API also allows the widget developer to query the state of a given widget at any time. 

To illustrate and provide a coding example for the Widget State API, we have created the Event Monitor, a sample widget that uses the Widget State API. Event Monitor allows the user to select specific state events to listen to or override. The widget will then display the timestamps associated with the captured events. Additionally, for events which are overridden, the user will be prompted to either close the widget or cancel the override. Information about the state of the widget is displayed and updated every time a registered event occurs.

#2   Adding the Event Monitor Widget to OWF

Follow the directions on the [Adding a Widget to OWF](OWF-7-Developer-Adding-a-Widget-to-OWF) page to create widget definitions which point to **EventMonitor.html**. Then, assign the widget to a user, and apply the widget to one of the user’s dashboards. Use the following data for widget definitions:

**Table: Event Monitor Widget Definition Text**

<table>
  <tr>
    <th>Definition</th>
    <th>Data Input Field</th>
  </tr>
  <tr>
    <td>URL</td>
    <td>https://owf-server:port/owf/examples/walkthrough/widget/EventMonitor.html</td>
  </tr>
  <tr>
    <td>Large Icon</td>
    <td>http://owf-server:port/widget-server-name:port/owf/examples/walkthrough/images/event_monitor_blue_icon.png</td>
  </tr>
  <tr>
    <td>Small Icon </td>
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

#3   Walkthrough for Listening to Widget Events

The following steps will explain how to listen to widget events:

**1. Import the Proper JavaScript Files**

 The **EventMonitor.html** uses the minified OWF bundle, which can be included from the location below:

```html
        <script type="text/javascript" src="https://servername:port/owf/js-min/owf-widget-min.js"></script>
```

 Replace all occurrences of `https://servername:port` with the name of the server where OWF is running, for example, `https://www.yourcompany.com:8443`. 



**2. Add Code to Initialize Eventing**

 The Widget State API requires the use of Eventing. To instantiate a WidgetState JavaScript object, first create the Widget Eventing Object. See **EventMonitor.html** for example:

```javascript
        …
        eventMonitor.widgetEventingController = Ozone.eventing.Widget.getInstance();
        …
```

**3. Create the Widget State Object**

 Before beginning to monitor the widget state, a new Widget State object must be created. The WidgetState object must be initialized with a JSON object. This object may contain up to five attributes: `widgetEventingController`, `autoInit`, `widgetGuid`, `stateChannel` and `onStateEventReceived`. (Not all five attributes are required.) 

   * `widgetEventingController` is the Widget Eventing Object created in Step 2. This is a mandatory attribute. It is used to facilitate the two-way communication between OWF widgets and the OWF framework.
   * `autoInit` is a Boolean flag which decides whether or not to automatically start listening to the state channel. This attribute is optional and defaults to true.
   * `widgetGuid` is the unique ID of the widget to be monitored. This attribute is optional and defaults to the widget in which the Widget State object was created.
   * `stateChannel` specifies the name of the channel on which to send and receive events. This attribute is optional and defaults to `_WIDGET_STATE_CHANNEL_ + <widgetGuid>`.
   * `onStateEventReceived` is a callback function that performs a specific function with the event that it receives. This is the function that gets called when widget events fire. So, not including this function means that nothing will happen when events fire. This may be desirable if the only thing the widget state API is being used for is to query state, rather than listening to events. 

```javascript
        …
          eventMonitor.widgetEventingController = Ozone.eventing.Widget.getInstance();
 		        
          eventMonitor.widgetState = Ozone.state.WidgetState.getInstance({
        				widgetEventingController:  eventMonitor.widgetEventingController,
        				autoInit: true,
        				onStateEventReceived: handleStateEvent
         			}); 
        …
```

**4. Define Callback for When Events Are Received**

 The onStateEventReceived callback (defined in Step 3) will be passed two parameters: `sender` and `msg`. sender is the id of the iframe that sent the event, or “..” if the event came from the OWF Framework. `msg` is the specific information about the fired event. It will be a JSON object which has two attributes: `eventName` and `eventKey`. `EventName` is the name of the event fired. `eventKey` is a unique id that is assigned to events. 

> _Note: The callback is not provided with any information about the widget. To get the current state of the widget, use the getWidgetState method of the `WidgetState` object._

#4   Additional Widget State API Functions 
##Register a State Event

To begin monitoring specific state events, the events must be registered. The WidgetState object provides two methods for registering events:

* `addStateEventListeners`—allows the widget to begin listening to specified events.
* `addStateEventOverrides`—allows the user to stop the event and perform the `WidgetState.onStateEventReceived` callback instead.

Both methods take a JSON object that has two attributes: `events` and `callback`. `events` is an array of event names to be registered. This is an optional attribute and defaults to all events. `callback` is a callback function that does something once the event has been successfully registered. 

```javascript
        …
        eventMonitor.widgetState.addStateEventListeners({
        	events: [event],
        	callback: function() {
                        …
        	}
        });
        …
        eventMonitor.widgetState.addStateEventOverrides({
        	events: [event],
        	callback: function() {
                        …
        	}
        });
        …
```

“Overriding a State Event” is optional ways to register a state event.
 
* **Overriding a State Event**

 Code can be added such that when state events are overridden, the `WidgetState.onStateEventReceived` callback function can do something with the event. 

```javascript
        …
        var continueEvent = confirm ("Event overridden. Would you like to close this widget?");
        if (continueEvent) {
        	// remove listener override to prevent looping
        	eventMonitor.widgetState.removeStateEventOverrides({
        		events: ['beforeclose'],
        		callback: function() {
              			// close widget in callback
            			this.widgetState.closeWidget();
        		}
        	});
        }
```

> _Note: It is possible to have more than one thing occur as a result of an event. This feature, called `EventChain`, requires that things occur sequentially. In a complex JavaScript environment like OWF, more than one element of the page can participate in the change. This example shows overriding the *beforeclose* event to confirm whether or not to close the widget. When firing an event to perform an action on the widget, always unregister the event first to prevent looping. The event can be re-registered later._

##Unregister a State Event

To stop monitoring state events, the events must be unregistered. The `WidgetState` object provides two methods for unregistering events:

* `removeStateEventListeners` - allows a widget to stop listening to specified events. 
* `removeStateEventOverrides` - allows the user to stop overriding events. 

Both methods take a JSON object that has two attributes: `events` and `callback`. `events` is an array of event names to unregister. This is an optional attribute and defaults to all events. `callback` is a callback function that does something specific with the event once it has been unregistered. 

```javascript
        …
        eventMonitor.widgetState.removeStateEventListeners({
        	events: [event],
        	callback: function() {
        		…
        	}
        });
        …
        eventMonitor.widgetState.removeStateEventOverrides({
        	events: [event],
        	callback: function() {
        		…
        	}
        });
```

##Retrieve a List of Registered Events for the Widget

The `WidgetState` object provides a method called `getRegisteredStateEvents` that returns an array of events to which the widget may subscribe.

```javascript
        …
        eventMonitor.registeredEvents = eventMonitor.widgetState.getRegisteredStateEvents({
        	callback: function(events) {
        		for (var i = 0; i < events.length; i++) {
        			…
        		}
        	}
        });
        …
```

##Retrieve the Current State of the Widget

The `WidgetState` object provides a method called `getWidgetState` that returns a JSON object describing the current state of the widget. This is useful because when events are received, *only* the `eventName` is passed. Therefore, this method is used to determine what state attributes, if any, may have changed.

```javascript
        …
        var currentState = eventMonitor.widgetState.getWidgetState({
        	callback: function(state) {
        		…
        	}
        });
        …
```

#5   Additional Considerations
##Required Includes

Here is the complete list of scripts needed to successfully use the Widget State API:

```html
        <link href="../css/dragAndDrop.css" rel="stylesheet" type="text/css">
        <script type="text/javascript" src="https://servername:port/owf/js-min/owf-widget-min.js"></script>
        <script type="text/javascript">
              //The location is assumed to be at /<context>/js/eventing/rpc_relay.uncompressed.html if it is not set
              //Ozone.eventing.Widget.widgetRelayURL = '/<context>/js/eventing/rpc_relay.uncompressed.html';
        </script>
```

Replace all occurrences of `https://servername:port` with the name of the server where OWF is running, for example, `https://www.yourcompany.com:8443`. Replace all occurrences of `<context>` with the root context of your Web application. 

##Discussion of State Events

The table below lists the common state event names and their descriptions.

**Table: Widget State Events**

<table>
  <tr>
    <th>Event Name</th>
    <th> Description</th>
  </tr>
  <tr>
    <td>activate</td>
    <td>Fires after the widget has been visually activated.</td>
  </tr>
  <tr>
    <td>add</td>
    <td>Fires after a component has been added to the widget.</td>
  </tr>
  <tr>
    <td>added</td>
    <td>Fires after a component has been added to the widget. (same as add)</td>
  </tr>
  <tr>
    <td>afterlayout</td>
    <td>Fires when the components in this widget are arranged by the associated layout manager.</td>
  </tr>
  <tr>
    <td>afterrender</td>
    <td>Fires after the widget has been rendered, postprocessed by any afterRender method defined for the widget, and, if stateful, after state has been restored.</td>
  </tr>
  <tr>
    <td>beforeactivate</td>
    <td>Fires before the widget is visually activated.</td>
  </tr>
  <tr>
    <td>beforeadd</td>
    <td>Fires before any Ext.Component is added or inserted into the widget.</td>
  </tr>
  <tr>
    <td>beforeclose</td>
    <td>Fires before the widget is closed.</td>
  </tr>
  <tr>
    <td>beforecollapse*</td>
    <td>Fires before the widget is collapsed. (Portal layout only)</td>
  </tr>
  <tr>
    <td>beforedeactivate</td>
    <td>Fires before the widget is visually deactivated.</td>
  </tr>
  <tr>
    <td>beforedestroy</td>
    <td>Fires before the widget is destroyed.</td>
  </tr>
  <tr>
    <td>beforeexpand*</td>
    <td>Fires before the widget is expanded. (Accordion and Portal layouts only)</td>
  </tr>
  <tr>
    <td>beforehide</td>
    <td>Fires before the widget is hidden.</td>
  </tr>
  <tr>
    <td>beforeremove</td>
    <td>Fires before any Ext.Component is removed from the widget.</td>
  </tr>
  <tr>
    <td>beforerender</td>
    <td>Fires before the widget is rendered.</td>
  </tr>
  <tr>
    <td>beforeshow</td>
    <td>Fires before the widget is shown.</td>
  </tr>
  <tr>
    <td>beforestaterestore</td>
    <td>Fires before the widget state is restored.</td>
  </tr>
  <tr>
    <td>beforestatesave*</td>
    <td>Fires before the widget state is saved. This happens when the widget attributes change (i.e. changes size or position, expands, collapses, is maximized or minimized, or when the title is changed).</td>
  </tr>
  <tr>
    <td>bodyresize*</td>
    <td>Fires after the widget has been resized.</td>
  </tr>
  <tr>
    <td>close</td>
    <td>Fires after the widget has been closed. This event is only useful if a widget is monitoring another widget’s events.</td>
  </tr>
  <tr>
    <td>collapse*</td>
    <td>Fires after the widget is collapsed. (Accordion and Portal layouts only)</td>
  </tr>
  <tr>
    <td>deactivate*</td>
    <td>Fires after the widget has been visually deactivated.</td>
  </tr>
  <tr>
    <td>destroy</td>
    <td>Fires after the widget has been destroyed. This event is only useful if a widget is monitoring another widget’s events.</td>
  </tr>
  <tr>
    <td>disable</td>
    <td>Fires after the widget has been disabled.</td>
  </tr>
  <tr>
    <td>drag*</td>
    <td>Fires while the widget is being dragged. This event fires constantly during the drag so it is not recommended to use it. A better alternative is to use the dragstart and dragend events.</td>
  </tr>
  <tr>
    <td>dragend*</td>
    <td>Fires after the widget has been dragged.</td>
  </tr>
  <tr>
    <td>dragstart*</td>
    <td>Fires after the widget has started to be dragged.</td>
  </tr>
  <tr>
    <td>enable</td>
    <td>Fires after the widget has been enabled.</td>
  </tr>
  <tr>
    <td>expand*</td>
    <td>Fires after the widget has been expanded. (Accordion and Portal layouts only)</td>
  </tr>
  <tr>
    <td>hide</td>
    <td>Fires after the widget has been hidden.</td>
  </tr>
  <tr>
    <td>iconchange</td>
    <td>Fires after the widget icon class has been set or changed.</td>
  </tr>
  <tr>
    <td>maximize</td>
    <td>Fires after the widget has been maximized.</td>
  </tr>
  <tr>
    <td>minimize</td>
    <td>Fires after the widget has been minimized.</td>
  </tr>
  <tr>
    <td>move*</td>
    <td>Fires after the widget has been moved.</td>
  </tr>
  <tr>
    <td>remove</td>
    <td>Fires after an Ext.Component has been removed from the widget.</td>
  </tr>
  <tr>
    <td>removed</td>
    <td>Fires after an Ext.Component has been removed from the widget.</td>
  </tr>
  <tr>
    <td>render</td>
    <td>Fires after the widget markup has been rendered.</td>
  </tr>
  <tr>
    <td>resize*</td>
    <td>Fires after the widget has been resized.</td>
  </tr>
  <tr>
    <td>restore</td>
    <td>Fires after the widget has been restored.</td>
  </tr>
  <tr>
    <td>show</td>
    <td>Fires after a hidden widget has been shown.</td>
  </tr>
  <tr>
    <td>staterestore*</td>
    <td>Fires after the widget state has been restored.</td>
  </tr>
  </tr>
  <tr>
    <td>statesave*</td>
    <td>Fires after the widget state has been saved. This happens when the widget attributes change (i.e. changes size or position, expands, collapses, is maximized or minimized, or when the title is changed).</td>
  </tr>
  <tr>
    <td>titlechange*</td>
    <td>Fires after the widget title has been changed.</td>
  </tr>
</table>

> _Note: The events marked with an asterisk (*) should usually be coupled with the `getWidgetState` method of the `WidgetState` object to be more useful._