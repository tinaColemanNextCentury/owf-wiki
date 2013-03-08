# Instructions: Configuring OWF Help COntent

When a user clicks the Help button in the toolbar, OWF offers online help: 

![Help Button on Toolbar](OWFImages/OWF7/help_button_on_toolbar.png)

**Figure: Help Button on Toolbar**

Out of the bundle, the Help window contains:
* Instructions for configuring help 
* Keyboard navigation shortcuts

OWF provides various user help videos including an OWF Overview. To add these files or others into the Help directory, follow these instructions:

1. Navigate to `\apache-tomcat-7.0.21\lib\help`
2. Add (or remove) files from the `\help` directory
 A. To add the OWF help videos, open the **owf-help.zip** and copy the user help video folders into `\apache-tomcat-7.0.21\lib\help`.

 > _Note: The **owf-help.zip** is available for download alongside the OWF Bundle._

3. Refresh the browser. Contents in the help window should be updated. 

##Custom Help File Types

Only files in the `\help` directory with specific file extensions will appear in the user interface. By default, files with the following file extensions will appear: `HTML`, `HTM`, `GSP`, `JSP`, `PDF`, `DOC`, `DOCX`, `MOV`, `MP4` and `WMV`. To modify the file types that will appear in the help window on the toolbar, the administrator must restart the server after updating the following list of values in **OwfConfig.groovy**:

```groovy
        <property name="helpFileRegex" value="^.*\.(html|htm|gsp|jsp|pdf|doc|docx|mov|mp4|wmv)$" /> 
```

##Changing the Location of Help 

The help directory location is defined by the `helpPath` property in **OwfConfig.groovy**. By default help files are located on the classpath. To change the directory location, replace `classpath:help` with one of the following supported locations, then restart the server:

```groovy
          //  'file:/some/absolute/path' ('file:C:/some/absolute/path' on Windows)
          //  'classpath:location/under/classpath'
          //  'location/within/OWF/war/file'
```