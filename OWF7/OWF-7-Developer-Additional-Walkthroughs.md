#   Additional Walkthroughs
#1   Overview - Adding the Widget Launcher

> _Note: Please see [Widget Launcher API](OWF-7-Developer—Widget-Launcher-API) for additional information on the primary Widget Launcher exercise._

The supplemental walkthrough will examine and explain how the "Announcing Clock Launcher" and "Second Tracker (Launched Version)" work together. The "Announcing Clock Launcher" will launch "Second Tracker (Launched Version)" and pass to it the name of a channel which "Second Tracker" will then subscribe to and listen for a time-based “seconds” updates. 

A third widget has capabilities which lends itself to this exercise, and that is the "Announcing Clock Dynamic Launcher". It dynamically looks up the GUID of "Second Tracker (Launched Version)" by using the Preferences API.

#2   Walkthrough - Simple Widget Launching

**Step 1: Add Two New Widgets**

A. Name the first widget “Announcing Clock Launcher”

 * Filename: **AnnouncingClock_Launcher.html**
 * URL: **https://localhost:844:/announcing-clock/clock/AnnouncingClock_Launcher.html**

B. Name the second widget “Second Tracker (Launched Version)”

* Filename: **SecondTracker_Launched.html**
* URL: **https://localhost:8443/announcing-clock/clock/SecondTracker_Launched.html**

See [Adding a Widget to OWF](OWF-7-Developer—Adding-a-Widget-to-OWF) for directions on adding a widget to OWF.

**Step 2: Examine the Function "launchSecondTracker"**

![section 14.2 codeblock 1](OWFImages/OWF7/dev_guide_14.2_codeblock_1.png)

Note the bold (and highlighted) GUID, `cb71a25d-d435-4770-ab0f-f33d7db31812`. That GUID needs to be correct so that the Launching API can identify the widget to launch, i.e. "Second Tracker (Launched Version).” 

> _Note: In addition to using the GUID to launch a widget, the Universal Name of the widget can be used as well.  Viewing a widget list or Widget Editor and “turning on” the Universal Name column will display all of the Universal Names for all widgets that have them. See the OWF Administrator’s Guide for more details._

The bold (and highlighted) `OWF.Launcher.launch` text is the actual function call to the Launching API's launch function which launches the "SecondTracker (Launched version)" Widget.

The bold (and highlighted) `// data` to be passed text is the note which precedes the payload of data that is being sent to the launched widget. The payload exists as a JSON object which has been encoded as a string.

The bold (and highlighted) `callbackOnLaunch` text is a parameter which is passed to the launch function. The value of the parameter is a function that gets called when the launch is complete, regardless of whether the launch, regardless of whether the launch failed or was a success. Said callback should be formed as follows:

```javascript
        /**
         * A callback function that gets called after the widget launcher has tried to launch the 
         * new widget and either succeeded or failed.
         */
         function callbackOnLaunch (resultJson)
         {
         var launchResultsMessage = "";
         if(resultJson.error)
         {
         // if there was an error, print that out on the launching widget
         launchResultsMessage += ("Launch Error " + resultJson.message);
         }
         if(resultJson.newWidgetLaunched)
         {
         // if the new widget was launched, say so
         launchResultsMessage += ("New Widget Launched, instance's unique id is " + resultJson.uniqueId);
         }
         else 
         {
         // if the new widget was not launched, say so and explain why not
           launchResultsMessage += ("New Widget Not Launched: " + resultJson.message + 
           " The existing widget instance's unqiue id is " + resultJson.uniqueId);          
                }
        
                document.getElementById("launchResults").firstChild.nodeValue = launchResultsMessage;
              }
```

It is clear how the above function takes the JSON object returned in the function parameter and does something with it; in this specific instance, it displays a status to the user and tells the user what has happened.

**Step 3: Examine "SecondTracker_Launched.html"**

![section 14.2 codeblock 2](OWFImages/OWF7/dev_guide_14.2_codeblock_2.png)

The bold (and highlighted) `var launchConfig = OWF.Launcher.getLaunchData()` text shows this function retrieving the launch configuration from the widget launching API.

The bold (and highlighted) `if(launchConfig...` text checks to see whether the retrieved payload was null. If null, an error will be displayed. The payload would be null, for example if the user had launched the Second Tracker (Launched Version) Widget from the Launch Menu, rather than having it be launched by another widget. 

In the bold (and highlighted) `else` text, the widget parses the payload which has been passed to it, turns it into a JSON object, and retrieves the channel name. 

#3   Walkthrough - Dynamic Widget Launching

**Step 1: Add a New Widget**

A. Name the widget “Announcing Clock Dynamic Launcher”

* Filename: **AnnouncingClock_DynamicLauncher.html** 
* URL: **https://localhost:8443/announcing-clock/clock/AnnouncingClock_DynamicLauncher.html**

**Step 2: Examine the Widget**

```javascript
        var WIDGET_TO_LAUNCH = "Second Tracker (Launched Version)"
```

The line of text above displays the exact name of the widget that “Announcing Clock Dynamic Launcher” is going to be looking for so that it can be launched.

**Step 3: Examine the functions of “Announcing Clock Dynamic Launcher”**

In the text below is the function which allows the widget to search for the GUID is display. This function displays where the widget is searching for the GUID of the widget to launch:

![section 14.3 codeblock](OWFImages/OWF7/dev_guide_14.3_codeblock.png)

In the bold (and highlighted) `searchParams` text, `widgetName` has been hard coded.  The bold (and highlighted) `onSuccess` and `onFailure` above show the two callbacks which can be passed. These are the individual functions which get called on those events.  On success, it simply launches the second tracker:

```javascript
          /**
              * This function launches the second tracker. It's called as a callback from
              * findWidgets on a successful query. 
              */
              function launchSecondTracker(findResultsResponseJSON)
              {
                // get guid
                if(findResultsResponseJSON.length == 0)
                {
                  // no result was found, so the looked up widget name doesn't exist
                  failWidgetLookupError("Widget was not found in user profile. User may not have access.");
                }
                else
                {
                  var guidOfWidgetToLaunch = findResultsResponseJSON[0].path;
         // data to be passed to the widget that is launched.
                  var data = {
                    channel: CHANNEL_NAME
                  };        
                  var dataString = OWF.Util.toString(data);
         // Launch the other widget!
                  OWF.Launcher.launch (
                    {
                      guid: guidOfWidgetToLaunch, // the guid of the widget to launch
                      launchOnlyIfClosed: true, //if true will only launch the widget if it is not already opened.
                      data: dataString // initial launch config data to be passed to 
         // a widget only if the widget is opened. this must be a string!
                    }, 
                    callbackOnLaunch
                  );
                }
              }
```

On failure, it prints an error message: 

```javascript
        /**
              * When the findWidget call fails for some reason, this error handling function
              * displays an error message on the widget
              */
              function failWidgetLookupError(widgetLookupErrorMessage)
              {
                document.getElementById("launchResults").firstChild.nodeValue = 
                 "Launching Failed because this widget was unable to look up the widget called " +
                 WIDGET_TO_LAUNCH + ". Are you sure the widget exists under that name? Error Message: " +
                 widgetLookupErrorMessage;
```