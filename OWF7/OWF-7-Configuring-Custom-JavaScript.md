#Customizing OWF JavaScript
OWF uses JavaScript, CSS bundling, minification, compression and caching in order to optimize the downloading of resources to the browser. Nearly all JavaScript and CSS resources which get downloaded to the browser have a unique version string in their names. This allows the OWF server to tell the browser to permanently cache these name-specific resources.

Where it was previously necessary to open the **owf.war** file to edit the JS files in order to customize OWF across all themes, it is now possible to make many common modifications externally without extracting the **owf.war** file.

An external JavaScript plugins folder for customizations is included in the bundle at `apache-tomcat-7.0.21/lib/js-plugins`, already containing the most commonly modified OWF JavaScript files. Any code inside the `init` method of these files will be run following the initialization of their parent file of the same name inside the **owf.war** file.

The following files are included in the bundle and ready to customize. The table explains which components in OWF will change when the corresponding files are customized:
 
<b>Table: External JavaScript Files for Customizing OWF</b>
    
<table>
    <tr>
      <th>Filename</th>
      <th>Description of
Customization</th>
    </tr>
    <tr>
      <td>Banner.js</td>
      <td>OWF banner on initialization, as well as functions that listen to the banner’s dock and undock events</td>
    </tr>
    <tr>
      <td>Dashboard.js</td>
      <td>All dashboard types on initialization through their parent class</td>
    </tr>
    <tr>
      <td>DashboardContainer.js</td>
      <td>The container that holds all dashboard types on initialization</td>
    </tr>
    <tr>
      <td>WidgetBase.js</td>
      <td>The widget base, which includes the header</td>
    </tr>
    <tr>
      <td>WidgetPanel.js</td>
      <td>The inner panel of widgets, below the widget header</td>
    </tr>
    <tr>
      <td>WidgetWindow.js</td>
      <td>The containing window for widgets</td>
    </tr>
</table>

> _Note: Though it is still possible to open the **owf.war** file, edit files, and recreate the WAR to customize OWF, the external method is recommended to ensure code separation as well as to make it easier to upgrade to future versions of OWF. Accordingly, only modify JavaScript inside the **owf.war** file if the desired file to customize is not in the `js-plugins` folder._

#1   Configuring the External JavaScript Files
The external JavaScript plugins folder will only be included in OWF if the steps in the **Deploy or Recreate External JavaScript/CSS** section are recompiled to include them, unless OWF is opened in debug mode. Since it requires action on the part of the implementer to utilize, there is no configuration property to quickly turn it on or off.

There is, however, a configuration parameter to set the name and location of the external folder to use in debug mode, which is located in the **OwfConfig.groovy** file located at `apache-tomcat-7.0.21/lib/`. The `owf.external.jsPluginPath` property controls where OWF looks for the external JavaScript files when in debug mode. The default setting of this property is “classpath:js-plugins,” so when OWF is rendered in debug mode, it will look in the classpath, which includes the `apache-tomcat-7.0.21/lib/` folder, for the `js-plugins` folder and include its JavaScript files in the list returned to the client. This default location is depicted in the code snippet below, along with examples of other configuration options:

```javascript
    owf {
      //Locations for the optional external themes and help directories.
      //Default: 'themes', 'help', and 'js-plugins' directories on the classpath.
      //Can be configured to an arbitrary file path.  The following
      //path styles are supported:
      //  'file:/some/absolute/path' ('file:C:/some/absolute/path' on Windows)
      //  'classpath:location/under/classpath'
      //  'location/within/OWF/war/file'
        external{ 
            themePath = 'classpath:themes'
            helpPath = 'classpath:help'
            jsPluginPath = 'classpath:js-plugins'
        }
      ...
    }
```

#2 Deploy or Recreate External JavaScript/CSS
In order to deploy any changes made to external files inside the `js-plugins` folder to the OWF server, the minified JavaScript files must be recompiled to include the external files. The instructions for including the external JavaScript files are as follows:

1.      Shut down the OWF server if it is currently running.
2.	From the command line, change the working directory to the `etc/tools`.
3.	 Execute the `create-web-bundles` script to include the external files in the minified JavaScript files inside the **owf.war** file.
    * A.	On a Windows system, use the following command: 

            create-web-bundles.bat -o ..\..\apache-tomcat-7.0.21\webapps\owf.war -js ..\..\apache-tomcat-7.0.21\lib\js-plugins
    * B.	On a Unix system, use the following command:

            bash create-web-bundles.sh -o ../../apache-tomcat-7.0.21/webapps/owf.war -js ../../apache-tomcat-7.0.21/lib/js-plugins
4.	Navigate to the `apache-tomcat-7.0.21/webapps` folder and delete the owf folder if it exists.
5.	Start OWF via `start.bat` or `start.sh`. Be sure to clear the browser’s cache to ensure the most recent minified files are being received.

> _Note: For testing purposes, changes made to external JavaScript files can immediately be viewed by opening OWF in debug mode, instructions for which can be found in section 6: **Debugging JavaScript/CSS Problems**._

#3   JavaScript/CSS Bundle Naming Convention
Individual JavaScript and CSS source files are concatenated into bundle files. The bundle files are minified or compressed and versioned. The original source JavaScript and CSS files which make up these bundle files are also included in the WAR for reference and extension. Every JavaScript or CSS source file has a compressed and versioned file, and a GZIP compressed and versioned file. For example the OWF-server JavaScript bundle source file is `js/owf-server.js`. The file is a concatenation of JavaScript files used for the main OWF page and it is readable. However, there are two other versions of the file referenced above:

* Main Source: `js/owf-server.js`
* Versioned and Minified: `js/owf-server__v6.0-GA-24385.js`
* Versioned and Gzip Compressed: `js/owf-server__v6.0-GA-24385.gz.js`

> _Note: The versioned, minified and Gzip compressed file names include a unique id number that changes with each release. In the examples above, the unique id number is 24385._

Every JavaScript and CSS source file follows the above naming convention.
If the filename uses the following naming convention, it is versioned and minified:

    _v<version>.<ext>

If the filename uses the following naming convention, it is versioned and GZIP compressed:

    _v<version>.gz.<ext>

At runtime the OWF Web server will use the versioned and compressed bundle files. If the browser supports GZIP compression the compressed bundle file will be used, otherwise the minified bundle file will be used.

#4  Toolbar Customization Walkthrough
One of the most commonly customized components of OWF is the toolbar, found at the top of the screen. For a specific implementation of OWF, it may be desirable to alter the OWF Toolbar by changing the logo or adding a new component such as a button or search box. This section discusses these modifications and puts forward the recommended approach to achieve them.

##Toolbar Overview
The external toolbar object, `apache-tomcat-7.0.21/lib/js-plugins/Banner.js`, corresponds to its parent, `/js/components/banner/Banner.js`, inside the **owf.war** file. When making customizations to the toolbar, the former, external `Banner.js` should always be the file being modified.

> _Note: For the purposes of this document, the term toolbar refers to the specific section of OWF that is directly above the dashboard space._

The default, non-customized toolbar is shown below.

![OWF Toolbar](OWFImages/OWF7/owf_toolbar.png)

<b>Figure: OWF Toolbar</b>

When separated into configurable sections, the toolbar components are:

![OWF Logo](OWFImages/OWF7/owf_logo.png)

<b>Figure: OWF Logo Area</b>

![Detachable Toolbar](OWFImages/OWF7/detachable_toolbar.png)

<b>Figure: Detachable Toolbar</b>

![Drop-down User Menu](OWFImages/OWF7/drop_down_user_menu.png)

<b>Figure: User Menu</b>

##Customizing the Toolbar Logo
The recommended way to modify the logo across all themes is through the external themes folder located at `apache-tomcat-7.0.21/lib/themes`. The first step is to mimic the structure of the themes folder inside the **owf.war** file by creating folders to achieve the following structure in the external themes folder: `apache-tomcat-7.0.21/lib/themes/common/images/banner/`. Inside the top-most banner folder, the custom logo file must be saved as **logo.png** in order to override the internal file of the same name.

##Adding/Removing Toolbar Components
Through the external `Banner.js` file, developers can add Ext components, such as buttons, menus, and form fields, to the toolbar, as well as modify the appearance and functionality of existing components.

> _Note: Although the toolbar’s default buttons are modifiable, they provide access to core OWF functionality and should be modified with extreme caution. The OWF team does not recommend removing these buttons._

To place custom components on the toolbar, add them to the items array as Ext components. To add custom components to the detached toolbar, get the floating toolbar via the `getPopOutBanner` method of the toolbar object, and then add items to its items array similarly.

The following example of the external `Banner.js` file shows an implementation that adds a search box component to both the docked and floating toolbars:

```javascript
Ext.define('Ozone.plugins.Banner', {
	extend: 'Ext.AbstractPlugin', 

	//Called after Banner.js initComponent() method inside the owf.war file
	init: function(cmp) {

		var banner = cmp;
		var searchAddedToPopOut = false;
		
		//Add a searchbox to the main banner
		this.addSearchBox(banner, banner.items.length - 1);

		//Make a reference to this object for inside the event handler
		var me = this;
		cmp.on('undocked', function() {
			//Check if the searchbox was already added to the pop out banner
			if(!me.searchAddedToPopout) {
				//Get the pop out banner
        		var popOutBanner = banner.getPopOutBanner();

				//Add the search box to the floating banner only after
				//the undock event because prior it may not exist.
				me.addSearchBox(popOutBanner, popOutBanner.items.length - 1);

				me.searchAddedToPopout = true;
			}
		});
	},

	//Function added to add a searchbox to any passed in component at the given position.
	addSearchBox: function(cmp, position) {
		cmp.insert(position, {
            xtype: 'searchbox', //OWF Custom Search Box Component
      		cls: 'custom-searchbox',
            style: {
            	margin: 5
            },
            listeners: {
                searchChanged: {
                    fn: function(cmp, value) {
		               var trimmedVal = Ext.String.trim(value);
		               if (trimmedVal.length > 0) {
                        	alert("You searched on '" + trimmedVal +"'.");
                    	}
                    },
                    scope: this
                }
            }
        });
	  }
    });
```

##Customizing the Toolbar User Menu
The User Menu is represented in the image below. It contains the username, last sign-in date, product information and Sign Out feature. The User Menu is defined inside the **owf.war** file as `/js/components/button/UserMenuButton.js`.

![Drop-down User Menu](OWFImages/OWF7/drop_down_user_menu.png)

<b>Figure: User Menu</b>

By default, the User Menu is not directly externalized with its own file in the `js-plugins` folder, but it is accessible externally via the `js-plugins/Banner.js` file by the following method:

```javascript
    Ext.define('Ozone.plugins.Banner', {
    	extend: 'Ext.AbstractPlugin', 

    	init: function(cmp) {

    		var banner = cmp;

    		//Get the UserMenuButton object
    		var userMenuButton = banner.items.get("userMenuBtn");
    	}
    }); 
```

The User Menu is configurable to add or remove items from it by modifying its `items` array. The items defined in this array are not arbitrary Ext components, but instead are custom objects that can contain the following properties: 

<b>Table: Custom Object Properties for a User Menu Button Item</b>

<table>
    <tr>
      <th>Property</th>
      <th>Description</th>
    </tr>
    <tr>
      <td>clickable: boolean</td>
      <td>If true, the element is clickable and keyboard-focusable and the and function registered as handler fires when it is clicked. (Default: true)</td>
    </tr>
    <tr>
      <td>handler: function</td>
      <td>A JavaScript function to execute when the element is clicked.</td>
    </tr>
    <tr>
      <td>id: String</td>
      <td>Becomes the HTML id of the node that this element creates.</td>
    </tr>
    <tr>
      <td>spacer: boolean</td>
      <td>If true, all other properties are ignored and a vertical spacer element is added to the menu. (Default: false) </td>
    </tr>
    <tr>
      <td>text: String</td>
      <td>The text that is
displayed on this element in the menu.</td>
    </tr>
</table>

#5   Sample Customization
A fully customized toolbar is shown in the image below. All code changes, along with developer notes can be used as examples when trying to modify installations of OWF. In the following example, the OWF logo changed and a search box was added.  

![Customized Toolbar](OWFImages/OWF7/customized_toolbar.png)

<b>Figure: Customized Toolbar</b>

##Custom CSS
To customize the toolbar CSS: 

* If the change applies to all themes: modify the following stylesheet `owf.war/themes/common/stylesheets/_banner.scss`
* If the change is theme specific: modify the following file `owf.war/themes/<theme_name>.theme/sass/<theme_name>.scss`

#6   Debugging JavaScript/CSS Problems
OWF may be configured to not use JavaScript and CSS bundling and compression. Disabling this feature is useful for debugging because the source JavaScript and CSS will be included into the page instead of the bundles. To disable this feature add the line below to `OwfConfig.groovy` and restart OWF.

    uiperformance.enabled = false

It is also possible to disable the JavaScript and CSS bundles at runtime in the browser. To disable the bundling and compression dynamically add `debug=true` to the OWF URL. See below:

    https://localhost:8443/owf/?debug=true

> _Note: If the OWF URL returns an error, it may have appended the dashboard id to include a GUID number. If this error is returned, try adding `#guid=` and the `GUID number` after `true`. 
For example:_ `https://localhost:8443/owf/?debug=true#guid=123456789` 