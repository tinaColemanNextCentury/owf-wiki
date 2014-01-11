#   Widget Drag and Drop API
#1   Overview

This walkthrough will go through the process of using the Widget Drag and Drop API by describing Channel Listener and Channel Shouter example widget behavior. Channel Listener and Channel Shouter are widgets that are included with OWF. In the walkthrough below, Channel Listener and Channel Shouter widgets work together to demonstrate both the Eventing, Widget Launcher and Widget Drag and Drop APIs.

As shown in the image below, Channel Shouter now has a ![Channel Shouter](OWFImages/OWF7/channel_shouter_small.png) icon next to the Channel text box, which has been highlighted in red for the purposes of documentation. If a channel name (in this instance, “Test”) is entered in the text box, clicking and dragging the ![Channel Shouter](OWFImages/OWF7/channel_shouter_small.png) icon will initiate a Drag and Drop for the channel name. A floating drag indicator will appear next to the mouse while the mouse button is depressed - this is represented by the red circle with the minus sign in it, in the Channel Shouter Widget. Additionally, the Active Channels table in the Channel Listener Widget will be highlighted during a drag operation. This indicates a channel may be dropped on it. Once the mouse is over the Active Channels table (the red-lined turquoise rectangle in the Channel Listener window, below) the drag indicator will change and indicate the channel may be dropped. Once a channel name is dropped, the Channel Listener Widget will subscribe to the channel and add it to the Active Channels table. Now a user may use the Channel Shouter Widget to send text to the Channel Listener on the entered channel.

![Drag and Drop](OWFImages/OWF7/drag_and_drop.png)

**Figure: Drag and Drop**

#2   Walkthrough
**Step 1: Import the Proper JavaScript Files**

The **ChannelListener.gsp** and **ChannelShouter.gsp** use the maximum JavaScript import list. However, the minimum required include list needed to use the Widget Drag and Drop API is described in the **Required Includes** section.

**Step 2: Add Code to Initialize Eventing and Widget Drag and Drop API for Channel Shouter**

The Widget Drag and Drop API requires the use of Eventing. To get an `OWF.DragAndDrop` JavaScript object, wrap the JavaScript that requires it in `OWF.ready`. See **ChannelShouter.gsp**, for example:

       …
        	OWF.ready(shoutInit);
        …

**Step 3: Attach an " *onmousedown* " Listener to Start the Drag Operation**

To start a Drag operation, a mousedown listener must be attached to a DOM node in the widget. In the Channel Shouter example, this DOM node is the ![Channel Shouter](OWFImages/OWF7/channel_shouter_small.png) icon next to the Channel text box. In the ChannelShouter example, use `dojo` to bind a listener to the *mousedown* event (`owfdojo` is an alias for `dojo`). Other JavaScript libraries have similar syntax to attach listeners or callback functions. Additionally, a listener may be set directly to the "`onmousedown`" attribute of the DOM node.

In the mousedown listener, execute the `doStartDrag` function. Pass to this function an object which contains a label for the Drag indicator, as well as the data to be sent on a successful Drop. See **ChannelShouter.gsp**, below for example:

```javascript
        …
        shoutInit = owfdojo.hitch(this, function() {
        …
                //add handler to text field for dragging
               owfdojo.connect(document.getElementById('dragSource'),'onmousedown',this,function(e) {
                  e.preventDefault();
                  var data = document.getElementById('InputChannel').value;
                  if (data != null && data != '') {
                        OWF.DragAndDrop.startDrag({
                                dragDropLabel: data,
                                dragDropData: data
                        });
                  }
                });
              });
        …
```

**Step 4: Add Code to Initialize Eventing and Widget Drag and Drop API for Channel Listener**

Channel Shouter Widget is now set to start a Drag. Next, set up Channel Listener to accept a Drop. Channel Listener must get a `WidgetDragAndDrop` object just like Channel Shouter.  

        Ext.onReady(function() {
        	OWF.ready(function() {
        …
                });
        });
        …

**Step 5: Update Channel Listener to respond to Drag and Drop**

Choose a DOM node to be a Drop Zone—an area that accepts a Drop. In the Channel Listener, the Drop Zone is the Active Channels Table.

Next, update Channel Listener to respond to Drag and Drop Events. `WidgetDragAndDrop` object allows added callback functions that respond to three events: `dragStart`, `dragStop` and `drop`. The `dragStart` event is fired whenever a Drag is initiated. This was done in ChannelShouter by calling the `doStartDrag` function in the mousedown listener. Channel Listener responds to the `dragStart` by highlighting the Active Channels table to show that it is a Drop location.

```javascript
        …
                            OWF.DragAndDrop.onDragStart(function() {
                              cmp.dragging = true;
                              cmp.getView().addCls('ddOver');
                            });
        …
```

`dragStop` is fired when a drag stops. This happens when the mouse button is released inside or outside a widget. In Channel Listener if a `dragStop` event occurs, the Active Channels table stops highlighting.

```javascript
        …
                            OWF.DragAndDrop.onDragStop(function() {
                              cmp.dragging = false;
                              cmp.getView().removeCls('ddOver');
                            });
        …
```

`drop` is fired when a Drag and Drop operation is successful. The callback assigned to this event will be executed with the data originally passed to the *doStartDrag* function. 

```javascript
        …
                            OWF.DragAndDrop.onDrop(function(msg) {
                              this.subscribeToChannel(msg.dragDropData, false);
                            }, this);
        …
```

And finally, the Drag indicator needs to change once the mouse is over the drop zone. This is accomplished by adding *mouseover* and *mouseout* listeners to the Drop Zone. Each listener will call `setDropEnabled` enabling and disabling whether the drag indicator shows whether a drop is allowed.

```javascript
        …
                            var view = cmp.getView();
                            view.el.on('mouseover', function(e, t, o) {
                              if (cmp.dragging) {
                                OWF.DragAndDrop.setDropEnabled(true);
                              }
                            }, this);
                            view.el.on('mouseout', function(e, t, o) {
                              if (cmp.dragging) {
                                OWF.DragAndDrop.setDropEnabled(false);
                              }
                            }, this);
        …
```

#3   Additional Considerations
##Required Includes

Here is the complete list of scripts needed to successfully use the Drag and Drop API:

```html
        <link href="../css/dragAndDrop.css" rel="stylesheet" type="text/css">
        <script type="text/javascript" src="https://servername:port/owf/js-min/owf-widget-min.js"></script>
        <script type="text/javascript">
              //The location is assumed to be at /<context>/js/eventing/rpc_relay.uncompressed.html if it is not set
              //OWF.relayFile = '/<context>/js/eventing/rpc_relay.uncompressed.html';
        </script>
```

Replace all occurrences of `https://servername:port` with the name of the server where OWF is running, for example, `https://www.yourcompany.com:8443`.  Replace all occurrences of `<context>` with the root context of your Web application.

> _Note: The dragAndDrop.css file (enabled for all widgets) can be found at the following location: 
`apache-tomcat-7.0.21\webapps\owf.war\css\dragAndDrop.css`_

##Drag and Drop API Enhancements

The following enhancements have been added to the Drag and Drop API:
* `addCallback` function supports multiple callbacks for the same event. This makes it easier to support multiple drop zones.
* `addDropZoneHandler` function to support multiple drop zones
* By including the **dragAndDrop.css**  during the import of the OWF widget JavaScript bundle,  widgets render a drag indicator during a drag. For information about includes, see section **Required Includes**. 

> _Note: Older versions of OWF limit eventing messages to 2,000 characters while using Internet Explorer 7. This limitation was removed in OWF 5 However, for widgets to receive larger messages, they must use updated OWF 5 widget Javascript files and RPC Relay file that are equipped to receive larger messages._
