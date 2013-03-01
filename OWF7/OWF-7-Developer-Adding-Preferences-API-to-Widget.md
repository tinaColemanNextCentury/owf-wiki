# Adding the Preferences API to a Widget
#1   Overview

The OWF Preference JavaScript API provides a convenient mechanism for the widget developer to store user specific data to the OWF database. A user preference is simply a string value that is uniquely mapped to a user, name and namespace combination. In the walkthrough below, a military time checkbox will be added to the Announcing Clock widget developed in the **Walkthrough** section on the [Creating a Widget](OWF-7-Developer-Creating-a-Widget) page.  The state of this check box, whether it has been checked or not, is stored in a user preference. The following is a screenshot of this preference taken from OWF’s Preference dialog:

![Preferences Dialog](OWFImages/OWF7/preferences_dialog.png)

**Figure: Preferences Dialog**

The Namespace should use a hierarchical naming pattern to avoid a naming collision with other widgets. The value can be any string value including JSON. 
The preference API comprises the following:

* `getUserPreference`({namespace: 'namespace', name:'name', onSuccess:onSuccess, onFailure:onFailure}); 
* `setUserPreference`({namespace: 'namespace',name: ' name', value: 'value', onSuccess:onSuccess, onFailure:onFailure}); 
* `deleteUserPreference`({namespace: 'namespace', name:'name', onSuccess:onSuccess, onFailure:onFailure}); 

Each of these methods communicates with the server asynchronously and therefore requires the use of callback functions to provide the results of the requested operation.
The `onSuccess` callback for all three of the above functions expects an argument to be passed in; a JSON object of the following structure:

```javascript
        {	"value":"true",
            "path":"militaryTime",
            "user":
            {
            "userId":"testAdmin1"
            },
            "namespace":"com.mycompany.AnnouncingClock"
        }
```

In `getUserPreference`, this is the preference retrieved. In setUserPreference, this is the preference object to be created. And in deleteUserPreference, this is the object deleted. 

If an object is not found on a `getUserPreference`, an empty JSON object is returned to the onSuccess function, such that it looks like this: 

        {
           // no attributes
        }

If an error occurs, such as a *500: Internal Server Error*, the `onFailure` callback is executed. It has two arguments, as follows:

        function onFailure(errorMessage,statusCode){
            alert('Error ' + errorMessage);
            alert(statusCode);
        }

`errorMessage` is a String describing the issue, while `errorCode` is a numeric code indicating the HTTP error code returned by the server. 

#2   Walkthrough

This walkthrough will expand on the **AnnouncingClock.html** widget created in the **Walkthrough** section on the [Creating a Widget](OWF-7-Developer-Creating-a-Widget) page, by adding a “Military Time” checkbox whose state is stored in the OWF database using the OWF preference JavaScript API.

**Step 1: Copy over Dojo’s window name transport**

Dojo’s window name transport is used for secure cross-domain browser based data transfer. The OWF Preference JavaScript API uses this transport when the widget is hosted on a different Web application server than OWF. This has file resources that should be located in the same Web application server as the widget.

1. Create a `js` directory under the `webapp` directory.
2. Copy the `javascript\dojo-1.5.0-windowname-only` directory from the OWF bundle to the `js` directory created above.

**Step 2: Add the Required Libraries**

The following JavaScript libraries must be added to the **AnnouncingClock.html** and are required for the proper execution of the OWF Preference JavaScript API. Add the following script statements right after the opening head tag:

```html
        <script type="text/javascript" src="https://servername:port/owf/js-min/owf-widget-min.js"></script>
        <script type="text/javascript">
        owfdojo.config.dojoBlankHtmlUrl = '../js/dojo-1.5.0-windowname-only/dojo/resources/blank.html';
        </script>
```

Replace all occurrences of `https://servername:port` with the name of the server where OWF is running, for example, `https://www.yourcompany.com:8443`. Additionally, be sure to verify that the windowname library paths point to the local installation.

**Step 3: Add the Military Time Checkbox**

Add the HTML markup for the check box inside the body tag after `<span id='clock'>&nbsp</span>` (the clock span tag) in the **AnnouncingClock.html** file:

```html
        Use Military Time:<input id="checkboxMilitaryTime" type="checkBox" onClick="militaryTimeCheckboxChanged(this.checked);"/>
```

The *onClick* event will be used to save the state of the check box. 

**Step 4: Persist the Checkbox State**

Add the following code within the script tag:

```javascript
        function onSetFailure(error,status) {
            OWF.Util.ErrorDlg.show("Got an error updating preferences! Status Code: " + status 
                           + ". Error message: " + error);
        };
        function militaryTimeCheckboxChanged(checkedState) {
            this.militaryTime = checkedState;
            OWF.Preferences.setUserPreference(
                {namespace:'com.mycompany.AnnouncingClock',
                 name:'militaryTime',
                 value:checkedState,
                 onSuccess:function(){},
                 onFailure:onSetFailure});
        }
```

> _Note: `OWF.Util.ErrorDlg.show` (as shown in the code block above) is a JavaScript method provided by the OWF team in the **owf/js/util/util.js** file. It launches a blocking error message similar to the built-in JavaScript alert method. Unlike the JavaScript alert method, which blocks use of the entire browser, this dialog will only block the particular widget in question, and NOT the entire browser session. While a developer is free to replace this method with any form of error display of their own, the OWF team STRONGLY discourages the use of the *window.alert* method as it blocks the use of all other widgets in the dashboard._

`OWF.Preferences.setUserPreference` will create or update the following user preferences:

* A *namespace* of ‘com.mycompany.AnnouncingClock’
* A *name* of ‘militaryTime’
* A *value* of either true or false depending on whether or not the military time checkbox is checked 
* The callback function is executed if the user preference is successfully stored in the database. Since no action is required under a successful completion in this walkthrough, we are passing a no-op function.
* The *onFailure* callback function that will display the error message if an error occurs. 

**Step 5: Initialize the Checkbox with the Saved State**

Change the body’s onload event to `clockInit()`:

```html
        <body onload="clockInit(); setInterval('updateClock()', 1000 )">
```

Add the following code within the script tag:

```javascript
        function onGetFailure(error,status) {
            if (status != 404) {
                OWF.Util.ErrorDlg.show("Got an error getting preferences! Status Code: " 
                                       + status + ". Error message: " + error);
            }
        }

        function onGetMilitaryTimeSuccess(pref){
            if (pref.value == 'true'){
                this.militaryTime = true;
               document.getElementById('checkboxMilitaryTime').checked = true;
            }
            else{
                this.militaryTime = false;
                document.getElementById('checkboxMilitaryTime').checked = false;
            }
            updateClock();
        }

        function clockInit (){
            OWF.Preferences.getUserPreference(
                {namespace:'com.mycompany.AnnouncingClock', 
                 name:'militaryTime',
                 onSuccess:onGetMilitaryTimeSuccess, 
                 onFailure:onGetFailure}); 
        }
```

The body’s *onload* event calls the *clockInit* method which retrieves the user’s `com.mycompany.AnnouncingClock.militaryTime` preference asynchronously. After successfully retrieving the user preference, the *getUserPreference* method invokes the *onGetMilitaryTimeSuccess* callback function passing the retrieved preference object. The value is read from the preference object and is used to update the state of the checkbox in the Document Object Model (DOM). 

**Step 6: Update the Time Display to Accommodate Military Time**

Replace the `updateClock` function with the following:

```javascript
        function updateClock ( ){
            var currentTime = new Date ( );
            var currentHours = currentTime.getHours ( );
            var currentMinutes = currentTime.getMinutes ( );
            var currentSeconds = currentTime.getSeconds ( );

            // Pad the minutes and seconds with leading zeros, if required
            currentMinutes = ( currentMinutes < 10 ? "0" : "" ) + currentMinutes;
            currentSeconds = ( currentSeconds < 10 ? "0" : "" ) + currentSeconds;

            var timeOfDay = '';
            // Convert the hours component to 12-hour format if needed
            if (!this.militaryTime)
            {
                // Choose either "AM" or "PM" as appropriate
                timeOfDay = ( currentHours < 12 ) ? "AM" : "PM";
                currentHours = ( currentHours > 12 ) ? currentHours - 12 : currentHours;
                // Convert an hours component of "0" to "12"
                currentHours = ( currentHours == 0 ) ? 12 : currentHours;
            }
            // Compose the string for display
            var currentTimeString = currentHours + ":" + currentMinutes + ":" + currentSeconds + " " + timeOfDay;

            // Update the time display
            document.getElementById("clock").firstChild.nodeValue = currentTimeString;
        }
```

The current time will now be displayed in either regular or military time depending on the state of the military time checkbox. 

**Step 7: Create a .war File**

A **.war** file is a Web application compressed into one file. While directories and files can be copied directly onto the Web server, it is easier, and more common to use a **.war** file.
To create the **.war** file for the announcing clock widget, open a command prompt and navigate to the `webapp` directory. Then run the following command:

        jar cvf announcing-clock.war .

**Step 8: Deploy the .war File to the Server**

The deployment method used depends on the Web application server. Usually it is as simple as copying the **.war** file into the `webapps` directory on the Web application server. See the specific Web application server documentation for information on the best practices for deploying changes.

The widget should now look like this:

![Announcing Clock Widget With Preferences API](OWFImages/OWF7/announcing_clock_widget_with_preferences_api.png?)

**Figure: Announcing Clock Widget With Preferences API**

The code for this walkthrough can be found in **AnnouncingClock_Preference.html** located in the OWF bundle under the `samples\html-widgets.zip\src\main\webapp\clock` directory. 

**Step 9: Testing the SecondTracker and Announcing Clock Widgets in OWF**

To launch and test the newly modified widgets, they must be deployed to OWF. For details, please see [Adding a Widget to OWF](OWF-7-Developer-Adding-a-Widget-to-OWF).

#3   Additional Considerations
##Browser Based Cross Domain Data Transfer

The OWF Preference JavaScript API uses Dojo’s windowname transport to access the OWF application server from externally hosted widgets. See a discussion of the [Dojo window.name transport](http://www.sitepen.com/blog/2008/07/22/windowname-transport/).

The windowname transport is distributed within the OWF bundle and is located in the `\javascript\dojo-1.5.0-windowname-only` directory. However, it is no longer necessary to include these JavaScript files explicitly because they are included in the **owf-widget-min.js** bundle.

The entire contents of the directory should be copied to the local widget’s server. 

##Required Includes

Here is the complete list of scripts needed to successfully use the preference API:

```javascript
        <script type="text/javascript" src="https://servername:port/owf/js-min/owf-widget-min.js"></script>
```

Replace all occurrences of `https://servername:port` with the name of the server where OWF is running, for example, `https://www.yourcompany.com:8443`. Additionally, be sure to verify that the windowname library paths point to the local installation.

##Payload Conventions – JSON/REST Data Encoding 

In order to avoid name collisions with user preferences defined by other widgets, always use a hierarchical naming pattern with the levels of the hierarchy separated by a dot (.). To form a unique namespace, prefix the internet domain name, reversing the component order. For example, if developing a widget for a company with the domain name of **mycompany.com** then the namespace prefix would be **com.mycompany**. From that point, organizational naming conventions can be applied to the rest of the namespace.

To store several pieces of information, multiple user preferences can be created. As an alternative, they can be aggregated into one logical object, converted into a JSON string and stored into one user preference. For example, consider storing a user’s first, middle and last name. Using the first option would require the use of the following three user preferences:

1. **com.mycompany.widget.firstName**
2. **com.mycompany.widget.middleName**
3. **com.mycompany.widget.lastName**

Using the second option would require just one user preference using the following JSON string:

        {“firstName” : “John”,
        “middleName” : “Quincy”,
        “lastName” : “Adams” }

While simple strings and JSON objects will work well for many use cases, there are two situations in which widget developers can run into issues:

1. The information that is being sent has potential security concerns. 
2. The size of information to be passed is large (such as a data set with hundreds of rows). Sending large quantities of information across the client browser can cause memory and performance issues.

The solution in both cases is to send a *reference* to the information rather than the information itself. The standardized best practice for sending said information is to send a REST URI encoded as a JSON object that contains the correct way to look this information up. This object would then be parsed by the receiving widget and acted upon appropriately.

Currently, the standardized JSON object has only one field, `dataURI`. Later versions of this standard may contain additional fields. Adhering to this standard will ensure that other OWF compliant widgets will be able to communicate effectively.

A sample JSON object with a REST URI is described below:

        {
          dataURI: ‘https://server/restful/path/to/object’
        