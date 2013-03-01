#   Adding Logging to the Widget
#1   Overview

The OZONE Widget Framework (OWF) supports diagnostic and error logging at a number of logging levels. While testing widgets in development, the log window can display log messages that have been output by the application. As mentioned, this capability is intended to be used for developers in building and testing their widgets and is not recommended for end-users in a production environment.

 ![Log Window Screen]  
 (OWFImages/OWF7/log_window_screen_400x313.png)

**Figure: Log Window Screen**

> _Note: In order to see the **.log4** JavaScript popup window, be sure to set the browser in use to allow popups for the duration of the debugging session._

#2   Walkthrough

This walkthrough will go through the process of enabling OWF console logging and adding log messages to the Announcing Clock widget initially created in the **Walkthrough** section of the [Creating a Widget](OWF-7-Developer-Creating-a-Widget) page.

**Step 1: Import the Proper JavaScript Files**

OWF uses the JavaScript file **log4javascript.js** to handle logging. To include the capability in the widget, add the following script tags to the head of the **AnnouncingClock.html** file.

```html
        <script type="text/javascript" src="https://servername:port/owf/js-min/owf-widget-min.js"></script>
```

Replace all occurrences of `https://servername:port` with the name of the server where OWF is running, for example, `https://www.yourcompany.com:8443`. 

**Step 2: Define the Logger**

To define the logger, add the following script to the head of the **AnnouncingClock.html** file:

```html
         <script type="text/javascript">
         	var logger = OWF.Log.getDefaultLogger();
         </script>
```

**Step 3: Override Default OWF Log Settings**

By default, logging is disabled throughout OWF. To enable logging, add the following code to the script in the previous step:

```javascript
        Ozone.log.setEnabled(true);
        	var appender = logger.getEffectiveAppenders()[0];
        	appender.setThreshold(log4javascript.Level.INFO);
```

The method `OWF.Log.setEnabled(true)` is defined in the **log.js** file that was imported in Step 1. It is this method which turns on the logging functionality. 

The log messages will be written to the appender, which in this case is a pop-up window that launches within OWF. The `setThreshold` method is defined in the **log4javascript.js** file that was imported in Step 1 of this overview, and is responsible for setting the logging level. There are six levels of logging. These levels are described in the table in the **Logging Levels** section.

The logging script is shown below in its entirety:

```javascript
        <script type="text/javascript">
              	var logger = OWF.Log.getDefaultLogger();
              	OWF.Log.setEnabled(true);
              	var appender = logger.getEffectiveAppenders()[0];
              	appender.setThreshold(log4javascript.Level.INFO);
       </script>
```

**Step 4: Add Log Message to the Widget**

To actually display a log message in the Announcing Clock Widget, add the following code to the JavaScript in the **AnnouncingClock.html** file:

```javascript
        logger.<logLevel>(<logMessage>);
```

Be sure that the `<logLevel>` is the log level described in the previous step and `<logMessage>` is the message to be printed out.

The full code for this walkthrough can be found in **AnnouncingClock_Logging.html** located in the OWF bundle under the `samples\html-widgets.zip\src\main\webapp\clock` directory.

**Step 5: Deploy Changes**

The modified **AnnouncingClock.html** file must be deployed to the Web application server in order for the changes to take effect. The deployment method used depends on the Web application server being used. Usually the process is as simple as copying the **.war** file into the `webapps` directory on the Web application server. In the event that a particular application server has different requirements, the appropriate Java application server documentation should be consulted for information on how the **.war** file should be deployed.

#3   Additional Considerations
##Logging Levels

There are six levels of logging. These levels are described in the table below:

**Table: Log Levels**

            Level   | Purpose
        -------------  | -------------
          TRACE | Indicates a level of logging which depicts program flow. For example, Entry/Exit of functions along with loop or condition statements. In general, this is used for tracking down specific problems, but may be removed once the problem has been solved.
          DEBUG | Outputs information that may be useful to developers running the application.
          INFO | Outputs information that may be useful for users and may be helpful in tracking down issues with a deployed system.
          WARN | Displays error conditions that can be successfully handled and do not cause the application to perform unexpectedly.
          ERROR | Displays errors that prevent the application from executing in a successful fashion.
          FATAL | Displays conditions that cause the application from failing to load or are about to cause the application to cease operating.

For more information about the format of the log messages visit: [http://log4javascript.org/docs/manual.html](http://log4javascript.org/docs/manual.html)

##Widget Load Time Logging
To record the time it takes for a widget to open, OWF ships with the parameters `sendWidgetLoadTimesToServer` and `publishWidgetLoadTimes` set to “true”: 

        sendWidgetLoadTimesToServer = true
        publishWidgetLoadTimes = true

The two parameters are located in **OwfConfig.groovy** in the `apache-tomcat-7.0.21\lib` folder of OWF bundle. They operate separately. The `publishWidgetLoadTimes` parameter writes to the Widget Log widget automatically. For the `sendWidgetLoadTimesToServer` to record data on the server in **\apache-tomcat-7.0.21\logs\ozone-widgeting-framework.log**, the log level value in **\apache-tomcat-7.0.21\lib\owf-override-log4j.xml** must be set to “info.” See the following example:

```xml
        <root>
        	<level value="info" />
        	<appender-ref ref="owf-async" />
        </root>
```

> _Note: To increase performance, OWF ships with the root log level set to “error.”_

To stop recording the load time in either location, change “true” to “false” and redeploy **OwfConfig.groovy**. 