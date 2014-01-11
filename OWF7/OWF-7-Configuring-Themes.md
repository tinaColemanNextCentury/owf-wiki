# Themes
#1 Overview
OWF includes four pre-made themes: a default OWF theme, two high-contrast themes and a large text theme. OWF developers can create their own themes to include in the OWF user interface. End-users can switch between themes by selecting the ![Settings](OWFImages/OWF7/settings_button_18px.png?raw=true) button on the toolbar and then choosing Themes. 

Since the OWF 4 redesign, one line of code can change the overall color of OWF. Font size and font family are also adjustable. However, changing the entire look and feel of OWF requires additional work.

#2 Changing the Default Theme
The default theme is named OWF. To change the default theme, change the `defaultTheme` value in the **apache-tomcat-7.0.21/lib/OwfConfig.groovy** file. 

#3 Creating and Modifying Themes
OWF uses Compass, an open-source CSS stylesheet framework built on top of the SASS family of stylesheet languages. Two languages comprise SASS. OWF uses SCSS, the newer of the two languages. SCSS is a superset of CSS. It compiles into CSS. Compass is a framework for managing large SASS projects as well as augmenting and managing the SASS compilation process.  For more information, see the [Compass](http://compass-style.org/) and [SASS] (http:/sass-lang.com/).

##Prerequisites
To create and modify themes, the developer will need: 

* Compass versions 0.11.3

> _Note: Previous versions of OWF allowed for the use of Compass versions 0.11.3 to 0.11.7. However, style changes require the use of Compass 0.11.3 because newer versions of Compass automatically upgrade SASS to versions that cause issues with acccessibility-bow.scss._ 

* SASS 3.1.3 (required by Compass)
* Ruby 1.9.2 (required by SASS and Compass)

To obtain these dependencies:

1.	Install Ruby.
2.	Use the included “gem” tool to install SASS and Compass by running `gem install compass –v 0.11.3` as an administrator. 
3.	Confirm that SASS and Compass are on the system PATH.

##Layout of Themes Directory
To locate the theme files unzip the `apache-tomcat-7.0.21/webapps/owf.war` and open the themes directory.  The following figure shows the layout of the theme files:
 
![Themes Directory Structure](OWFImages/OWF7/themes_directory_structure.png)

<b>Figure: Themes Directory Structure</b>

The following table provides a brief description of the theme folder and the files found in `owf.war/themes`:

**Table: Theme File and Folder Description**

<table>
 <tr>
   <th>File or Folder Name</th>
   <th>Description</th>
 </tr>
 <tr>
   <td>/compile_all_themes.bat or /compile_all_themes.sh</td>
   <td>Shell scripts for Windows or UNIX that automate the process of compiling all of the themes</td>
 </tr>
 <tr>
   <td>/watch_all_themes.bat or  /watch_all_themes.sh</td>
   <td>Shell scripts for Windows or UNIX that start watch processes on all themes, which will automatically recompile the stylesheets whenever a change is detected</td>
 </tr>
 <tr>
   <td>/a_default.theme</td>
   <td>Parent folder for the OWF default theme</td>
 </tr>
 <tr>
   <td>/accessibility-bow.theme</td>
   <td>Parent folder for the black-on-white theme</td>
 </tr>
 <tr>
   <td>/large-text.theme</td>
   <td>Parent folder for the large text theme</td>
 </tr>
 <tr>
   <td>/accessibility-wob.theme</td>
   <td>Parent folder for the white-on-black theme</td>
 </tr>
 <tr>
   <td>/common</td>
   <td>Parent directory for files that are likely to be used by most or all themes</td>
 </tr>
 <tr>
   <td>/common/images</td>
   <td>Directory for images that are common to many themes or can serve as defaults</td>
 </tr>
 <tr>
   <td>/common/lib/owf_utils.rb</td>
   <td>Functions (written in Ruby) that are useable within the SCSS file (should not need to be modified)</td>
 </tr>
 <tr>
   <td>/common/stylesheets/</td>
   <td>SCSS "partials" that build OWF themes</td>
 </tr>
 <tr>
   <td>/common/stylesheets/_owf_all.scss</td>
   <td>Central import file that imports all other files in the directory. If creating new SCSS partials, include them in this file.</td>
 </tr>
 <tr>
   <td>/common/stylesheets/variables/</td>
   <td>Contains variables used within the SCSS stylesheets</td>
 </tr>
 <tr>
   <td>/common/stylesheets/variables/_constants.scss</td>
   <td>Variables values that should generally not change</td>
 </tr>
 <tr>
   <td>/common/stylesheets/variables/_ext_overrides.scss <br><i>Note: Modifying this file may require an Ext JS developer license.</i></td>
   <td>Overridden default values for Ext JS's SCSS files</td>
 </tr>
 <tr>
   <td>/common/stylesheets/variables/ *all other files</td>
   <td>Variables that control aspects of the stylesheet generation and default values. The values of these variables may be overridden in a given theme</td>
 </tr>
 <tr>
   <td>/template</td>
   <td>Directory containing a theme template that contains every file listed in this table except for <b>.css</b>. These files are as complete as possible without including properties that differentiates themes. To differentiate, developers must enter data.</td>
 </tr>
</table>

The following table explains the files and folders that comprise a theme. The files and folders are found under a specific theme’s directory like the black-on-white theme shown in the following figure:

![Black-on-White Theme Directory Structure](OWFImages/OWF7/bow_theme_directory_structure.png) 

<b>Figure: Black-on-White Theme Directory Structure</b>

In OWF, the parent theme directories include .theme in their naming convention. Example: accessibility-bow.theme. The following table, Theming Conventions, uses an example theme named example.theme (this example is not included in the bundle).

<b>Table: Theming Conventions</b>

<table>
  <tr>
    <th>Convention</th>
    <th>Description</th>
  </tr>
  <tr>
   <td>example.theme/theme.json</td>
   <td>Contains the theme metadata description that tells OWF where to find the theme's files at runtime and provides information about the description, author, and display name</td>
  </tr>
  <tr>
   <td>example.theme/css/example.css</td>
   <td>The result of compiling a SCSS file from the SASS directory is stored here, in a file with the same name but with a <b>.css</b> extension instead of <b>.scss</b></td>
  </tr>
  <tr>
   <td>example.theme/images</td>
   <td>Location of theme-specific images. OWF searches for images here first.  If they are not found, OWF searches common/images</td>
  </tr>
  <tr>
   <td>example.theme/images/preview/</td>
   <td>Directory for theme screenshots</td>
  </tr>
  <tr>
   <td>example.theme/sass/example.scss</td>
   <td>The main .scss file for a theme – overrides any desired variables from the common/stylesheets/variables/example files. It defines the theme background and imports the desired files from common/stylesheets. This file is essentially where the theme is defined.</td>
  </tr>
</table>
  
#4   Creating a New Theme

1.	Choose a theme name.
The name should not have any spaces. It should be all lowercase. Words can be separated by hyphens.
2.	Copy the `template` directory to `theme_name.theme`; substitute the name created in step 1 for the theme for `theme_name`. 
3.	Navigate into the `theme_name.theme` directory.
4.	Open `theme.json` in a text editor and edit the following fields: 
     * The `name` attribute must use the `theme_name` chosen in step 1.  
     * The `display_name` attribute should contain a user-friendly, readable name for the theme (It can include spaces and capital letters.).  
     * The CSS attribute must include the `theme_name` as show below: `themes/<theme_name>.theme/css/<theme_name>.css`.
     * All URL properties are relative to the context root.  For now, ignore the `thumb` and `screenshots` fields, because images of a theme cannot exist until the theme is created.
5.	Rename `sass/theme.scss` to `sass/<theme_name>.scss`
6.	Edit `sass/<theme_name>.scss` ( **MANDATORY** )
    * A. Set the `$theme-name` variable to the `<theme_name>` chosen in step 1.
    * B. Set the overall background.  If the background is not set, it defaults to plain white. 

 The `sass/<theme_name>.scss` file is the primary place to create a custom theme by overriding variables. The files within `themes/common/stylesheets/variables` contain lists of variables that are available for overriding.  Custom values for these variables should be defined directly below the `$theme-name` declaration (BEFORE importing `variables/*`). The lower part of this file imports all the SCSS partials that use the variable values to construct the stylesheets. 

 > _Note: For complex customizations, import statements can be deleted if equivalent functionality is custom-implemented by the theme._
7.	By default, a theme will search the `common/images` directory for image files. To use custom images in the new theme, override those images by placing new images in the `theme_name.theme/images` directory. Those new images will only apply to `theme_name`. New images must have identical pathnames and file names as the images being overridden relative to the `images` directory.
8.	Compile your theme.  This can be done in several ways.  
     * To do a one-time compile of only this theme, navigate to the `sass` directory and run `compass compile` in a terminal. You may pass in the `--force` option to force a recompile even when source files do not appear to be changed.  
     * To start a process that will continue to watch your SCSS for changes and recompile as needed, navigate to the `sass` directory and run `compass watch` in a terminal.
     * To do a one-time compile of ALL themes, navigate to the `themes` directory and run the appropriate script. 

          * A.	On Windows, this is done by running `compile_all_themes.bat`  
          * B.	On UNIX, this is done by running `sh compile_all_themes.sh` 
> _Note: The scripts assume that their current directory is the themes directory._
     * To start watches on ALL themes, navigate to the themes directory and run the appropriate script. These scripts assume that the current directory is the `themes` directory.
          * A.	On Windows, run `watch_all_themes.bat`.  This will open a new, minimized command prompt for each theme, in which `compass watch` will be running.  
          * B.	On UNIX, run `sh watch_all_themes.sh` in a terminal. This will start `compass watch` as a background process for each theme.  The script will not exit until the watches exit, and so is generally terminated with a SIGINT. 
9.	Once the theme successfully compiles, verify that `theme_name.css` has been created in the css directory, and that it does not contain any error messages (These messages replace the entire normal output, so if errors exist they will be obvious).
10.	Deploy OWF with the newly created theme.  Do this one of two ways: 
    * For a development instance, run `grails –Duser=testAdmin1 run-app –https` from the top directory of the source tree.
    * Build OWF and start the Tomcat server, as described in 3.3: OWF Bundle Description. To build OWF, run `ant` from the top directory of the source tree. To start the build server, run `start.bat` or `start.sh` located in `/apache-tomcat-7.0.21`. 

 > _Note: Before running ant, the developer may need to run ant init-build._
11.	Log into OWF as a user or admin, and open the theme selector window which is located under the settings button on the toolbar.
12.	Select and apply the new theme in the theme selector.
> _Note: Currently, there are no screenshots for the newly created theme._
13.	Once the new theme is running, take some screenshots of it. Screenshots should be saved in the `theme_name.theme/images/preview` directory. 
14.	Edit `theme_name.json`. Set the `thumb` attribute to one of the theme screenshots of the entire browser viewing area.  Next, add screenshot items to the `screenshots` array.  These items are JSON objects that contain the attributes `url` and `description`. For an example of screenshot objects, see the `theme.json` files of other themes or the comment section at the bottom of the template `theme.json`.
15.	In the OWF user interface, open the theme selector again and verify that the screenshots display. 

#5   Making Themes Usable Outside of owf.war

Once the creation of a custom theme is complete, (see the section entitled **Creating a New Theme**) it can be housed outside of the **owf.war** in a customizable location on the `classpath`.  The following section, added to the **apache-tomcat-7.0.21\lib\OwfConfig.groovy** file, allows an administrator to define where themes, help files, and js-plugins will reside.

```groovy
    owf {
      //Locations for the optional external themes and help directories.
      //Default: 'themes', 'help', and 'js-plugins' directories on the classpath.
      //Can be configured to an arbitrary file path.  The following path styles are supported:
      //  'file:/some/absolute/path' ('file:C:/some/absolute/path' on Windows)
      //  'classpath:location/under/classpath'
      //  'location/within/OWF/war/file'
        external{
            themePath = 'classpath:themes'
            helpPath = 'classpath:help'
            jsPluginPath = 'classpath:js-plugins'
```

In order to make the themes usable from OWF, one of two scenarios will need to be implemented.  Either the `\etc\tools\create-web-bundles.bat`(or `.sh`) command will need to be run in order to create gzipped CSS files, or `uiperformance` will need to be disabled.

When running the script, note that it takes the following arguments on the command line, the first of which is required:

* `-js externalJsLocation` (required)
The location of the external js plugin folder. 
* `-o owfLocation`
The location of either the OWF WAR file or a directory where the WAR was extracted. Giving it the WAR file extracts it to a temp directory. It is then recreated where it was originally located after the rebundling is complete.
* `-e externalThemesLocation` (Optional)
The location of the external themes folder. If it is unspecified, external themes are not bundled.
Once the `create-web-bundles.bat` (or `.sh`) has been executed, the included themes should be available from the theme selector in OWF.

#6   Non-themable OWF Components
The following components are not theme-able:

* Sign-out page
* CAS sign-in page

#7   Themable OWF Components
This section lists the various SCSS files that are used to construct the OWF stylesheets and the themable components that are controlled by those files. Changes to these files will affect **all** themes. All themable components are located in the `owf.war/themes/common/stylesheets` directory.

<b>Table: Themable Components</b>

<table>
 <tr>
   <th>File That Must Be Modified</th>
   <th>Themable Component(s)</th>
 </tr>
 <tr>
   <td>_aboutWindow.scss</td>
   <td>About Window</td>
 </tr>
 <tr>
   <td>_adminWidget.scss</td>
   <td>Admin Editors</td>
 </tr>
 <tr>
   <td>_banner.scss</td>
   <td>Toolbar <br> User Menu</td>
 </tr>
 <tr>
   <td>_buttons.scss</td>
   <td>Buttons</td>
 </tr>
 <tr>
   <td>_dashboardSwitcher.scss</td>
   <td>Dashboard Switcher</td>
 </tr>
 <tr>
   <td>_editWidget.scss</td>
   <td>Admin Editors</td>
 </tr>
 <tr>
   <td>_grid.scss</td>
   <td>Grids</td>
 </tr>
 <tr>
   <td>_launchMenu.scss</td>
   <td>Launch Menu</td>
 </tr>
 <tr>
   <td>_main.scss</td>
   <td>Drop-down Menu <br> Form <br> Headers: Window, Panel and Taskbar <br> Keyboard Focus <br> Loadmask <br> Message Box <br> Progress Bar <br> Tooltips <br> Etc.</td>
 </tr>
 <tr>
   <td>_manageWindowContainers.scss</td>
   <td>Dashboard Editors <br> Managers Widget Managers</td>
 </tr>
 <tr>
   <td>_marketplaceWindow.scss</td>
   <td>Marketplace Window</td>
 </tr>
 <tr>
   <td>_portal.scss</td>
   <td>Widget Portlets</td>
 </tr>
 <tr>
   <td>_settingsWindow.scss</td>
   <td>Administration Tools Window <br> Settings Window</td>
 </tr>
 <tr>
   <td>_systemWindow.scss</td>
   <td>About Window <br> Administration Tools Window <br> Dashboard Switcher <br> Settings Window</td>
 </tr>
 <tr>
   <td>_themeSwitcher.scss</td>
   <td>Theme Switcher Window</td>
 </tr>
 <tr>
   <td>_widgetChrome.scss</td>
   <td>Widget Chrome Menu Bar <br> Widget Chrome Buttons <br> Widget Chrome Sample Widget</td>
 </tr>
 <tr>
   <td>_widget.scss</td>
   <td>Launch Menu Widget Icons <br> Widget Switcher Widget Icons</td>
 </tr>
</table>

> _Note: **.scss** files that apply to themes will be listed in the table above, other **.scss** files that are included in the bundle but do not pertain to themes may not appear in the table._

#8   Enabling OWF Customization Configuration

In order to enable the ability to override the JavaScript in OWF, **OwfConfig.groovy** must be updated in the `apache-tomcat-7.0.21/lib` directory. 
Add the following property: `uiperformance.enabled=false`. To apply the changes, restart the system.

```groovy
    environments {
        production {
            dataSource {
                dbCreate = "none"
                username = "sa"
                password = ""
                driverClassName = "org.hsqldb.jdbcDriver"
                url = "jdbc:hsqldb:file:prodDb;shutdown=true"
                pooled = true
                properties {
                    minEvictableIdleTimeMillis = 180000
                    timeBetweenEvictionRunsMillis = 180000
                    numTestsPerEvictionRun = 3
                    testOnBorrow = true
                    testWhileIdle = true
                    testOnReturn = true
                    validationQuery = "SELECT 1 FROM INFORMATION_SCHEMA.SYSTEM_USERS"
                }
            }
            //enable uiperformance plugin which bundles and compresses javascript
            uiperformance.enabled = false
        }
    }


    beans {
    	//This block is equivalent to using
    // an     org.springframework.beans.factory.config.PropertyOverrideConfigurer
	//See Chapter 14 of the Grails documentation for more information: http://grails.org/doc/1.1/	
    }
    println('OwfConfig.groovy completed successfully.')
```

> _Note: For the current build, the modification does have a mildly negative side effect of removing the performance-enhancing OWF JavaScript file-bundling feature._