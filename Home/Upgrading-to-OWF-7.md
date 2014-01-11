> _Note: Version 3.5.0 changed the way that OWF handles URLs. Bookmarks, favorite places, and locations of sample widgets which have been created or carried over from previous versions of OWF will no longer load correctly. If upgrading from a version of OWF prior to 3.5.0, the OWF team suggests that users log into OWF via the main URL, load the dashboards which are to be bookmarked, and re-save them. Previous bookmarks can be deleted._

1. Backup everything:
<br>Before starting the upgrade, backup the entire deployment of OWF and the corresponding database. Make sure all custom override configuration files have been included in the backup (In Tomcat, they are normally located in the `/lib` directory). 
2.	Install OWF:
<br>The following example shows how an administrator might copy and unzip OWF from the bundle on Unix or  operating systems:

            cp OWF-bundle-7-GA.zip/opt/.
            cd /opt
            unzip OWF-bundle-7-GA.zip
 The following example shows how an administrator might copy and unzip OWF from the bundle on Windows operating systems:
 * a. Create a new directory from where OWF will be run. This can be done via the Windows UI or the command prompt.
 * b. Copy **OWF-bundle-7-GA.zip** to the new directory created in step a.
 * c. Right-click on **OWF-bundle-7-GA.zip**, and select “open,” “explore” or the command for the system’s default zip/unzip program.
 * d. Unzip/unpack the bundle into the new directory created in step a.
<br>
<br>The use of the bundled deployment archive provides all of the necessary mechanisms to deploy and run the Tomcat Web container on any Java 1.6+ enabled system. If upgrading from a version of OWF prior to 3.5.0, please seek appropriate documentation for the specific build in question.
3. Upgrade database: 
<br>Before starting the database upgrade, shut down the older version of OWF’s server. Then run the upgrade script(s) that corresponds to the database in use. The scripts referenced below, which update from version 6.0.0, will also upgrade version 6.0.1, as well. The upgrade scripts for the current release are: 

        dbscripts\MySqlPrefsUpgrade_v6.0.0_v7.0.0.sql
        dbscripts\OraclePrefsUpgrade_v6.0.0_v7.0.0.sql
        dbscripts\PostgreSQLPrefsUpgrade_v6.0.0_v7.0.0.sql
        dbscripts\SQLServerPrefsUpgrade_v6.0.0_v7.0.0.sql
> _Note: If updating with MySQL, be sure to modify the SQL script (mentioned above) with the appropriate schema name. For example:_ `use OWF;`

4. Reconfigure and re-apply customizations: 
<br>The following override files were modified in OWF 7. Any changes made to this file under earlier versions of OWF will need to be manually merged with the newly deployed files. The file will then need to be moved to the 
`\apache-tomcat-7.0.21\lib` directory:

        \apache-tomcat-7.0.21\lib\OwfConfig.groovy
        \etc\override\CASSpringOverrideConfig.xml
5.	Below is an aggregate list of all of the imports needed for the widget APIs:

        <script type="text/javascript" src="js/dojo-1.2.3-windowname-only/dojo/dojo.js"></script>
        <script type="text/javascript" src="js/dojo-1.2.3-windowname-only/dojox/io/windowName.js"></script>
        <script type="text/javascript" src="js/dojo-1.2.3-windowname-only/dojox/secure/capability.js"></script>
        <script type="text/javascript" src="https://servername:port/owf/js-min/owf-widget-min.js"></script>
6.	Replace all occurrences of `https://servername:port` with the name of the server where OWF is running, for example, `https://www.yourcompany.com:8443`. Additionally, be sure to verify that the `windowname` library paths point to the local installation.
7.	If a custom keystore was deployed in a previous build, the keystore for OWF 7 will need to be manually configured in the same manner.
8.	Copy any custom certificates from previous build to OWF 7. Usually this is found in `\apache-tomcat-7.0.21\certs`. 
9.	 If custom changes were applied to a previous **owf.war** file, such as skinning. 
> _Note: With the upgrade to ExtJS 4.0.1, the way skinning is done has changed, using SASS and Compass to generate custom themes. In OWF 3.6.0, the OWF development team redesigned the application theme to follow this new model. The files to generate the new theme can be found in the \web-app\themes\owf-ext-theme directory of the exploded owf.war file. This theme, along with the examples on the Sencha website, can be used as guidelines for customizing the OWF theme._
 
The OWF upgrade is now complete.
