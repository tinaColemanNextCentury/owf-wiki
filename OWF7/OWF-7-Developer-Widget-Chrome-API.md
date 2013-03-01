#  Widget Chrome API
#1   Overview

This walkthrough will address the Widget Chrome API. For the purposes of this document, “chrome” refers to the visible frame which often surrounds a window or Web pages, as seen in the image below:

![Widget Chrome Example](OWFImages/OWF7/widget_chrome_example_463x435.png)

**Figure: Widget Chrome Example**

The OWF Bundle includes an example widget that uses the Widget Chrome API. The example widget adds buttons and a menubar to the chrome upon opening. Developers can configure the buttons and menubar by modifying the **widgetChromeData.js** file found in `/apache-tomcat-7.0.21/webapps/owf/examples/walkthrough/widgets`. Normally, a widget should not use an external JavaScript file for this information. However, as a training tool, this Widget Chrome example allows developers to add buttons and menus to the widget’s chrome. 

Follow the directions on the [Adding a Widget to OWF](OWF-7-Developer-Adding-a-Widget-to-OWF) page to create a widget definition which points to **WidgetChrome.gsp**. Then, assign the widget to a user and apply the widget to one of the user’s dashboards. Use the following data for the widget definition:

**Table: Data for Widget Chrome API**

<table>
    <tr>
      <th>Definition</th>
      <th>Data Input Field</th>
      </th>
    </tr>
    <tr>
       <td>URL</td>
       <td>http://widget-server-name:port/owf/examples/walkthrough/widgets/WidgetChrome.gsp</td>
    </tr>
    <tr>
       <td>Large Icon</td>
       <td>http://widget-server-name:port/owf/examples/walkthrough/images/chromeWiget_blue_icon.png</td>
    </tr>
    <tr>
       <td>Small Icon</td>
       <td>http://widget-server-name:port/owf/examples/walkthrough/images/chromeWiget_blue_icon.png</td>
    </tr>
    <tr>
       <td>Width</td>
       <td>540</td>
    </tr>
    <tr>
       <td>Height</td>
       <td>440</td>
    </tr>
</table>

> _Note: Widgets added to a fit pane layout will not have chrome. Therefore, functionality added to widget chrome buttons and menus will not be accessible to widgets in that layout._

#2   Walkthrough

**Step 1: Import the Proper JavaScript Files**

The **WidgetChrome.gsp** uses the minified OWF bundle, which can be included from the location below:

```javascript
        <script type="text/javascript" src="https://servername:port/owf/js-min/owf-widget-min.js"></script>
```

Replace all occurrences of `https://servername:port` with the name of the server where OWF is running, for example, `https://www.yourcompany.com:8443`. 

The minimum required include list needed to use the Widget State API is described in the section, **Using the Widget State API with the Widget Chrome API**. 

```javascript
        {
          xtype: 'button',
          //path to an image to use. this path should either be fully qualified or relative to the /owf 
          icon: './themes/owf-ext-theme/resources/themes/images/owf-ext/skin/exclamation.png',
          text: 'Alert',
          itemId:'alert',
          tooltip: {
           text: '<b>Alert!</b>'
          },
          handler: function(sender, data) {
           //widgetState is an already instantiated WidgetState Obj
           if (widgetState) {
            widgetState.getWidgetState({
              callback: function(state) {
               //check if the widget is visible
               if (!state.collapsed && !state.minimized && state.active) {
                //render visual content here
               }
              }
            });
           }
          }
         }
```

**Step 2: Add Code to Initialize Eventing and OWF.Chrome object** 

The Widget Chrome API requires the use of Eventing. 

        …
        	OWF.ready(init);
        …

**Step 3: Add a Button**

The Widget Chrome API has functions which allow for the adding or removing of buttons on the widget chrome. To apply, simply call these functions with a proper configuration object:

* `addHeaderButtons` — adds buttons to the right of the standard widget buttons
* `insertHeaderButtons` — adds buttons to any position in the button area
* `updateHeaderButtons` — updates any previously added buttons specified
* `removeHeaderButtons` — removes any previously added buttons specified
* `listHeaderButtons` — lists previously added buttons
* `isModified` — allows the developer to determine if the widget chrome has been modified

For example, see the `insertHeaderButtons` usage below. 

        …
         OWF.Chrome.insertHeaderButtons({items:[{
          type: 'gear',
          itemId:'gear',
          handler: function(sender, data) {
           Ext.Msg.alert('Utility', 'Utility Button Pressed');
          }}]
         });
        …

**Step 4: Add a Menu**

The Widget Chrome API can add and remove menus on a menubar that starts under the widget title. To apply, use the correct configuration object:

* `addHeaderMenus` — adds menus to a menubar beneath the widget chrome
* `insertHeaderMenus` — adds menus to any position on the menubar
* `updateHeaderMenus` — updates any previously added menus specified
* `removeHeaderMenus` — removes any previously added menus specified
* `listHeaderMenus` — lists all previously added menus
* `isModified` — allows the developer to determine if the widget chrome has been modified

For example, see the `insertHeaderMenus` usage below. 

```javascript
        …
         OWF.Chrome.insertHeaderButtons({
           items:[{
              itemId:'menu1',
              icon: './themes/common/images/skin/exclamation.png',
              text: 'Menu 1',
              menu: {
                 items: [{
                    itemId:'menu1_menuItem1',
                    icon: './themes/common/images/skin/exclamation.png',
                    text: 'Menu Item 1',
                    handler: function(sender, data) {
                       alert('You clicked Menu Item 1 from Menu 1.');
                    }
                 }]
              }
           }]
         });
        …
```
#3   Button Configuration

The `addHeaderButtons`, `insertHeaderButtons`, `updateHeaderButtons` and `removeHeaderButtons` functions take a configuration object as a parameter. This configuration object allows the developer to define one or more buttons. 

The structure of this button configuration is very similar to buttons in general ExtJS development. See the code block below for a simple example. The button example uses built in ExtJS button types. The example below is of the type `‘gear’`, which means a standard gear icon will be used. There are several standard types which are defined by ExtJS. Each type has a corresponding image which is appropriately styled and sized for the current theme. For a complete list of types please see the [ExtJS 4.x API documentation](http://docs.sencha.com/ext-js/4-0/#/api/Ext.panel.Tool-cfg-type).

```javascript
        {
        //this item’s array is required. It allows you to pass one more button configurations
        items: [{
          //gear is a standard ext tool type. It has a standard icon
          type: 'gear',
  
          //required – itemId - this must be unique among all buttons
          itemId:'gear',
  
          //handler function for when the button is pressed.
          handler: function(sender, data) {
           alert('Utility', 'Utility Button Pressed');
          }
         }]
        }
```

To define a button with a custom image, set the icon property to the URL of the image.

```javascript
        {
        items: [
         {
          xtype: 'widgettool',
          icon: './themes/owf-ext-theme/resources/themes/images/owf-ext/skin/information.png',
          itemId:'help',
          handler: function(sender, data) {
           alert('About', 'About Button Pressed');
          }
         }
        ]
        }
```

The ‘`widgettool`’ xtype does not allow text or a tooltip to be added to the button. To define a button with text or a tooltip use the `‘button’` xtype. 

```javascript
        {
        items: [
         {
          xtype: 'button',
          icon: './themes/owf-ext-theme/resources/themes/images/owf-ext/skin/exclamation.png',
          text: 'Alert',
          itemId:'alert',
          tooltip: {
           text: '<b>Alert!</b>'
          },
          handler: function(sender, data) {
           alert('Alert', 'Alert Button Pressed');  }
         }
        ]
        }
```

Below is a full description of all the fields supported in a button configuration.

```javascript
        {
        //this items array is required it allows you to pass one more button configurations
        items: [
         {
          //required - itemId this must be unique among all buttons
          itemId:'alert',

          //optional – widgettool (default), button
          xtype: 'button',

          //optional – if xtype is ‘widgettool’ type defines a standard ExtJS icon
          type: ‘help’,

          //optional – if the xtype is ‘widgettool’ the type property will determine the icon
          icon: './themes/owf-ext-theme/resources/themes/images/owf-ext/skin/exclamation.png',

          //optional – text to display. Text is only displayed for ‘button’ xtype
          text: 'Alert',

          //optional tooltip – only displays for ‘button’ xtype
          tooltip: {
           text: '<b>Alert!</b>'
          },
          //optional handler for when the button is clicked
          handler: function(sender, data) {
           Ext.Msg.alert('Alert', 'Alert Button Pressed');
          }
         }
         ]
        }
```

* `itemId` - This is a unique id among all buttons that are added. It is a required property. It is used for identification and defines the internal Eventing channel which is used to execute the `handler` function. If `itemId` is not unique, this may result in duplicate buttons which may not be able to be removed properly.
* `xtype` - This is an ExtJS property used to determine the component to create. Currently the Widget Chrome API only supports two xtype values: `‘button’` and `‘widgettool’`. `xtype` is an optional field, if it is omitted, `‘widgettool’` is used.
* `type` - This property is used only for `‘widgettool’` buttons. It determines the standard icon to be used. For a complete list of types please see the [ExtJS 4.x API documentation](http://docs.sencha.com/ext-js/4-0/#/api/Ext.panel.Tool-cfg-type).
* `icon` - This property defines the URL of the image to be used for the button. If the URL is a relative path, it will be relative to the `/owf` context. This is useful if the desired image is hosted by the OWF Web server. Otherwise a fully qualified URL should be used. If `type` is being used to determine the image, the icon property is optional.
* `text` - This property defines text to appear alongside the button. This property is only used if the xtype is `‘button’`. `‘widgettool’` will not show text.
* `tooltip` - This property defines an ExtJS tooltip. It has two important sub properties, `title` and `text`. `tooltip` is only used when the `xtype` is `‘button’`.
* `handler` - The handler attribute defines a function to be executed when the button is pressed. This function is executed using Widget Eventing API from inside the widget. The internal channel name used is the `itemId` attribute. This function’s parameter list contains the standard parameters for an Eventing callback function.

#4   Menu Configuration##

The following functions pass in a configuration object as a parameter to define one or menus: 

* `addHeaderMenus` 
* `insertHeaderMenus` 
* `updateHeaderMenus`
* `removeHeaderMenus`

The structure of this menu configuration is very similar to menu buttons in general ExtJS development. See the code block below for a simple menu example. 

```javascript
        {
        //this item’s array is required. It allows you to pass one more menu configurations
        items: [{
          //required – id that is unique among all menus, sub-menus, and menu items
          itemId:'menu1',

          //optional – text to display on as the menu label
          text: 'Menu 1',

          //required – menu configuration
          menu: {
            // required - array of menu item configurations
            items: [{
              //required – id that is unique among all menus, sub-menus, and menu items
              itemId:'menuItem1',

              //optional – text to display as the menu item label
              text: 'Menu Item 1',

              //optional – function to be executed when menu item is clicked
              handler: function(sender, data) {
                alert('Alert', Menu Item 1 Selected');
              }
            }]
          }
         }]
        }
```

To define a menu with a custom image, set the icon property to the URL of the image.

```javascript
        {
        items: [{
          itemId:'menu1',
          text: 'Menu 1',
          menu: {
            items: [{
              itemId:'menuItem1',
              icon: './themes/owf-ext-theme/resources/themes/images/owf-ext/skin/exclamation.png',
              text: 'Menu Item 1',
              handler: function(sender, data) {
                alert('Alert', Menu Item 1 Selected');
              }
            }]
          }
         }]
        }
```

OWF allows menus on the widget chrome to have an infinite number of sub-menus. To define a menu with a sub-menu, simply replace the `handler` attribute of the menu item configuration with a menu configuration object.

```javascript
        {
        items: [{
          itemId:'menu1',
          text: 'Menu 1',
          menu: {
            items: [{
              itemId:'menuItem1',
              icon: './themes/owf-ext-theme/resources/themes/images/owf-ext/skin/exclamation.png',
              text: 'Menu Item 1',
              menu: {
                itemId:'submenu1',
                icon: './themes/owf-ext-theme/resources/themes/images/owf-ext/skin/exclamation.png',
                text: 'Sub-menu 1',
                items: [{
                  itemId:'submenuItem1',
                  icon: './themes/owf-ext-theme/resources/themes/images/owf-ext/skin/exclamation.png',
                  text: 'Sub-menu Item 1',
                  handler: function(sender, data) {
                    alert('Alert', Sub-menu Item 1 Selected');
                  }
                }]
              }
            }]
          }
         }]
        }
```

Below is a full description of all the fields supported in a menu configuration.

```javascript
        {
        //this items array is required it allows you to pass one more menu configurations
        items: [
         {
          //required – id that is unique among all menus, sub-menus, and menu items
          itemId:'menu1',

          //optional – URL of icon to appear to the left of the menu text 
          icon: './themes/owf-ext-theme/resources/themes/images/owf-ext/skin/exclamation.png',

          //optional – text to display as the menu label
          text: Menu 1,

          //required – menu configuration
          menu: {
            // required - array of menu item configurations
            items: [{
              //required – id that is unique among all menus, sub-menus, and menu items
              itemId:'menuItem1',

              //optional – text to display as the menu item label
              text: 'Menu Item 1',

              //optional – function to be executed when menu item is clicked
              handler: function(sender, data) {
                alert('Alert', Menu Item 1 Selected');
              }
            }]
          }
         }
         ]
        }
```

* `itemId` - This is a unique id among all menus, sub-menus, and menu items that are added. It is a required property for all menus, sub-menus, and menu items that are added. It is used for identification and defines the internal Eventing channel which is used to execute the `handler` function. If `itemId` is not unique the handler may not execute properly.
* `icon` - This property defines the URL of the image to be used for the menu. It is an optional property for all menus, sub-menus, and menu items that are added. If the URL is a relative path, it will be relative to the `/owf` context. This is useful if the desired image is hosted by the OWF Web server. Otherwise a fully qualified URL should be used. 
* `text` - This property defines text to appear as the menu label. While this property is optional for all menus, sub-menus and menu items that are added, it is suggested that either this or the icon property or both be specified.
* `menu` - This property defines an ExtJS menu configuration. It has one important sub property, `items`. `items` is an array of ExtJS menu item configurations. In addition to the `itemId`, `icon` and `text` properties described above, the items included in the `items` array have two important sub properties, `handler` and `menu`. Either `handler` or `menu` should be specified for each `menu` item, but not both.
   * `handler` - The `handler` attribute defines a function to be executed when the menu item is pressed. This function is executed using Widget Eventing API from inside the widget. The internal channel name used is the `itemId` attribute. This function’s parameter list contains the standard parameters for an Eventing callback function.
   * `menu`- This property defines an ExtJS menu configuration. Specifying this property will create a sub-menu.

#5   Grouping Menu Items

ExtJS provides a menu separator to divide logical groups of menu items. There are two ways to add a separator bar to a menu:  Insert ‘-‘ or the following configuration into the items array:

```javascript
        {
          xtype: 'menuItem1'
        }
```

The following code block shows a sample menu configuration that includes two menu separator bars.

```javascript
        {
        items: [{
          itemId:'menu1',
          text: 'Menu 1',
          menu: {
            items: [{
              itemId:'menuItem1',
              icon: './themes/owf-ext-theme/resources/themes/images/owf-ext/skin/exclamation.png',
              text: 'Menu Item 1',
              handler: function(sender, data) {
                alert('Alert', Menu Item 1 Selected');
              }
            },{
              itemId:'menuItem2',
              icon: './themes/owf-ext-theme/resources/themes/images/owf-ext/skin/exclamation.png',
              text: 'Menu Item 2',
              handler: function(sender, data) {
                alert('Alert', Menu Item 2 Selected');
              }
            },{
              xtype: ‘menuseparator’ // add a menu separator
            },{
            },{
              itemId:'menuItem3',
              icon: './themes/owf-ext-theme/resources/themes/images/owf-ext/skin/exclamation.png',
              text: 'Menu Item 3',
              handler: function(sender, data) {
                alert('Alert', Menu Item 3 Selected');
              }
            }, 
            ‘-‘, // add a menu separator
            {
              itemId:'menuItem4',
              icon: './themes/owf-ext-theme/resources/themes/images/owf-ext/skin/exclamation.png',
              text: 'Menu Item 4',
              handler: function(sender, data) {
                alert('Alert', Menu Item 4 Selected');
              }
            }]
            }
           }]
          }
```

#6   Changing the Widget’s Title

The API allows the widget’s title to be retrieved and changed. To retrieve the widget’s title, see the example below:

```javascript
    OWF.Chrome.getTitle({
                         callback: function(msg) {
                             //msg will always be a json string
                             var res = Ozone.util.parseJson(msg);
                             if (res.success) {
                                 var alert = Ext.Msg.show({
                                     title: 'Get Title',w
                                     msg: res.title,
                                     buttons: Ext.Msg.OK,
                                     closable: false,
                                     modal: true
                                 });
                             }
                         }
    		     });
```

To set the widget’s title see the example below:

```javascript
        OWF.Chrome.setTitle({
                               title: text,
                               callback: function (msg) {
                               //msg will always be a json string
                                   var res = Ozone.util.parseJson(msg);
                                   if (res.success) {
                                        //confirm res.title has changed or do something else
                                   }
                               }
                            });
```

#7   Additional Considerations
##Using the Widget State API with the Widget Chrome API

Custom buttons and menus added to the widget may be clicked at any time. This includes times when a widget is hidden, collapsed or minimized. This may cause issues for `handler` functions which are executed when the button/menu is pressed. If a `handler` function displays new visual content, it is possible that the function will result in an error, or the new visual content will be rendered incorrectly. To avoid this issue, it is recommended to use the Widget Chrome API and the Widget State API together. Using the Widget State API will allow the widget to recognize whether it is visible or not. See code below for an example:

```javascript
         {
          xtype: 'button',
          //path to an image to use. this path should either be fully qualified or relative to the /owf 
          icon: './themes/owf-ext-theme/resources/themes/images/owf-ext/skin/exclamation.png',
          text: 'Alert',
          itemId:'alert',
          tooltip: {
           text: '<b>Alert!</b>'
          },
          handler: function(sender, data) {
           //widgetState is an already instantiated WidgetState Obj
           if (widgetState) {
            widgetState.getWidgetState({
              callback: function(state) {
               //check if the widget is visible
               if (!state.collapsed && !state.minimized && state.active) {
                //render visual content here
               }
              }
            });
           }
          }
         }
```

##Required Includes

The following code block is the complete list of scripts needed to successfully use the Widget Chrome API:

```html
        <link href="../css/dragAndDrop.css" rel="stylesheet" type="text/css">
        <script type="text/javascript" src="https://servername:port/owf/js-min/owf-widget-min.js"></script>
        <script type="text/javascript">
              //The location is assumed to be at /<context>/js/eventing/rpc_relay.uncompressed.html if it is not set
              //OWF.relayFile = '/<context>/js/eventing/rpc_relay.uncompressed.html';
        </script>
```

Replace all occurrences of `https://servername:port` with the name of the server where OWF is running, for example, `https://www.yourcompany.com:8443`. Replace all occurrences of `<context>` with the root context of your Web application.