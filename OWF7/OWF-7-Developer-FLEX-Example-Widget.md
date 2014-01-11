#  FLEX Example

The Flex sample widgets demonstrate how **.SWF** files built using the Adobe Flex framework can be integrated into OWF. It consists of two independent widgets – the Flex Pan Widget and the Direct Widget.

The Flex Pan Widget demonstrates the integration of a Flex Rich Internet Application with OWF. The application displays a large image of the Earth and allows Users to zoom and scroll around the image. The Flex Pan Widget exposes eventing interfaces to control pan and zoom control.

The Flex Pan Widget subscribes to the **map.command** channel for the following messages:

* zoomIn
* zoomOut
* panUp
* panDown
* panLeft
* panRight

The Flex Pan Widget publishes to the **map.mouse** channel for mouse coordinates in the format:

{ absX : 100, absY : 110, localX : 200, localY : 500 }

The abs coordinates are relative to the map image and local coordinates are relative to the widget's window.
 
The Flex Pan Widget subscribes to the **map.marker** channel for messages that post markers on the map image. The format for a **map.marker** message is:

{ x: 100, y: 200 } 

This event payload will put a map marker at 100, 200 on the map. Markers are persisted to the database using the Preferences API.

The Flex Direct Widget connects to the Flex Pan Widget via the eventing mechanism to control the panning and zooming. It also displays the current mouse position.

#1   Technologies

The following is required to build/deploy this example:

* A Java JDK installation of 1.6 or higher.
* Flex SDK 3.4 or 3.5
* A J2EE container such as Tomcat, Jetty or JBoss.

#2   Building/Compilation

1. Extract **\flex-widget.zip** into a new directory.
2. Open **build.xml** and set the `FLEX_HOME` property. 

 For example: 

```xml
        <property name="FLEX_HOME" value="C:\Development\Flex" />
```

 By default, the widget looks for the framework JavaScripts on localhost. The location of the source must be modified in both the **src/main/webapp/direct.html** and the **src/main/resources/custom-template/templates/html-templates/express-installation-with-history/index.template.html** files to reflect the actual location of the OWF server: 

```html
        <script type="text/javascript" language="javascript" src="https://localhost:8443/owf/js-min/owf-widget-min.js"></script>
```

3. Replace all occurrences of `https://servername:port` with the name of the server where OWF is running, for example, `https://www.yourcompany.com:8443`. Additionally, be sure to verify that the windowname library paths point to the local installation. Moreover, the **src/main/webapp/direct.html** and **src/main/resources/custom-template/templates/html-templates/express-installation-with-history/index.template.html** instantiate the `Ozone.eventing.widget` object, which takes the path to the RPC relay file as an argument. The path used must be from the context root of the local widget. 

4. Open a command prompt and navigate to the directory created in Step 1.

5. Type ANT. The resulting **owf-sample-flex.war** file will be in the target directory and can be deployed to the widget server. To test that these widgets work properly together, follow the walkthrough in [Adding a Widget to OWF](OWF-7-Developer—Adding-a-Widget-to-OWF) to create widget definitions which point to **pan.html**, and then assign and apply the widget using the following widget definitions.

**Table: Flex Pan Widget Definition Text**

    Definition   | Data Input Field
  -------------  | -------------
             URL | http://widget-server-name:port/owf-sample-flex/pan.html
    Large Icon   | http://widget-server-name:port/owf-sample-flex/images/pan.gif
    Small Icon   | http://widget-server-name:port/owf-sample-flex/images/pansm.gif
           Width | 800
          Height | 400

Repeat step 1 for the **direct.html** widget. Use the following data for widget definitions:

**Table: Flex Monitor Direct Widget Definition Text**

    Definition   | Data Input Field
  -------------  | -------------
             URL | http://widget-server-name:port/owf-sample-flex/direct.html
    Large Icon   | http://widget-server-name:port/owf-sample-flex/images/direct.gif
    Small Icon   | http://widget-server-name:port/owf-sample-flex/images/directsm.gif
           Width | 300
          Height | 305

Launch both widgets and use the functions on each widget to see how navigational commands and locations are shared between the two widgets.

#3   Supporting Drag and Drop in Flex Widgets

This walkthrough uses Flex Channel Listener and Flex Channel Shouter example widget behavior to explain the Widget Drag and Drop API. 

> _Note: This guide assumes developers understand how to develop Flex applications using Adobe Flash Builder and are using the Flex Channel Listener and Flex Channel Shouter sample widgets that are included with OWF._

**Step 1: Import Required Files**

This includes:

* Files mentioned in the **Required Includes** section found on the [Widget Drag and Drop API](OWF-7-Developer—Widget-Drag-and-Drop-API) page.
* `DragAndDropSupport.as` action script file that enables drag and drop in Flex widgets. 

 A. Find it in the `etc/widget/flash-dragAndDrop/ozone/owf/dd/DragAndDropSupport` directory.
 
 B. Copy the `etc/widget/flash-dragAndDrop/ozone` directory to the `flex-channel-shouter/src` and `flex-channel-listener/src` directory.

**Step 2: Enable Flex Drag and Drop Support**

Create an instance of `DragAndDropSupport` class when the `applicationComplete` event fires. Set the `wmode` of Flex app to "`".

Example **listener.mxml** and **shouter.mxml**:

```xml
        <s:Application xmlns:fx="http://ns.adobe.com/mxml/2009" 
        			   xmlns:s="library://ns.adobe.com/flex/spark" 
        			   xmlns:mx="library://ns.adobe.com/flex/mx"
        			   minWidth="400" minHeight="400"
        			   applicationComplete=" applicationCompleteHandler(event)"> 
        <fx:Script>
        		<![CDATA[
        ...
        protected function applicationCompleteHandler(event:FlexEvent):void {
        	var dd:DragAndDropSupport = DragAndDropSupport.getInstance(stage);
        }
        ...
        </fx:Script>

        	...
	
        </s:Application>
```
 
Example **index.template.html**:

```html
        <script type="text/javascript">
                    ...
                    params.allowfullscreen = "true";
                    params.wmode = "opaque";
                    var attributes = {};
                    ...
        </script>
```

**Step 3: Add Code to Initialize Widget Drag and Drop API**

Register the widget to Drag and Drop API by calling `OWF.DragAndDrop.setFlashWidgetId` method and passing the id of the app. 

```html
        <script>
    
            OWF.ready(function() {
            	OWF.DragAndDrop.setFlashWidgetId("${application}");
            });
    
            ...

        </script>
```

**Step 4: Attach Flex mouseDown Listener to Drag Operation**

To start a drag operation, a mouse down listener must be attached to a Flex Component:

* In the Flex Channel Shouter example, it is the "Drag" button. 
* In the **mouseDown** listener, execute the public javascript fuction, `startDrag`, using Flex's `ExternalInterface`. `startDrag` function in turn calls `OWF.DragAndDrop.startDrag` which starts the drag and notifies other widgets that a Drag has been started in a widget.

```html
        index.template.html:

        <script>
    
            OWF.ready(function() {
            	OWF.DragAndDrop.setFlashWidgetId("${application}");
            });

            function startDrag(channel) {
                OWF.DragAndDrop.startDrag({
                    dragDropLabel: channel,
                    dragDropData: channel
                });
            }
    
            ...

        </script>

        shouter.mxml:

        <fx:Script>
        	<![CDATA[
			
                        protected function button1_mouseDownHandler(event:MouseEvent):void
                        {
                                if(channel_name.text == "")
                                        return;
				
                                event.preventDefault();
                                event.stopPropagation();
				
                                ExternalInterface.call('startDrag', channel_name.text);
                        }

                        ...

                ]]>
        </fx:Script>

        ...
                <s:Button label="Drag" mouseDown="button1_mouseDownHandler(event)"/>
        ...
```

**Step 5: Respond to Drag and Drop Events**

Choose a Flex component to be a Drop Zone (an area that accepts a Drop). 

> _Note: In the Flex Channel Listener, the Drop Zone is the List Panel below the "Add Channel" and "Remove Channel" buttons._

Drag and Drop API allows callback functions that respond to three events: `dragStart`, `dragStop` and `drop`. 

* The `dragStart` event is fired whenever a Drag is initiated. This was done in Flex Channel Shouter by calling the `startDrag` function in the `mousedown` listener. 
* Flex Channel Listener responds to the `dragStart` by highlighting the Drop Zone to show that it is a drop location. 
* In `dragStart` callback, execute the `onDragStart` function which is exposed by the Flex Widget. Also, execute the `updateInteractiveObjects` method which is exposed by the `DragAndDropSupport` class. This is a required step to make drag and drop work as expected in Flex widgets:

```html
        index.template.html:

        <script>

        	OWF.ready(function() {
            		...
    	
            		OWF.DragAndDrop.onDragStart(function(msg) {
                    		OWF.Util.getFlashApp().onDragStart();
                    		OWF.Util.getFlashApp().updateInteractiveObjects();
                	}); 
        
        		...
                 	});

        </script>

        listener.mxml:

        protected function applicationCompleteHandler(event:FlexEvent):void {
        	...
       
        	// expose onDragStart so that it can be called from JavaScript
        	ExternalInterface.addCallback('onDragStart', function():void {
        		channelsBG = "0x00adef";
        	});

        	...
        }
```

* Like the name implies, `dragStop` fires when a Drag stops. This happens when a user releases the mouse button inside or outside a widget. In Flex Channel Listener, the highlighted Drop Zone will stop highlighting if a `dragStop` occurs.

```html
        index.template.html:

        <script>

        	OWF.ready(function() {
    		        ... 
        
        		OWF.DragAndDrop.onDropStop(function() {
        			OWF.Util.getFlashApp().onDragStop();
        		});
		
        		...
        	});

        </script>

        listener.mxml:

        protected function applicationCompleteHandler(event:FlexEvent):void {
        	...
       
        	// expose onDragStop so that it can be called from JavaScript
        	ExternalInterface.addCallback('onDragStop', function():void {
        		channelsBG = "0xffffff";
        	});

        	...
        }
```

* A drop fire when a Drag and Drop operation is successful. The callback assigned to this event executes with the data originally passed to the `startDrag` function.

```html
        index.template.html:

        <script>

        	OWF.ready(function() {
            		... 
        
        		OWF.DragAndDrop.onDrop(function() {
        			OWF.Util.getFlashApp().onDrop(msg.dragDropData);
        		});
		
        		...
        	});

        </script>

        listener.mxml:

        protected function applicationCompleteHandler(event:FlexEvent):void {
        	...
       
        	// expose onDrop so that it can be called from JavaScript
        	ExternalInterface.addCallback('onDrop', onDropReceive);
        	...
        }

        public function onDropReceive(data:Object):void {
        	listenToChannel(data as String);
        }
```

#4   Known Issues

Flex has a known issue with DHTML and z-index ordering. The default wmode for Flex is “window”. It also allows for two other options; transparent and opaque. In order for Flex widgets to adhere to the proper z-index ordering the wmode must be set to something other than the default. 

To reduce the impact of the z-index issue, the OWF team added a `useShims` property to **OwfConfig.groovy**. To turn it on, change the parameter to true. 

Flex widgets may use a JavaScript file named **history.js**. This JavaScript file may throw a JavaScript error in Internet Explorer when a Flex widget is launched. To fix this replace the code below with code in the following section.

Existing code:

![section 13.4.4 codeblock 1](OWFImages/OWF7/dev_guide_13.4.4_codeblock_1.png)

Replacement code: 

![section 13.4.4 codeblock 2](OWFImages/OWF7/dev_guide_13.4.4_codeblock_2.png?raw=true)