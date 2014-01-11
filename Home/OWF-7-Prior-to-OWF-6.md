##Prior to OWF 6
There have been significant changes made to dashboards between previous versions of OWF and OWF 6. These changes demand that some conversion requirements be met if dashboards from previous versions of OWF are going to work in OWF 6.

### Dashboard Changes
The underlying structure of user and group dashboards has changed dramatically. In OWF 6, dashboards use a finite set of panes that can be combined through a graphical designer in a myriad of ways. This allows users to develop views that exceed the complexity and flexibility of dashboards from previous versions.  While the new Dashboard Designer can be used to mimic previous dashboard styles, there are fundamental changes that may prevent pixel-perfect translations from pre-OWF 6 dashboards to OWF 6 dashboards. As always, **full backups** of an OWF database should be performed and saved prior to conversion the OWF 6. Moreover, the database upgrade from OWF 5 to OWF 6 is more complex than prior upgrades.

### Dashboard Conversion Requirements
The database upgrade scripts provided in the OWF 6 release attempt to convert previous dashboards into OWF 6 dashboards that approximates the original behavior. Given the complexity of the conversions, there are additional requirements for running the conversion scripts in OWF 6.

For the OWF 6 upgrade, each conversion script contains scripted functions or stored procedures required to perform some of the more complicated data manipulations required by the new dashboard format. As an example, the PostgreSQL upgrade script contains PL/PGSQL code.  For this reason, scripts should be executed against their host database using native tools that can handle larger scripts. Tools that attempt to parse the scripts and chunk the data based on common SQL delimiters may fail (e.g., tools that rely on single statement JDBC connections).

> _Note:  While these upgrade scripts generally avoid the scripting constructs available only in the latest versions of supported databases, there could be some compatibility issues with older database servers. If this is the case, the scripts may be functional with minor edits. If that is not feasible, the conversion code can be removed from the upgrade script to allow upgrading of the table structures.  This will require that dashboards be recreated via the dashboard designer in OWF 6._

### Dashboard Conversions
Each of the primary dashboard types from previous versions of OWF have been converted to a new style.  While maintaining the useful characteristics of the dashboard types, the new formats differ slightly from their predecessors.

**Desktop Dashboard** – Desktops see the least amount of changes during the conversion. OWF 6 desktop dashboards look and act as their predecessors.

**Portal Dashboard** – Portals have a number of visual and functional differences from their counterparts.  Single, double, and triple column portals from previous versions of OWF will convert to OWF 6. The major visual differences include a lack of padding between widgets. Also, each column will scroll independently when widgets extend below the view of the browser. One functional change is the inclusion of splitters.  The edges of each column allow for resizing.

**Accordion Dashboard** – Accordions have been split into two accordion panes in OWF 6. Widgets on the left side of an older accordion will appear as they did in previous versions of OWF, displayed within a single column accordion pane. Widgets on the top and bottom of the right column of a previous version of OWF’s dashboards have been placed in their own accordion pane. This allows a user to add additional widgets on the right side of an accordion dashboard in OWF 6.

**Tabbed Dashboard** – Tabbed dashboards translate closely from previous versions of OWF to OWF 6 with one major functional change—they no longer support button widgets. During the conversion to OWF 6, any button widgets will be placed in normal tabs alongside any previous tabbed widgets.

### Dashboard Inspection and Validation
An OWF 6 administrator should verify the conversion of major dashboards through visual inspection prior to rolling out an upgraded instance to a user base. This will allow the administrator ample time to adjust to the changes and better inform their users. Minor changes to dashboards may be affected by editing the dashboard and using the new visual designer features. However, if major problems are discovered upon inspection or during the upgrade itself, normal support channels may be consulted. To aid the diagnosis of major problems, OWF 6 includes a basic validation utility. The validation utility may be used to discern potential problem dashboards in large installations or facilitate discussions with community support.

> _Note: The upgrade scripts create basic copies of the dashboard and dashboard_widget_state tables, named dashboard_backup and dashboard_widget_state_backup, respectively. These tables are used by the validation utility and can be deleted after the upgrade is verified and validated._

The validation utility can be found in the following location:
`owf-server-bundle/etc/tools/dbvalidation.zip` 

The file contains an executable JAR which connects to an OWF database through JDBC and validates that previous versions of OWF dashboards have been successfully converted to OWF 6 style.

**Instructions:**

1.	Extract the `dbvalidation.zip` to a temporary directory.
2.	Change directory to that temporary directory.
3.	Open `dbvalidation.jar/META-INF/MANIFEST.MF` file and add to Class-Path property to include JDBC driver on the classpath. 

 > _Note: OWF does not provide a JDBC driver for any database. Obtain the appropriate JDBC driver and place it into the Web server’s `dbvalidation.jar/lib` directory. Refer to Using JAR files: The Basics for instructions on how to extract and compress a JAR._ 

        Class-Path: lib/groovy-all-1.8.8.jar lib/{ jdbc-driver}.jar

4.	Save `MANIFEST.MF` file. Then, execute the following line:

        java -jar dbvalidation.jar

5.	There will be a prompt to enter the database URL, username, password and class name of the database driver.
6.	Upon completion, any encountered errors will be logged to console.
