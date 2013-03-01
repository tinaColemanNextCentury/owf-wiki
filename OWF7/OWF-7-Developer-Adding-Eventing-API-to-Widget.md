#   Adding the Eventing API to the Widget

#1   Overview

In order to create rich, interactive and integrated presentation-tier workflows, widgets must be able to communicate with each other; this is done via Eventing. The Eventing Framework is a client-side browser communication mechanism that allows widgets to communicate with each other by using an asynchronous publish-subscribe messaging system.

Widgets have the ability to send and receive data on specifically named channels. All widgets can be built so they can publish messages to any channel, just as all widgets can be built to subscribe to any channel at any time.

There are two main components to the Eventing Framework. First is the supporting infrastructure within each dashboard that routes messages. This piece is already implemented by OWF, and is mentioned only to explain how the Eventing infrastructure works. Second, and of more direct interest to widget developers, is the infrastructure available to each widget, detailed below.

#2   Walkthrough

This walkthrough will go through the process of creating a new widget called SecondTracker. The new widget will use the Eventing API to track how many seconds the Announcing Clock Widget has been running. See the **Walkthrough** section found on the [Creating a Widget](OWF-7-Developer-Creating-a-Widget) page for more information on the proposed directory structure.

> _Note: The full code can be found in **SecondTracker.html** located in the OWF Sample Widgets bundle under the `\html-widgets.zip\src\main\webapp\clock`._

1. **Copy relay file**
 
  From the unzipped bundle, go to the `\javascript\eventing` folder, and copy the file **rpc_relay.uncompressed.html**. Paste it into the `owf-server-bundle\samples\html-widget\src\main\webapp` folder. 

2. **Create the SecondTracker Widget**

   In the `webapp` folder, create a file called **SecondTracker.html**. Copy and paste the following code into the file:

 ```html
        <html>
        <head>
            <title>Second Tracker</title>
        </head>
        <body>
            <div class="widgetContents">
                <div class="panel-header">
                    Second Tracker
                </div>
        
                <div class="panel-body">
                    <table class="messagePanel">
                        <tr>
                            <td width="50%">Current Time:</td>
                            <td> <span id="currentTime"></span><br/> </td>
                        </tr>
                        <tr>
                            <td width="50%">Connection Uptime (s):</td>
                            <td> <span id='minutesOnline'>0</span> </td>
                        </tr>
                        <tr>
                            <td width="50%"> Received on channel: </td>
                            <td> <span id="channelName"></span> </td>
                        </tr>
                    </table>
                <div id="tracker-error-panel" class="error-panel">
                    <span id="error"></span>
                </div>
                </div>
            </div></body>
        </html>
 ```

3. **Import the JavaScript files**

  To add the Eventing API to the widget, include the event manager script and its dependencies. To do this, copy and paste the following script tags into the head of the **SecondTracker.html** file:

 ```html
        <script type="text/javascript" src="https://servername:port/owf/js-min/owf-widget-min.js"></script>
 ```

   Replace all occurrences of `https://servername:port` with the name of the server where OWF is running, for example, `https://www.yourcompany.com:8443`. 

 > _Note: The **owf-widget-min.js** file may be replaced with the debug version and may be hosted locally. Refer to the section **OWF Bundled Java Script** and its subsections (located on the [Creating a Widget](OWF-7-Developer-Creating-a-Widget) page) for more details on owf-minified files._

4. **Add code that uses the Eventing API to subscribe to a channel**

  Copy and paste the following code into the head of the **SecondTracker.html** file:

 ```html
        <script type="text/javascript">
          //The location is assumed to be at /<context>/js/eventing rpc_relay.uncompressed.html if it is not set
          OWF.relayFile = '/owf-sample-html/js/eventing/rpc_relay.uncompressed.html';

           function trackerInit() {           
            document.getElementById('currentTime').innerHTML = new Date();

            var launchConfig = OWF.Launcher.getLaunchData();

            if(!launchConfig) {
            // Not launched
            document.getElementById("error").innerHTML = "Widget was launched manually";
            document.getElementById("tracker-error-panel").style.display = 'block';

             // Receive clock broadcast in a default manner
             OWF.Eventing.subscribe(“ClockChannel”, this.update);
         }
         else {
            // We are expecting the channel to listen on to be passed in dynamically.
            // Update it on the page
            var launchConfigJson = OWF.Util.parseJson(launchConfig);
            var channelToUse = launchConfigJson.channel;

            document.getElementById("channelName").innerHTML = channelToUse;   
               
            // intialize the time clock on the page.
            document.getElementById('currentTime').innerHTML = new Date();

            // Make sure we do not see the error panel
            document.getElementById("tracker-error-panel").style.display = 'none';
            
            OWF.Eventing.subscribe(channelToUse, this.update);
         }
        }


        /**
          * The function called every time a message is received on the eventing channel
          */
          var update = function(sender, msg) {
          var count = parseInt(document.getElementById('minutesOnline').innerHTML);
          count = count +1;
          document.getElementById('minutesOnline').innerHTML = count;
          document.getElementById('currentTime').innerHTML = msg;
        };
      
        owfdojo.addOnLoad(function() {
          OWF.ready(trackerInit);
        });

        </script>
 ```

 The code above performs several functions:  

    A. The `relayFile` is configured by setting **OWF.relayFile** to the location of the file. (In the above example **owf-sample-html** is assumed to be the root context.) The developer must replace `/owf-sample-html/js/eventing` with the correct relative location of the **rpc_relay.uncompressed.html** file (see the note below for more information).

    > _Note: Pay attention to the OWF relay file argument. In order to work correctly, the relay **file must be specified with full location details, but without a fully qualified path**. In the case where the relay is residing at **http://server/path/relay.html**, the path used must be from the context root of the local widget. In this case, it would be **/path/relay.html**. Do not include the protocol._

    Within the first method, `trackerInit`, the widget subscribes to the channel ClockChannel, passing in its update function.  To do this, include additional logic that determines if SecondTracker was launched using the WidgetLaunch API. Please see the [Widget Launcher API](OWF-7-Developer-Widget-Launcher-API) page for additional details.

    B. The second method, update, serves as a callback for the Eventing framework. Whenever a message is broadcast on the channel that the update function was subscribed to (in this case, ClockChannel), the function will be invoked. All Eventing callback functions should take two arguments - sender and message. When the update function is fired, the count is incremented, and the `innerHTML` of the `currentTime` span is updated to reflect the message sent by the clock.

    C. The third method contains code to be executed when the page loads.
`OWF.ready` is called when the page loads by the line below:

        owfdojo.addOnLoad(function() {
        	OWF.ready(trackerInit);
        });

   Opening the SecondTracker widget ( **http(s)://servername:port/announcing-clock/SecondTraker.html** ) in a browser should look similar to the following figure.

![SecondTracker Widget](OWFImages/OWF7/secondtracker_widget.png)

**Figure: SecondTracker Widget**

**5. Update the Announcing Clock Widget to use the Eventing API to publish to a channel**

The AnnouncingClock must be updated to publish messages on the expected channel. 
Replace the code in the **AnnouncingClock.html** file with the following:

 ```html
        <html>
        <head>
        <title>Announcing Tracker</title>

        // This line includes the debug API included in the AnnouncingClock’s sample webapp directory.
        // In a production environment and an OWF bundle, owf-widget-debug.js is located in the 
        // /owf/js-min directory.
        <script type="text/javascript" src="../js/owf-widget-debug.js"></script>

        <script type="text/javascript">
            //The location is assumed to be at /<context>/js/eventing/rpc_relay.uncompressed.html if it is not set
            OWF.relayFile = '/owf-sample-html/js/eventing/rpc_relay.uncompressed.html';

            var logger = OWF.Log.getDefaultLogger();
            var appender = logger.getEffectiveAppenders()[0];
   
            // Enable logging 
            appender.setThreshold(log4javascript.Level.INFO);
            OWF.Log.setEnabled(false);


            function updateClock() {
                var currentTime = new Date ( );
         
                var currentHours = currentTime.getHours ( );
                var currentMinutes = currentTime.getMinutes ( );
                var currentSeconds = currentTime.getSeconds ( );
         
                // Pad the minutes and seconds with leading zeros, if required
                currentMinutes = ( currentMinutes < 10 ? "0" : "" ) + currentMinutes;
                currentSeconds = ( currentSeconds < 10 ? "0" : "" ) + currentSeconds;
         
                // Choose either "AM" or "PM" as appropriate
                var timeOfDay = ( currentHours < 12 ) ? "AM" : "PM";
         
                // Convert the hours component to 12-hour format if needed
                currentHours = ( currentHours > 12 ) ? currentHours - 12 : currentHours;
         
                // Convert an hours component of "0" to "12"
                currentHours = ( currentHours == 0 ) ? 12 : currentHours;
         
                // Compose the string for display
                var currentTimeString = currentHours + ":" + currentMinutes + ":" + currentSeconds + " " + timeOfDay;
         
                // Update the time display
                document.getElementById("clock").firstChild.nodeValue = currentTimeString;

                OWF.Eventing.publish("ClockChannel", currentTimeString);

                // Log a message 
                if (currentSeconds % 10 == 0) {
                logger.debug(currentTimeString);
                }

            }

            function initPage() { 
                updateClock();

                msg = 'Running in OWF: ' + (OWF.Util.isRunningInOWF()?"Yes":"No");

                document.getElementById("message-panel").innerHTML = msg;
                document.getElementById("message-panel").style.display = 'block';

                setInterval('updateClock()', 1000 )
            }

            owfdojo.addOnLoad(function() {
              OWF.ready(initPage);
            });
            </script>
        </head>
        <body>
          <div class="widgetContents">

                    <div class="panel-header">
                        Announcing Clock
                    </div>

                    <div id="error-panel" class="error-panel">
                    </div>

                    <div class="panel-body">
                      <div class="clock-frame">
                          <span id="clock">&nbsp;</span>
                      </div>
                    </div>

                    <div class="button-panel">
                    </div>

                    <div id="message-panel" class="message-panel">
                    </div>

                </div>

            </body>

        </html>
 ```

 Notice, that the following JavaScript has been added into the head of the **AnnouncingClock.html** file created in the **Walkthrough** section located on the [Creating a Widget](OWF-7-Developer-Creating-a-Widget) page:

        <script type="text/javascript" src="../js/owf-widget-debug.js"></script>

 > _Note: In production environments, `owf-widget-debug.js` is found in the `js-min` directory._

 The updateClock function has been modified to publish the current time. See the code snippet below:

        OWF.Eventing.publish("ClockChannel", currentTimeString);

 Once complete, any widget that subscribes to ClockChannel will receive messages broadcast from this widget. Once this widget is closed, the broadcast will stop.
The full code can be found in **AnnouncingClock_Eventing.html** located in the OWF Sample Widgets bundle under the  `\html-widgets.zip\src\main\webapp\clock` directory.

**6. Deploy changes**

  To implement the changes, deploy the **SecondTracker.html** and the modified **AnnouncingClock.html** files to the Web application server. 

The deployment method used depends on the Web application server. Usually it can be done by re-bundling the .war file with the new **SecondTracker.html** and **AnnouncingClock.html** files and then copying the **.war** file into the `\webapps` directory on the Web application server. See the Web application server documentation for information on the best practices for deploying changes.

**7. Add the SecondTracker and Announcing Clock Widgets to OWF**

  For the Eventing to function correctly, add the **SecondTracker.html** and the modified **AnnouncingClock.html** files to OWF via the OWF Administration page. For details on how to do this, see [Adding a Widget to OWF](OWF-7-Developer-Adding-a-Widget-to-OWF).

**8. Testing the SecondTracker and Announcing Clock Widgets in OWF**

  To launch and test the newly modified widgets, deploy them on OWF. For details, please see the **Walkthrough** section on the [Adding a Widget to OWF](OWF-7-Developer-Adding-a-Widget-to-OWF) page.

#3   Additional Considerations
##Channel Conventions

It is important to use a unique channel name so widgets are not accidentally published or subscribed to a pre-existing channel. One approach is to use a hierarchical naming pattern with the levels of the hierarchy separated by a dot (.). To form a unique channel, prefix the channel name with a customer domain name reversing the component order. For example, if developing a widget for a company with the domain name of mycompany.com, the channel name’s prefix would be com.mycompany. From that point, naming conventions for an individual’s organization can be used to complete the channel name.

##Required Includes
Here is the complete list of scripts needed to successfully use the Eventing API:

```html
        <link href="../css/dragAndDrop.css" rel="stylesheet" type="text/css">
        <script type="text/javascript" src="https://servername:port/owf/js-min/owf-widget-min.js"></script>
        <script type="text/javascript">
                //The location is assumed to be at /<context>/js/eventing/rpc_relay.uncompressed.html if it is not set
                //OWF.relayFile = '/<context>/js/eventing/rpc_relay.uncompressed.html';
        </script>
```

Replace all occurrences of `https://servername:port` with the name of the server where OWF is running, for example, `https://www.yourcompany.com:8443`. Replace all occurrences of `<context>` with the root context of your Web application.

##Payload Conventions - Data Encoding and RESTful Eventing

It is acceptable to directly encode the data broadcasted on Eventing channels as a simple string. This approach works when sending only a single variable. While a flat string would require the least amount of overhead, it leads to rigid code in the data, especially if the complexity of the sent data increases, because the code that parses the string may not be flexible. In that case, refactoring the message payload may break contract with established listening widgets.

Sending JSON objects with the data directly embedded is an approach that leads to considerably more flexible code. This process allows for the adding of additional data without having to recode widgets that may not have been updated to communicate with the most current version of the broadcasting widget.

While simple strings and JSON objects will work well for many use cases, there are two situations in which widget developers can run into issues:

1. The information that is being sent has potential security concerns.
2. The size of information to be passed is large (such as a data set with hundreds of rows). Sending large quantities of information across the client browser can cause memory and performance issues.

The solution in both cases is to send a reference to the information rather than the information itself. The standardized best practice for sending said information is to send a REST URI encoded as a JSON object that contains the correct way to look up this information. The JSON object would then be parsed by the receiving widget and acted upon appropriately.

Currently, the standardized JSON object has only one field, dataURI. Later versions of this standard may contain additional fields. Adhering to this standard will ensure that other OWF compliant widgets will be able to communicate effectively.

A sample JSON object with a REST URI is described below:

        {
            dataURI: ‘https://server/restful/path/to/object’
        }

For a widget to make information available to other OWF widgets, by exposing a REST API, it is important to guarantee that REST information will be accessible via cross-domain through AJAX calls. By default, many browsers will prevent such a call from succeeding and therefore developers must take explicit steps to make their application function correctly.

The recommended approach is to use Dojo’s *window.name* technique. The Dojo windowname library is already included with OWF as it is the solution that OWF uses to make cross-domain AJAX calls to the Preference API.

More details can be found about the window.name technique here: [http://www.sitepen.com/blog/2008/07/22/windowname-transport/](http://www.sitepen.com/blog/2008/07/22/windowname-transport/)

Two additional techniques that developers may wish to take into consideration are:

* JSONP, details of which can be found here: [http://bob.pythonmac.org/archives/2005/12/05/remote-json-jsonp/](http://bob.pythonmac.org/archives/2005/12/05/remote-json-jsonp/)
* Subspace, details of which can be found here: [http://www2007.org/papers/paper801.pdf](http://www2007.org/papers/paper801.pdf) 

##Eventing Browser Limitations

Microsoft Internet Explorer 7 has a maximum URL length of 2,083 characters.
See the the Microsoft knowledge base article for more information [http://support.microsoft.com/kb/208427](http://support.microsoft.com/kb/208427).

Prior to OWF 5, this limit on the URL would also limit the maximum size of the Eventing message payload in Internet Explorer 7. However in the current version of OWF upgrades were made to allow more than 2000 characters to be sent. This was accomplished by breaking up the large messages into smaller chunks, each less than 2000 in size, and sending each chunk individually. This approach allows larger messages to be sent at the cost of performance. It is still recommeneded to follow guidelines in the **Payload Conventions - Data Encoding and RESTful Eventing** section due to the concerns described in that section.

##Eventing API Enhancements

OWF automatically enables eventing and drag and drop. By automatically enabling eventing, a widget in a floating window (like the Desktop or Tabbed Dashboards) activates when a user clicks inside it. Without eventing, users would have to click once to focus the widget and then click a second time to activate it. Eventing also activates drag and drop indicators. For example, a widget will activate when a user drags the mouse over it. 