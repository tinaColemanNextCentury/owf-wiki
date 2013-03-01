#   HTML Examples

There are seven simple HTML examples that were collectively designed to act as a progressive walkthrough within this guide and OWF. These example widgets are described in the table below:

**Table: HTML Widget Examples**

<table>
    <tr>
        <th>File</th>
        <th> Purpose</th>
    </tr>
    <tr>
        <td>AnnouncingClock.html</td>
        <td>This example is a simple updating clock.</td>
    </tr>
    <tr>
        <td>AnnouncingClock_Eventing.html</td>
        <td>This example broadcasts the time on a specified channel.</td>
    </tr>
    <tr>
        <td>SecondTracker.html</td>
        <td>This example receives and displays the time broadcasted by the AnnouncingClock_Eventing.html widget by listening to a specified channel.</td>
    </tr>
    <tr>
        <td>AnnouncingClock_Preference.html</td>
        <td>This example adds an option to display the clock in military time and saves this preference to the OWF database.</td>
    </tr>
    <tr>
        <td>AnnouncingClock_Logging.html</td>
        <td>This example prints periodic logging messages to a logging popup window.</td>
    </tr>
    <tr>
        <td>AnnouncingClock_Advanced.html</td>
        <td>This example combines the functionality of eventing, preferences, localization, and logging into a single clock widget.</td>
    </tr>
</table>

#1   Technologies

No additional software is required; the Announcing Clock Widget pages can be hosted in any Web server.

#2   Building/Compilation

An ANT build script is provided with the sample HTML Widget. (ANT must be installed to execute this script.) The build script creates the **owf-sample-html.war** file that will be deployed on the Web server. To build the **owf-sample-html.war**: 

1. Extract **/html-widgets.zip** into a new directory.
2. Open a command prompt and navigate to the directory created in Step 1.
3. Type ANT. The resulting **owf-sample-html.war** file will be in the target directory and can be deployed to the widget server.
4. The widgets consist of several HTML pages that can be dropped anywhere on a Web server. By default, the widgets look for the framework JavaScript files on localhost. Accordingly, change their paths to reflect the actual location of the OWF server: 

```html
        <script type="text/javascript" src="https://servername:port/owf/js-min/owf-widget-min.js"></script>
```

5. Replace all occurrences of `https://servername:port` with the name of the server where OWF is running, for example, `https://www.yourcompany.com:8443`. Additionally, be sure to verify that the windowname library paths point to the local installation.

Additionally, the **AnnouncingClock_Eventing.html**, **SecondTracker.html** and **AnnouncingClock_Advanced.html** files instantiate the `Ozone.eventing.widget` object, which takes a path as an argument. The path used must be from the context root of the local widget.

#3   Updating OWF JavaScript Includes

The simplest way to upgrade a widget’s OWF JavaScript includes is to replace all OWF JavaScript includes with the list found in the Widget Best Practices (on the [Creating a Widget](OWF-7-Developer-Creating-a-Widget) page). This mass change will ensure that all JavaScript includes are accounted for. If a smaller list is required for specific functionality, please refer to the appropriate feature section. 

#4   Upgrade Eventing Relay File

New JavaScript libraries have been introduced. These libraries will need to be re-deployed to every Web server which hosts widgets for OWF. The new libraries are located in `\javascript`.

#5   Preference API behavior change

In prior versions of OWF an attempt to retrieve or delete a nonexistent preference resulted in an error. Starting with OWF 3.3, the Preference API considers retrieving or deleting a preference that does not exist, a “success” and calls the `onSuccess` callback with an “undefined” value. For example, the `getUserPreference()` method in the Preferences API will return an empty object when the requested named property is not found.

There have also been a few method changes in the Preference API. The methods `putUserPreference` and `createOrUpdateUserPreference` have been removed in favor of `setUserPreference`. Additionally, all methods now take a JSON configuration object as a parameter. See [Adding the Preferences API to a Widget](OWF-7-Developer-Adding-Preferences-API-to-Widget) for more details.