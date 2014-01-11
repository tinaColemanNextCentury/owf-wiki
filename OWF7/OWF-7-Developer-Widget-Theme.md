#   Widget Theme
#1   Overview

This walkthrough uses the Channel Listener example to explain widget theming. It describes how Channel Listener responds to the current OWF Theme. 

Sample widgets that ship with OWF respond to the user’s current OWF theme. However, this section explains how a developer can customize their own widgets to match the default themes used in OWF. 

![Channel Listener Shown in OWF’s Four Default Themes](OWFImages/OWF7/channel_listener_with_4_themes.png)

**Figure: Channel Listener Shown in OWF’s Four Default Themes**

A widget’s implementation determines how its user interface must change to match the OWF themes. Developers using standard HTML/JavaScript widgets should create CSS stylesheets that match OWF themes and use logic to decide which CSS stylesheet to include. This is the approach taken in the Channel Listener example in the next section.
Important points:

* The `name`, `contrastType` and `fontSize` of the current themes are appended to the widget’s URL as `themeName`, `themeContrast` and `themeFontSize`. 
* The value for `themeContrast` will be one of the following choices:
 * `standard` – regular theme 
 * `black-on-white` – indicates the use of high contrast colors: black on top of white
 * `white-on-black` – indicates the use of high contrast colors: white on top of black
* The `themeFontSize` will be an integer indicating the font size of the OWF theme in pixels. 

#2   Walkthrough

When modifying their own widgets: Developers should add logic to **ChannelListener.gsp** that includes the correct CSS based on the current OWF Theme.

To copy an example from the product:
Go to the unpacked **owf.war** and locate **ChannelListener.gsp** in the `apache-tomcat-7.0.21\webapps\owf\examples\walkthrough\widgets` folder.

> _Note: Notice that `ChannelListener` is implemented as a GSP file. It allows the Web server to change the included CSS file depending on the OWF theme. In this scenario `ChannelListener` has a specifically named CSS file for each possible OWF theme._

```html
        <html>
        	<head>
            <title>Channel Listener</title>
        
              <g:if test="${params.themeName != null && params.themeName != ''} ">
                <link rel='stylesheet' type='text/css' href='../../../themes/${params.themeName}.theme/css/${params.themeName}.css' />
              </g:if>
              <g:else>
                <link href="../../../js-lib/ext-4.0.7/resources/css/ext-all.css" rel="stylesheet" type="text/css">
                <link href="../../../css/dragAndDrop.css" rel="stylesheet" type="text/css">
              </g:else>
        …
```

If a widget includes themes separate from the OWF themes, use the other theme’s `themeContrast` and `themeFontSize` attributes to decide which theme the widget should use. If the available widget themes do not match the current OWF theme, make sure that the widget has a default theme.

#3   Additional Considerations
##Accessing Theme Information from JavaScript

It is also possible to use JavaScript to find the theme types.  See the example below:

```javascript
        var themeInfo = OWF.getCurrentTheme();

        /* themeInfo looks like:
         *  {
         *    //name of the theme
         *    themeName: 'theme-name',
         *
         *    //describes color contrast of the theme.  This may be one of 3 values:
         *    // 'standard' (colors provide no special contrast)
         *    // 'black-on-white' (black on white color contrast)
         *    // 'white-on-black' (white on black color contrast)
         *    themeContrast: 'black-on-white',
         *
         *    //this field is a number of the fontSize in pixels
         *    themeFontSize: 12
         *  }
```
