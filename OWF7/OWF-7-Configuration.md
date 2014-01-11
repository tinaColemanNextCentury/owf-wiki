# Configuration
#1 Default Configuration

The OWF Bundle is configured to run by default on localhost with a predefined set of users. In addition to `users.properties`, detailed in the **Adding Users/Roles/Groups** section, OWF provides override files which are used to modify the default configuration.

To use an override file, place the individual file somewhere on the classpath of the server running OWF. When using the default Tomcat bundle, externalized configuration files should be placed in the folder `\apache-tomcat-7.0.21\lib`. By default, **OwfConfig.groovy** is located in `\apache-tomcat-7.0.21\lib`. The other override file, **CASSpringOverrideConfig.xml**, is located in the Ozone Bundle at `\etc\override`. If using an application server other than Tomcat, copy the override files into the directory that will include them in the classpath for that specific application server.

Optional override files are:

   **CASSpringOverrideConfig.xml**

   **OwfConfig.groovy**

Each of the override files is detailed in the sections that follow.

##Adding Users/Roles/Groups

The addition of users, groups, and roles into OWF depends on the choice of security implementation. The following example outlines the procedures for adding users, groups, and roles to the sample OWF X509-only, CAS-only, and X509-with-CAS security modules:

> _Note: The sample security modules are included as examples and should NOT be used in a production environment. For more information, please refer to the [OWF Security](OWF-7-Configuring-OWF-Security) page._

1.	Edit `\apache-tomcat-7.0.21\lib\users.properties`

        testUser1=password,ROLE_USER,Test User 1,[group1;I am a sample Group 1 from users.properties;test@gmail.com;active]
        testUser2=password,ROLE_USER,Test User 2
        testUser3=password,ROLE_USER,Test User 3
        testAdmin1=password,ROLE_ADMIN,Test Admin 1,[group1;I am a sample Group 1 from users.properties;test@email.com;active],[group2;I am a sample Group 2 from users.properties;test2@email.com;active],[group3;I am a sample Group 3 from users.properties;test3@email.com;inactive]

    > _Note: To have actual spaces between names and numbers, escape spaces using the “\” (do not include the quotation marks) character. Moreover, when using CAS, or a custom setup which employs anything other than X509 authentication, the user names MUST be entered in all lower case. This is a technical issue with Spring Security, and will be remedied in a future release._
 
2.	Add users to the file in accordance with the following rules: 
    * A.	Data Format:
Username=password, role, display name,[group name, group description, group contact email, active/inactive status].
    * B.	All of the information for a single user, including group information, should be on a single line.
    * C.	Multiple groups may be delimited by commas.
    * D.	Group information is optional, and may be left out for any single user.
    * E.	Once a group has been created for the first time, the description, contact email, and active/inactive status will not affect those values within OWF—that information must be managed through the OWF Group Manager administrative widget. 
3.	Save the file and restart the OWF server. 
Any user added to `users.properties` will be granted access to OWF upon restart.
Any user deleted from `users.properties` will be denied access to OWF upon restart.

> _Note: If a custom webserver is being used along with the provided example security, the `users.properties` file can be copied to any directory that is on the classpath of the Web server in use. For example, if using Jetty, the file can be copied to the `\<jetty root>\resources` directory._

To add users to any security module use X509 authentication, generated a PKI User Certificate that can be recognized by OWF. 

##Help Content Configuration
When a user clicks the question mark button in the toolbar, OWF offers online help:
 
![OWF Toolbar](OWFImages/OWF7/help_button_on_toolbar.png) 

<b>Figure: Help Button on Toolbar</b>

Out of the bundle, the Help window contains:

* Instructions for Configuring Help 
* Keyboard Navigation Shortcuts

OWF provides various user help videos including an OWF Overview. To add these files or others into the help directory, follow these instructions:

1.	Navigate to `\apache-tomcat-7.0.21\lib\help`
2.	Add (or remove) files from the `\help` directory
    * A.	To add the OWF help videos, open the **owf-help.zip** and copy the user help video folders into `\apache-tomcat-7.0.21\lib\help`.
    
  > _Note: The owf-help.zip is available for download alongside the OWF Bundle._

3.	Refresh the browser. Contents in the help window should be updated. 

###Changing the Location of Help

The help directory location is defined by the `helpPath` property in **OwfConfig.groovy**. By default help files are located on the classpath. To change the directory location, replace `classpath:help` with one of the following supported locations, then restart the server:

    //  'file:/some/absolute/path' ('file:C:/some/absolute/path' on Windows)
    //  'classpath:location/under/classpath'
    //  'location/within/OWF/war/file'

##2 Custom Configuration

OWF externalized configuration files are employed in **OwfConfig.groovy**, and **CASSpringOverrideConfig.xml**. When OWF is deployed to a non-localhost environment, all externalized configuration files must be deployed and modified. In order to deploy to a non-localhost environment, changes need to be made to each file. Those changes are explained in the individual sections about each file. 

Use of a production quality database (such as Oracle or MySQL), instead of the default HSQLDB, will require a change to the **OwfConfig.groovy** file, detailed in the following section.

> _Note: In previous versions of OWF, the **OwfConfig.xml** file housed many of the application’s customizable values. Beginning with OWF 6, these values have been moved to the **OwfConfig.groovy** file described below._

###OwfConfig.groovy File

`OwfConfig.groovy` is an OWF configuration file that allows an administrator to modify database connectivity information and other OWF variables. Once changes are made, restart the system to apply the changes. Developers comfortable with the Groovy language and the Grails application framework should be comfortable writing additional code for this file. 

For full descriptions on database variables, please see the table entitled, OWF Externalized Database Properties (located on the [Installation](OWF-7-Configuration-Installation) page. For more details on the `uiperformace plugin` please see the section **Enabling OWF Customization Configuration** on the [Customizing OWF Javascript](OWF-7-Configuring-Custom-JavaScript) page.

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
            uiperformance.enabled = true
    
        }
    }

    //this section may modify any existing spring beans
    beans {
    
    }
    
    //main owf config object
    owf {
        
        // log4j file watch interval in milliseconds
        log4jWatchTime = 180000; // 3 minutes

        enablePendingApprovalWidgetTagGroup = false

        sendWidgetLoadTimesToServer = true
        publishWidgetLoadTimes = true

        //showLastLogin = false
        lastLoginDateFormat = 'n/j/Y G:i'

        defaultTheme = "a_default"

        showAccessAlert = "true"
        accessAlertMsg = "Lorem ipsum dolor sit amet, consectetur adipiscing elit."

        // Specifies a freeTextEntryMessage to appear on all dialogs which allow text entry
        // To turn off the warning message, use the following:
        //     freeTextEntryWarningMessage=''
        freeTextEntryWarningMessage = ''

        //use to specify a logout url
        logoutURL = "/logout"

        //sets the autoSave interval for saving dashboards in milliseconds 900000 is 15 minutes
        autoSaveInterval = 900000

        helpFileRegex = '^.*\\.(html|gsp|jsp|pdf|doc|docx|mov|mp4|swf|wmv)$'

        //This value controls whether the OWF UI uses shims on floating elements,
        // setting this to true will make
        //Applet/Flex have less zindex issues, but browser performance may suffer
        // due to the additional shim frames being created
        useShims = false

        //Locations for the optional external themes and help directories.
        //Default: 'themes', 'help', and 'js-plugins' directories on the classpath.
        //Can be configured to an arbitrary file path.  The following
        //path styles are supported:
        //  'file:/some/absolute/path' ('file:C:/some/absolute/path' on Windows)
        //  'classpath:location/under/classpath'
        //  'location/within/OWF/war/file'
            external {
            themePath = 'classpath:themes'
            helpPath = 'classpath:help'
            jsPluginPath = 'classpath:js-plugins'
        }

        // Optional Configuration elements for custom headers/footers.
        // Example values are shown.  File locations are relative or absolute paths to
        // resources hosted on the owf web server.  Heights are in pixel amounts.
        //customHeaderFooter {
        //	header = 'location/within/web/context/example.html'
        //	headerHeight = 0
        //	footer = 'location/within/web/context/example.html'
        //	footerHeight = 0
        //	jsImports = ['location/for/exampleImport1.js', 'location/for/exampleImport2.js']
        //	cssImports = ['location/for/exampleImport1.css', 'location/for/exampleImport2.css']
        //}

        metric {
            enabled = false
            url = 'https://localhost:8443/metric/metric'

            //Optional additional properties with default values shown
            //keystorePath = System.properties['javax.net.ssl.keyStore']
            //keystorePass = System.properties['javax.net.ssl.keyStorePassword']
            //truststorePath = System.properties['javax.net.ssl.trustStore']
            //timeout = 1800000
        }
    }


    println('OwfConfig.groovy completed successfully.')
```

The **OwfConfig.groovy** file contains customizable functionality which can be modified by an administrator. Restarting the system once the files have been modified will apply the changes.

###Custom log4jWatchTime
The values associated with the `log4j WatchTime` offers a time-based value as to how often the `log4j` logging system looks for updates in the **owf-override-log4j.xml** file. The `180000` value is stored in milliseconds. Accordingly, the value of `180000` as presented below is actually a 3-minute timer.

    log4j {
        // log4j file watch interval in milliseconds
        log4jWatchTime = 180000; // 3 minutes
    }

> _Note: When changes are made to the `log4jwatchTime` property, the server does NOT need to be restarted._

###Enabling Marketplace Widget Approval

OWF is automatically configured to allow users to search for and request widgets from a Marketplace server. This allows users to immediately use widgets imported from Marketplace. When a user requests a widget from Marketplace, it will appear in the user’s Launch Menu. 

If an administrator wants to approve widgets from Marketplace before user’s can use them, they must update **OwfConfig.groovy** and add the Marketplace Approvals Widget to OWF:

1.	Set the `enablePendingApprovalWidgetTagGroup` property in **OwfConfig.groovy** to true:
    enablePendingApprovalWidgetTagGroup = true
2.	Save OwfConfig.groovy and restart the server. 
3.	Next, add the Widget Approval descriptor file to OWF:
 * A.	Sign in to OWF as an administrator;
 * B.	Click the Administration button on the toolbar, then, select Widgets to open the Widgets Manager.
 * C.	From the manager, click Create. 
 * D.	Type `../admin/descriptors/Approvals_descriptor.html` into the Import Widget from Descriptor URL and click Load. (This file is stored in the `apache-tomcat-7.0.21\webapps\owf\admin\descriptors` directory.)
 * E.	Click Apply and add the widget to users or groups.  

> _Note: Instructions for connecting OWF to Marketplace(s) are found in the OWF Administrator’s Guide._

###Widget Load Times
Because the speed with which widgets launch and operate is related to an individual system’s resources, OWF has implemented ways to track the time between a widget’s rendering and the time it is actually ready to be used. 

The following values can be active at the same time: 

    sendWidgetLoadTimeToServer = true
    publishWidgetLoadTimes = true

`sendWidgetLoadTimeToServer` sends widget load time data to a system log file where it is written and stored.
 
`publishWidgetLoadTimes` will send the data to the Widget Log Widget, which can be opened from the Launch Menu, after its assigned to a user’s instance of OWF.

###Using Shims
From the `useShims` property in **OwfConfig.groovy**, developers can configure OWF to use shims. The property is set to `false` by default. Shims can be used to improve the stability of floating element features. To use shims, set the `useShims` property to `true` as shown in the following code example:

    //this value controls whether the OWF UI uses shims on floating elements,
    // setting this to true will make
    //Applet/Flex have less zindex issues, but browser performance may suffer
    // due to the additional shim frames being created
    useShims = true


###Custom Last Sign-in Date
OWF stores the last sign-in dates of all users and displays it in both the User Menu and inside administration widgets. While the administration widgets show the exact date and time, the User Menu displays a rounded approximation known as a fuzzy date shown below: 

![Sign-in Information](OWFImages/OWF7/drop_down_user_menu.png)

<b>Figure: Sign-in displayed on drop-down User Menu</b>

The exact date will appear in a pop-up when a user hovers over the fuzzy date. This exact date format is customizable. 
To change the default format of the sign-in date, shown in the User Menu, change the `lastLogin.DateFormat` value. For example, the default code formats the date like this: January 22, 2011, 1:39 p.m. To change this format, update the highlighted code in **OwfConfig.groovy**: 

    //showLastLogin = false
    lastLoginDateFormat = 'n/j/Y G:i'

There are several formatting options available. Explore them in the [Sencha/Ext JS documentation](http://dev.sencha.com/deploy/ext-4.0.2a/docs/#/api/Ext.Date). 

###Custom Show Access Alert
Depending on the individual security requirements where OWF is being deployed, users may be required to agree to the specific terms of a security warning. Deploying a security warning is accomplished via a custom access alert. There are two sets of properties (and their values) which govern the access alert message.

OWF ships with placeholder text that is shown in the following configurable XML:
  
    showAccessAlert = "true"
    accessAlertMsg = "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla interdum eleifend sapien dignissim malesuada. Sed imperdiet augue vitae justo feugiat eget porta est blandit. Proin ipsum ipsum, rutrum ac gravida in, ullamcorper a augue. Sed at scelerisque augue. Morbi scelerisque gravida sapien ut feugiat. Donec dictum, nisl commodo dapibus pellentesque, enim quam consectetur quam, at dictum dui augue at risus. Ut id nunc in justo molestie semper. Curabitur magna velit, varius eu porttitor et, tempor pulvinar nulla. Nam at tellus nec felis tincidunt fringilla. Nunc nisi sem, egestas ut consequat eget, luctus et nisi. Nulla et lorem odio, vitae pretium ipsum. Integer tellus libero, molestie a feugiat a, imperdiet sit amet metus. Aenean auctor fringilla eros, sit amet suscipit felis eleifend a."

1.	The value for the property `showAccessAlert` must be true or false. These values are case sensitive and will only work as `true` or `false` (all lowercase) values. True will display the warning message, as created in the value tag for the property name `accessAlertMsg`. The value can be made false, which will stop the warning from triggering. This allows an administrator to keep a warning message saved, regardless of whether it is being used or not.
2.	When the `showAccessAlert` value is set to true, upon sign in, users will be presented with the new access alert message and will not be granted access to OWF until they click the OK button.

###Custom “Data-Entry” Message
OWF ships with the ability to add a custom text-entry message area. The message can serve as a warning for text entry, or be a message directly related to the specific instance of OWF. The message appears in red and is positioned as shown in the image below: 

![Free Text-Entry Warning Example](OWFImages/OWF7/group_editor.png?raw=true)

<b>Figure: Free Text-Entry Warning Example</b>

An administrator can customize the message shown above by entering text in the `freeTextEntryWarningMessage` shown below: 

    1	// Specifies a freeTextEntryMessage to appear on all dialogs which allow text entry
    2	// To turn off the warning message, use the following:
    3	//     freeTextEntryWarningMessage=''
    4	freeTextEntryWarningMessage=''	

Once the file is saved and the system restarted, administrators will be presented with the new custom text entry warning message when entering data into administration widgets and interfaces.  To cancel the message, leave an empty string of two single quotes, as shown in line 4 above.

###Custom Logout
OWF allows users to sign out of OWF in accordance with their instance’s security plugins.  Any modifications made to the URL will take effect when the system is restarted.

    //use to specify a logout url
    logoutURL = "/logout"

> _Note: The security plugin being used must be customized so that the value entered above will work as expected._

###Custom “Auto Save” Interval
The OWF user interface will automatically save the user’s dashboard at a configurable time interval. The default is to save every 15 minutes. Any modifications to the default save interval will take effect when the OwfConfig.groovy is saved and the system is restarted. 

    //sets the autoSave interval for saving dashboards in milliseconds 900000 is 15 minutes
    autoSaveInterval = 900000

> _Note: The value for the above setting is in milliseconds. It can be changed to any millisecond value._

> _Note: The Auto Save will keep the user session alive as long as a dashboard is visible in the browser._
 
###Custom Help File Types
Only files in the `\help` directory with specific file extensions will appear in the user interface. By default, files with the following file extensions will appear: `HTM`, `HTML`, `GSP`, `JSP`, `PDF`, `DOC`, `DOCX`, `MOV`, `MP4` and `WMV`. To modify the file types that will appear in the Help window on the OWF Toolbar, the administrator must restart the server after updating the following list of values in **OwfConfig.groovy**:

```groovy
    helpFileRegex = '^.*\\.(htm|html|gsp|jsp|pdf|doc|docx|mov|mp4|wmv)$'
```

###Enabling Ozone Metrics Service
To enable the Metrics Service change the `metric.enabled` property to true. If the metrics service is located on a different server than OWF, enter its URL as shown in the following example: 

        metric {
            enabled = true
            url = 'https://servername:port/metric/metric'

> _Note: Find detailed instructions regarding Metrics Service security, configuration and installation (including database information) in the Metrics Service Guide which is located in the **metric-bundle.zip**._

####Configuring the Metrics Widget in OWF
To view metrics data using an OWF widget, make metrics data available in OWF:

1.	Integrate the metrics server into OWF, as described in the previous section.
2.	From the toolbar, click the OWF Administration button and select Widgets to open the Widget Manager.
3.	 Use the following information to create the View Metrics widget:

<b>Table: Data for Metrics Widget Definition </b>

<table>
    <tr>
      <th>Definition</th>
      <th>Data Input</th>
    </tr>
    <tr>
      <td>URL</td>
      <td>https://widget-servername:port/metric/admin/Metrics.gsp</td>
    </tr>
    <tr>
      <td>Large Icon</td>
      <td>https:// widget-servername:port/metric/themes/common/images/icons/16x16_metrics.png</td>
    </tr>
    <tr>
      <td>Small Icon</td>
      <td>https:// widget-servername:port/metric/themes/common/images/icons/64x64_metrics.png</td>
    </tr>
    <tr>
      <td>Width</td>
      <td>700</td>
    </tr>
    <tr>
      <td>Height</td>
      <td>500</td>
    </tr>
    <tr>
      <td>Widget Type</td>
      <td>Metric</td>
    </tr>
</table>

####Viewing the Metrics Widget in OWF
The Metrics Service can only be viewed in OWF. After following the steps in the previous section and assigning the View Metrics widget to users, the widget will appear under the Metrics button on the toolbar. 

> _Note: OWF users who signed in using CAS will be prompted to sign in to additional security for the Metrics Service_. 

![Metrics Widget](OWFImages/OWF7/metrics_widget.png)

<br><b>Figure: Metrics Widget</b>

The widget opens to a Tag Cloud tab that lists widgets views (widgets that are viewed more will be larger in the Tag Cloud) and a grid of widget data. Clicking the name of a widget from the Tag Cloud or the grid switches to the widget’s Graph tab. This displays how many times that widget was viewed. To change the monitoring dates, click the calendar icon(s) above the graph. Use the arrows or click directly on the month and year to select different date durations. Clicking the month and year (identified in the image below) opens a drop-down date selector. After clicking OK, click the highlighted date on the calendar to complete the change.

![Graphing Tab on the Metrics Widget ](OWFImages/OWF7/metrics_widget_graphing_tab.png) 

<br><b>Figure: Graph Tab Displaying Date Switcher</b>

##Custom Logging Functions

General logging can be enabled by editing the **owf-override-log4j.xml** file which can be found in the `apache-tomcat-7.0.21\lib` directory:

```xml
    <logger name="AuditOWFWebRequestsLogger" additivity="false">
      <level value="error" />
      <appender-ref ref="ozone-async" />
    </logger>

    <!-- For security logging, set this log level to "info". -->
    <logger name="ozone.securitysample.authentication.audit.SecurityAuditLogger" additivity="false">
      <level value="info" />
      <appender-ref ref="ozone-async-audit" />
    </logger>

    <!—Add this to enable general OWF Debug logging -->
    <logger name="grails.app" additivity="false">
      <level value="trace" />
      <appender-ref ref="ozone-async" />
    </logger>
```

> _Note: The **owf-override-log4j.xml** file shown above does not ship with the code shown at the bottom of the sample. However, it can be pasted into the file at an administrator’s discretion in order to enable the logging of general OWF server debug messages._

To confirm that the log files are being written, examine the `apache-tomcat-7.0.21\logs` directory. Developers familiar with `Log4j` configurations should be comfortable with this file. 

> _Note: Useful configurations/common requests are called out in comments in the file. For example, audit logging describing each user’s Web calls can be enabled by setting `AuditOWFWebRequesterLogger` and `ozone.filter` to logging level `info`._

Different third party libraries within OWF have also been called out so that administrators can easily modify logging levels.

##Audit Logging
OWF includes an option to audit all user entry and exit in the system.  The OWF Bundle ships with this feature enabled by default. The Audit Log tracks the following types of changes:

* Both successful and unsuccessful sign-in attempts
* User Sign-out Events:	
  * A user signing out on purpose
  * A session times out

> _Note: References to the CAS and OWF must match the settings of the current installation._

###Configuring Audit Log Levels
OWF logging levels can be set by editing the **/apache-tomcat-7.0.21/lib/owf-override-log4j.xml** file, which ships with the OWF Bundle. To change the audit log level, open the file and search for the following section:

```xml
    <!-- For security Audit logging, set this log level to "info". -->
     <logger name="ozone.securitysample.authentication.audit.SecurityAuditLogger" additivity="false">
        <level value="info" />
        <appender-ref ref="ozone-async-audit" />
    </logger>
```

The log statement shown above, `ozone.securitysample.authentication.audit.SecurityAuditLogger`, captures sign-in and sign-out events. In debug mode, the logger will record authentication credentials, such as: SubjectDN, IssuerDN and Validity dates for X.509 Certificate logins, as well as CAS credentials for CAS sign-in. When deploying a custom security plugin, use the logger shown above to capture all sign-in events for the system. This logger supports “info”, “debug” and “off” levels, as described in the section below. 

When distributed, the default log level is set to “info.” Audit logging supports the following three log levels: 

1.	**Info** - The minimal amount of information concerning a database change is logged and consists of the following fields within the log statement:
 * A.	**Log level** - This will set to “INFO” or “DEBUG” while logging is turned on.
 * B.	**Log date/time** - The date and time that an event occurred. The time pattern can be changed by editing the `layout` tag of the `ozone-audit-log appender`.
 * C.	**Remote IP** - The IP address of the remote client that triggered the log event.
 * D.	**Session ID** - The http request session ID of the log event.
 * E.	**User** - The user name of the authenticated user that caused the log event.
 * F.	**Event Type** - USER LOGIN or USER LOGOUT.
 * G.	**Event Message** - A description of the event.
2.	**Debug** - This level provides all of the same information as the INFO level, but provides more detail in the event message.
3.	**Off** - No login events will be logged.

When the audit log levels are modified, it is not necessary to restart or “bounce” OWF, as the server has a log-change listener which periodically (every 3 minutes, by default) checks for log file changes and reloads the changes should a modification to the log level take place.

###Sign-in Events

When using the sample pluggable security modules included in the OWF Bundle, successful sign-in authentication is captured by `ozone.securitysample.authentication.listener.AuthenticationSuccessListener` and `ozone.securitysample.authentication.listener.AuthenticationFailureListener` captures sing-in authentication which fails.
A sign-in failure will occur and be recorded in the log if a user has a valid PKI Certificate but the associated username is not registered as a valid user within OWF. A failed sign in produces the following log statement at the info level:

    INFO [02/15/2011 15:24:04 -0500] IP: 127.0.0.1 User: testAdmin1 [USER LOGIN]: LOGIN FAILURE - ACCESS DENIED with FAILURE MSG [Login for 'testAdmin1' attempted with authenticated credentials [CERTIFICATE LOGIN]; However, the Provider was not found. Access is DENIED.]

A failed sign in produces the following log statement at the debug level:

    DEBUG [02/15/2011 15:27:18 -0500] IP: 127.0.0.1 User: testAdmin1 [USER LOGIN]:LOGIN FAILURE - ACCESS DENIED with FAILURE MSG [Login for 'testAdmin1' attempted with authenticated credentials [CERTIFICATE LOGIN >> Signature Algorithm: [SHA1withRSA, OID = 1.2.840.113549.1.1.5]; Subject: [EMAILADDRESS=testAdmin1@nowhere.com, CN=testAdmin1, OU=Ozone, O=Ozone, L=Columbia, ST=Maryland, C=US]; Validity: [From: Thu Feb 04 13:58:52 EST 2010, To: Sun Feb 03 13:58:52 EST 2013]; Issuer: [EMAILADDRESS=ozone@nowhere.com, CN=localhost, OU=Ozone, O=Ozone, L=Columbia, ST=Maryland, C=US]; ]; However, the Provider was not found. Access is DENIED. Login Exception Message: [No AuthenticationProvider found for org.springframework.security.web.authentication.preauth.PreAuthenticatedAuthenticationToken]]

A successful PKI Certificate sign in produces the following log statement at the info level:

    INFO [02/15/2011 15:39:13 -0500] IP: 127.0.0.1 User: testAdmin1 [USER LOGIN]: LOGIN SUCCESS - ACCESS GRANTED USER [testAdmin1], with DISPLAY NAME [Test Admin 1], with AUTHORITIES [ROLE_ADMIN,ROLE_USER], with ORGANIZATION [Test Admin Organization], with EMAIL [testAdmin1@nowhere.com]with CREDENTIALS [CERTIFICATE LOGIN]

A successful PKI Certificate sign-in statement produces the following log statement at the debug level:

    DEBUG [02/15/2011 15:42:10 -0500] IP: 127.0.0.1 User: testAdmin1 [USER LOGIN]:LOGIN SUCCESS - ACCESS GRANTED USER [testAdmin1], with DISPLAY NAME [Test Admin 1], with AUTHORITIES [ROLE_ADMIN,ROLE_USER], with ORGANIZATION [Test Admin Organization], with EMAIL [testAdmin1@nowhere.com] with CREDENTIALS [CERTIFICATE LOGIN >> Signature Algorithm: [SHA1withRSA, OID = 1.2.840.113549.1.1.5]; Subject: [EMAILADDRESS=testAdmin1@nowhere.com, CN=testAdmin1, OU=Ozone, O=Ozone, L=Columbia, ST=Maryland, C=US]; Validity: [From: Thu Feb 04 13:58:52 EST 2010, To: Sun Feb 03 13:58:52 EST 2013]; Issuer: [EMAILADDRESS=ozone@nowhere.com, CN=localhost, OU=Ozone, O=Ozone, L=Columbia, ST=Maryland, C=US]; ]

###Logout Events

Sign-out events are logged by the `ozone.securitysample.authentication.audit.SecurityAuditLogger` logger as mentioned in the section, **Configuring Audit Log Levels**. This logger supports two levels of logging: info and debug, with the latter providing more detailed information about each sign-out event. 

Below is a typical user-initiated sign-out event which has been saved as a log entry, with the log level set to info:

    INFO  [02/03/2011 16:13:35 -0500] IP: 127.0.0.1 SessionID: 8ki2ttimdxc User: testAdmin1 [USER LOGOUT]:

Below is a typical user-initiated sign-out event which has been saved as a log entry, with the log level set to debug:

    DEBUG [02/03/2011 15:59:53 -0500] IP: 127.0.0.1 SessionID: 1tjefhsxz1x6t User: testUser1 [USER SESSION TIMEOUT] with ID [2], with EMAIL [testUser1@nowhere.com], with ACCOUNT CREATED DATE [02/03/2011 15:58:50 -0500], with LAST LOGIN DATE [02/03/2011 15:58:50 -0500]
 
A user can also be forced to sign-out when their session times out. Below are info and debug log statements:

    INFO  [02/07/2011 10:08:21 -0500] IP: 127.0.0.1 SessionID: 1b4nvaqnb0qx8 User: testAdmin1 [USER SESSION TIMEOUT]
	
    DEBUG [02/07/2011 10:24:21 -0500] IP: 127.0.0.1 SessionID: d0pq3g4xguv3 User: testAdmin1 [USER SESSION TIMEOUT] with ID [1], with EMAIL [testAdmin1@nowhere.com], with ACCOUNT CREATED DATE [02/07/2011 10:23:18 -0500], with LAST LOGIN DATE [02/07/2011 10:23:18 -0500]

###Auditing Login Attempts From Custom Security Modules
Audit logging of custom security modules can be achieved by adding logging capabilities via security authentication event listeners in the **/owf-security/OWFsecurityContext.xml** file, as in the case of the `ozone.securitysample.authentication.listener.AuthenticationSuccessListener` and `ozone.securitysample.authentication.listener.AuthenticationFailureListener` beans (both of which implement `org.springframework.context.ApplicationListener<org.springframework.security.authentication.event.AbstractAuthenticationEvent>` ) shown below:

```xml
    <!-- REQUIRED FOR AUDIT LOGGING OF AUTHENTICATION FAILURES -->
        <bean id="authenticationFailureListener" 	class="ozone. securitysample.authentication.listener.AuthenticationFailureListener"/>
    
    <!-- REQUIRED FOR AUDIT LOGGING OF AUTHENTICATION SUCCESS -->
        <bean id="authenticationSuccessListener"      	class="ozone. securitysample.authentication.listener.AuthenticationSuccessListener"/>
```

Once an onApplicationEvent event of type InteractiveAuthenticationSuccessEvent is fired in the Spring Security framework, the authenticationSuccessListener bean will be used to log the details of the successful authentication. Moreover, once an onApplicationEvent event of type AbstractAuthenticationFailureEvent is fired in the Spring Security framework, the authenticationFailureListener bean will be used to log the details of the failed authentication.

##Server Settings
All references to the CAS and OWF must match the settings of the current installation. Based on the settings in OzoneConfig.properties, the variables (e.g. ${ozone.host}) are filled in at runtime. Also, OzoneConfig.properties includes CAS configurations for OWF, Marketplace and the Metrics Service. 

<b>Table: OWFCasBeans.xml Server Settings</b>

<table>
    <tr>
      <th>Property</th>
      <th>Purpose</th>
      <th>Example</th>
    </tr>
    <tr>
      <td>casProcessingFilterEntryPoint.<br>loginUrl</td>
      <td>Must point to the<br> CAS login page.</td>
      <td>https://${ozone.host}:${ozone.port}/<br>${ozone.cas.serverLoginLocation} <br><i>(e.g. https://servername:port/cas/login)</i>
</td>
    </tr>
    <tr>
      <td>serviceProperties.<br>Service </td>
      <td>Must point to the<br> OWF web server.</td>
      <td>https://${ozone.host}:${ozone.port}/<br>${ozone.cas.owf.jSpringCasSecurity<br>CheckLocation} <br><i>(e.g. https://servername:port /owf/<br>j_spring_cas_security_check)</i>
</td>
    </tr>
    <tr>
      <td>ticketValidatorFactory.<br>casServiceUrl</td>
      <td>Must point to the<br> CAS server.</td>
      <td>https://${ozone.host}:${ozone.port}/<br>${ozone.cas.serverName}
<br><i>(e.g. https://servername:port/cas)</i></td>
    </tr>
    <tr>
      <td>ticketValidatorFactory.<br>proxyCallbackUrl</td>
      <td>Must point to the<br> OWF web server.</td>
      <td>https://${ozone.host}:${ozone.port}/<br>${ozone.cas.owf.serverSecure<br>ReceptorLocation} <br><i>(e.g. https://servername:port/prefs/<br>secure/receptor)</i>
</td>
    </tr>
</table>

<b>Table: OWFLogInOutBeans.xml Server Setting</b>

<table>
    <tr>
      <th>Property</th>
      <th>Purpose</th>
      <th>Example</th>
    </tr>
    <tr>
      <td>OzoneLogoutSuccessHandler/<br>constructor-arg/index=1</td>
      <td>Must point to the<br> CAS logout page.</td>
      <td>https://${ozone.host}:${ozone.port}/<br>${ozone.cas.serverLogoutLocation}
<br><i>(e.g. https://servername:port/cas/logout)</i>
</td>
    </tr>
</table>

##CASSpringOverrideConfig.xml File
**CASSpringOverrideConfig.xml** is a Spring framework override file, and should be deployed to the same server as **cas.war**, if using CAS as a security mechanism. Administrators should generally be focused with variable data in the following abridged section: 
 
```xml
    <bean id="openIdProviderController" class="org.jasig.cas.web.OpenIdProviderController" >
    <property name="loginUrl" value="https://${ozone.host}:${ozone.port}/${ozone.cas.serverLoginLocation}" />
    </bean>

    <bean class="ozone3.cas.adaptors.UserPropertiesFileAuthenticationHandler">
    <property name="propertyFileName" value="/users.properties"/>
    </bean>
```

If using CAS, the server needs to be configured to point to the CAS login screen. The following value would need to change in order to point CAS to the server login:

    https://${ozone.host}:${ozone.port}/cas/login 

If using **CASSpringOverrideConfig.xml** from a server without connectivity to the outside Internet, copy the **CASSpringOverrideConfig.xml** to the `\apache-tomcat-7.0.21-6.1.11\lib` folder. From there, the file will use classpath references to override the online Springframework URLs that the header points to during start up.

##JVM Memory Settings
Adjusting a server’s memory settings can increase performance or resolve permgen OutOfMemory errors. To adjust memory settings:

1.	In the Tomcat start script (`apache-tomcat-7.0.21\lib\start.sh` or `start.bat`) set the initial permgem size to at least 256 MB. This can be accomplished by adding -XX:PermSize=256m to the Java options. If more server memory is available, increasing this permgem size may increase performance.
2.	Set the maximum permgem size to at least 384 MB. This can be accomplished by adding -XX:MaxPermSize=384m to the Java options. If you have more memory available on your server increasing this permgem size may increase performance.
3.	If you have a server JVM, point to it when starting Java to increase performance. To do this, navigate to `serverjvm.dll` or add server flag –server to the deployment command line. 