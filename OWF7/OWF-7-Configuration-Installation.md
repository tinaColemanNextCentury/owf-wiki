#1 Installation

#1 Dependencies

Listed below are the dependencies for OWF:

* Java 1.6 or higher.
* A Relational Database Management System (RDBMS). OWF currently ships with an in-memory HyperSQL (HSQLDB) database for testing and development purposes, but it is expected that a live deployment will use a more robust RDBMS such as Oracle or MySQL.

##Supported Browsers
OWF supports Internet Explorer 7 and higher and Firefox 3.6 and higher. OWF is tested against the following browsers:

* Internet Explorer 7 & 9
* Firefox 3.6 & 15

##OWF Bundle Description
The distribution of OWF consists of a ZIP file containing the necessary components to set up and run OWF in a development environment. The bundle contains the following:

* Tomcat-7.0.21 (Simple Java Web Container)
* Sample PKI Certificates for SSL (sample user certificates and server certificate)
* OWF Web application ( **owf.war** )
* Central Authentication Service application ( **cas.war** ) 
* Externalized Security Configurations found in the owf-security directory located inside **OWF-bundle-7-GA.zip**.
* Tomcat start scripts (`start.sh` or `start.bat`)
* The following developer-configurable externalized properties files:
   * **OwfConfig.groovy**
   * **CASSpringOverrideConfig.xml**
   * **OzoneConfig.properties**

The following example shows how an administrator might copy, unzip and start OWF from the bundle deployment on \*nix operating systems, assuming the bundle is named **OWF-bundle-7-GA.zip**:

    cp OWF-bundle-7-GA.zip/opt/.
    cd /opt
    unzip OWF-bundle-7-GA.zip
    cd apache-tomcat-7.0.21
    ./start.sh

The following example shows how an administrator might copy, unzip, and start OWF from the bundle on Windows operating systems, assuming the bundle is named **OWF-bundle-7-GA.zip**:

1.	Create a new directory from where OWF will be run. This can be done via the Windows UI or a command prompt.
2.	Copy **OWF-bundle-7-GA.zip** to the new directory created in step 1.
3.	Right-click on **OWF-bundle-7-GA.zip** and select `open, explore` or the command for the system’s default zip/unzip program.
4.	Unzip/unpack the bundle into the new directory created in step 1.
5.	From a command-line, run `start.bat` from within the `apache-tomcat-7.0.21` directory.

The use of the bundled deployment archive provides all of the necessary mechanisms to deploy and run the Tomcat Web container on any Java 1.6+ enabled system.

#2 Default Installation

Running the OWF Bundle via the included Tomcat Web server with the default values requires minimal installation. With standard configuration, OWF makes use of the default authentication module, which provides X509 authentication/authorization, with CAS as a fallback if the framework cannot authenticate the user via certificates installed in their browser.

> _Note: If OWF 7 is installed as an upgrade, please see [Upgrading to OWF 7](Upgrading-to-OWF-7)._

The application uses a `KeyStore` and a `Truststore` which are local to the installation. There is no need to install any certificates into the server’s Java installation. The default certificates contained in the OWF Bundle only function for `localhost` communications. When accessed from a remote machine with a name that differs from `localhost`, while using the included certificates, OWF will not function correctly. Accordingly, see 3.5.5: Server Certificate Creation and Installation for information about creating additional certificates. 

###Installing User PKI Certificates
By default, the security infrastructure of the OWF Bundle is configured to use client certificates with CAS fallback. In order to identify themselves via certificates, clients need to install a PKI certificate into their Web browser. The client certificates that are included with the OWF bundle will be recognized immediately and can be used in the default security configuration. The certificates are located in the `\apache-tomcat-7.0.21\certs` directory of the OWF bundle. 

The default client certificates can be used by importing the included `testUser1.p12` or `testAdmin1.p12` certificate into the user’s browser. In Internet Explorer, client certificates can be added by selecting Tools -> Internet Options -> Content -> Certificates -> Personal, and then clicking the Import button. The certificate `testUser1` grants rights to use the application, while `testAdmin1` is a certificate for a user granted both user rights and administrator rights. The private key password for both certificates is `password`.

In Firefox, this menu is accessed via Tools -> Options -> Advanced -> Encryption -> View Certificates ->Your Certificates -> Import. 

> _Note: Depending on the browser, importing certificates may cause warning messages to be displayed before accessing OWF. Web browsers will allow exceptions to be added to permit usage of these certificates the first time they are accessed._

##Custom Installation
OWF can be customized to run in a variety of environments. The following sections detail how to change default database settings and set up security.

> _Note: If OWF 7 is being installed as an upgrade, please see [Prior to OWF 6](/ozoneplatform/owf/wiki/OWF-7-Prior-to-OWF-6)._

#3  Database Setup
While the full extent of administering databases is outside the scope of this guide, this section provides information on how to work with databases for OWF.

**OwfConfig.groovy** is an OWF configuration file that allows an administrator to modify database connectivity information. It is located in the `\apache-tomcat-7.0.21\lib` directory. Once changes are made, restart the system to apply them. Developers comfortable with the Groovy language and the Grails Web application framework should be comfortable writing additional code for the file. 

Listed below are the variable database elements that need to be modified to customize the OWF preferences database. A detailed explanation of each field follows in the table, OWF Externalized Database Properties:

```groovy
    dataSource {
        pooled = true
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
```

**Table: OWF Externalized Database Properties**

<table>
    <tr>
      <th>Property</th>
      <th>Purpose</th>
      <th>Example</th>
    </tr>
    <tr>
      <td>dbCreate</td>
      <td>The way the database is created/updated when the server is started
<br>Note: Use the appropriate database creation script in the dbscript folder before running OWF.
</td>
      <td>None</td>
    </tr>
    <tr>
      <td>username</td>
      <td>The Username for the database connection</td>
      <td>admin</td>
    </tr>
    <tr>
      <td>Password</td>
      <td>The password for the database connection</td>
      <td>Password</td>
    </tr>
    <tr>
      <td>driverClassName</td>
      <td>JDBC driver</td>
      <td>org.hsqldb.jdbcDriver</td>
    </tr>
    <tr>
      <td>url</td>
      <td>JDBC Connection String</td>
      <td>jdbc:hsqldb:file:prodDb;
shutdown=true
</td>
    </tr>
    <tr>
      <td>Pooled</td>
      <td>Enable database connection pooling when true</td>
      <td>True</td>
    </tr>
    <tr>
      <td>minEvictableIdleTimeMillis</td>
      <td>Minimum amount of time in milliseconds an object	 can be idle in the pool before becoming eligible for eviction</td>
      <td>18000</td>
    </tr>
    <tr>
      <td>timeBetweenEvictionRunsMillis</td>
      <td>Time in milliseconds to sleep between runs of the idle
 object evictor thread </td>
      <td>18000</td>
    </tr>
    <tr>
      <td>numTestsPerEvitionRun</td>
      <td>Number of objects to be examined on each run of the idle evictor thread</td>
      <td>3</td>
    </tr>
    <tr>
      <td>testOnBorrow</td>
      <td>When true, objects are validated before borrowed from the pool</td>
      <td>true</td>
    </tr>
    <tr>
      <td>testWhileIdle</td>
      <td>When true, objects are validated by the idle object evictor thread</td>
      <td>true</td>
    </tr>
    <tr>
      <td>testOnReturn</td>
      <td>When true, objects are validated before returned to the pool</td>
      <td>true</td>
    </tr>
    <tr>
      <td>validationQuery</td>
      <td>Validation query, used to test connections before use
<br> Note: Syntax varies by database, see the examples included in this document.</td>
      <td>SELECT 1 FROM <br>INFORMATION_SCHEMA.<br>SYSTEM_USERS</td>
    </tr>
</table>

> _Note: When setting up databases for OWF, be mindful of the database’s Lexical sorting mechanism. For some instances of OWF, with a small handful of users, this may not be much of an issue, but as the database becomes more populated, sorting may become increasingly difficult to manage._

##Using Oracle
1.	Create an Oracle database user for OWF. It is recommended that there be a dedicated user for OWF to avoid database object name collisions. The OWF team recommends using UTF-8 encoding.
2.	Due to licensing issues, OWF does not provide a JDBC driver for Oracle. Obtain the appropriate JDBC driver and place it into the Web server’s classpath. For example, if running Tomcat, the driver can be placed in the `\apache-tomcat-7.0.21\lib` directory. 
3.	Open the **\apache-tomcat-7.0.21\lib\OwfConfig.groovy** file and modify the `environments -> production -> dataSource` section using the values that are appropriate for the OWF environment. For example:

 ```groovy
        dataSource {
            pooled = true
            dbCreate = "none"
            username = "owf_user"
            password = "owf_password"
            dialect = "org.hibernate.dialect.Oracle10gDialect"
            driverClassName = "oracle.jdbc.driver.OracleDriver"
            url = "jdbc:oracle:thin:@myhost.somewhere.org:1521:DEVDB1"
            properties {
                minEvictableIdleTimeMillis = 180000
                timeBetweenEvictionRunsMillis = 180000
                numTestsPerEvictionRun = 3
                testOnBorrow = true
                testWhileIdle = true
                testOnReturn = true
                validationQuery = "SELECT 1 FROM DUAL"
            }
        }
 ```

  In the example above, an Oracle database-user named `owf_user` with a password of `owf_password` is used for a database named DEVDB1.

  There are several different types of Oracle drivers (thin, OCI, kprb) and connection options (service, SID, TNSName) available. Please consult the Oracle DBA and Oracle’s JDBC documentation to create the connection most appropriate for the installed environment.

4. To create the schema, run the `\dbscripts\OraclePrefsInitialCreate.sql` script, prior to starting OWF. 

5. Ensure that the transaction is committed. 

> _Note: If running a production environment, no additional steps are necessary. However, if sample widgets are to be installed, `OraclePrefsUpdate_v7.0.0.sql` must be run prior to logging in. Logging in between the execution of these scripts can cause system failure._

> _Note: The OWF team is aware of a known issue with the Oracle Web-based Admin Console returning truncated characters when dealing with large data sets. Accordingly, using SQLPlus to run the script mentioned above is recommended._

##Using MySQL

* Create a schema within MySQL for use with OWF. It is recommended that there be a dedicated schema for OWF to avoid database object name collisions. The OWF team recommends using UTF-8 encoding.
* Create a MySQL User with full access to the OWF schema created above.
* OWF does not provide a JDBC driver for MySQL. Obtain the appropriate JDBC driver and place it into the Web server’s classpath. For example, if running Tomcat, the driver can be placed in the `\apache-tomcat-7.0.21\lib` directory.
* Open the **\apache-tomcat-7.0.21\lib\OwfConfig.groovy** file and modify the `environments -> production -> dataSource` section using the values that are appropriate for the OWF environment. 

For example:

```groovy
    dataSource {
        pooled = true
        dbCreate = "none"
        driverClassName = "com.mysql.jdbc.Driver"
        url="jdbc:mysql://myhost.somewhere.org/owf"
        username = "owf_user"
        password = "owf_password"
        dialect = "org.hibernate.dialect.MySQL5InnoDBDialect"
        properties {
            minEvictableIdleTimeMillis = 180000
            timeBetweenEvictionRunsMillis = 180000
            numTestsPerEvictionRun = 3
            testOnBorrow = true
            testWhileIdle = true
            testOnReturn = true
            validationQuery = "SELECT 1"
        }
       }
```

   In the example above, a MySQL database-user named `owf_user` with a password of `owf_password` is used, for a database named owf. The dialect `org.hibernate.dialect.MySQL5InnoDBDialect` will use the `InnoDB` engine which is recommended for interactive webapps and explicitly used as the engine on OWF create and upgrade scripts.

* Create the schema by running the `\dbscript\MySqlPrefsInitialCreate.sql` script, prior to starting OWF.

> _Note: If manually creating the database objects, be sure to modify the SQL script (mentioned above) with the appropriate schema name. For example: 
`use owf;`_

> _Note: If running a production environment, no additional steps are necessary. However, if sample widgets are to be installed, `MySqlPrefsUpdate_v7.0.0.sql` must be run prior to logging in. Logging in between the execution of these scripts can cause system failure._

##Using PostgreSQL

1.	Create either a new login role or a new schema in order to avoid database object name collisions between OWF and other database applications.
2.	Edit the user so that it can create database objects. 
3.	Create a new database. Use UTF-8 as encoding (default).
4.	OWF does not provide a JDBC driver for PostgreSQL. Obtain the appropriate JDBC driver and place it into the Web server’s classpath. For example, if running Tomcat, the driver can be placed in the `\apache-tomcat-7.0.21\lib` directory.
5.	Open the **\apache-tomcat-7.0.21\lib\OwfConfig.groovy** file and modify the `environments -> production -> dataSource` section using the values that are appropriate for the OWF environment. 
 For example:

 ```groovy
        dataSource {
            pooled = true
            dbCreate = "none"
            username = "owf_user"
            password = "owf"
            driverClassName = "org.postgresql.Driver"
            url = "jdbc:postgresql://localhost:5432/OWF"
            dialect="org.hibernate.dialect.PostgreSQLDialect"
            properties {
                minEvictableIdleTimeMillis = 180000
                timeBetweenEvictionRunsMillis = 180000
                numTestsPerEvictionRun = 3
                testOnBorrow = true
                testWhileIdle = true
                testOnReturn = true
                validationQuery = "SELECT 1"
            }
        }
 ```

  In the example above, a PostgreSQL database user named owf_user with a password of owf is used, for a database named OWF. 
6.	Create the schema by running the `\dbscript\PostgreSQLPrefsInitialCreate.sql` script before starting OWF.
7.	If OWF is being installed as a production environment, this can serve as the final step. However, if sample data is required (e.g., creating a testing environment), the remaining steps can be followed.
 > _Note: If sample data scripts ( mentioned in step 7) are to be run, script execution must take place before logging into OWF. Logging in before the execution of the script can cause system failure._
8.	Open the administration tool for PostgreSQL (pgAdmin III), connect to the OWF server as `owf_user`, and select the SQL icon.
9.	When the query window opens, select `File -> Open` and navigate to `\dbscripts\PostgreSQLPrefsUpdate_v7.0.0.sql` in the bundle.

 > _Note: ONLY run this script against an empty database as it will delete pre-existing data._

10.	Execute the script.

##Using SQL Server

1.	Create a new SQL Server database for use with OWF.
2.	Create a SQL Server user with full access to the OWF database created above.
3.	OWF does not provide a JDBC driver for SQL Server. Obtain the appropriate JDBC driver and place it on the Web server’s classpath. For example, if running Tomcat, the driver can be placed in the `\apache-tomcat-7.0.21\lib` directory.
4.	Open the **\apache-tomcat-7.0.21\lib\OwfConfig.groovy** file and modify the `environments  production -> dataSource` section using the values that are appropriate for the OWF environment. 
  For example:

 ```groovy
        dataSource {
            pooled = true
            dbCreate = "none"
            username = "owf_user"
            password = "owf"
            driverClassName = "net.sourceforge.jtds.jdbc.Driver"
            url = "jdbc:jtds:sqlserver://localhost:1443/OWF"
            dialect="ozone.owf.hibernate.OWFSQLServerDialect"
            properties {
                minEvictableIdleTimeMillis = 180000
                timeBetweenEvictionRunsMillis = 180000
                numTestsPerEvictionRun = 3
                testOnBorrow = true
                testWhileIdle = true
                testOnReturn = true
                validationQuery = "SELECT 1"
            }
        }
 ```

  In the example above the SQL Server database user named `owf_user` with password of `owf` is used, to access a database named OWF.
5.	Create the schema by running the `SQLServerPrefsInitialCreate.sql` script, prior to starting OWF.
If sample data is required (e.g., creating a testing environment), the remaining steps can be followed.
> _Note: If sample data scripts (as mentioned in step 5) are to be run, script execution must take place before logging into OWF. Logging in before the execution of the script can cause system failure._
6.	Open Microsoft SQL Server Management Studio (or another database editing tool) and select File -> Open File.
7.	Navigate to `\dbscripts\SQLServerPrefsUpdate_v7.0.0.sql` in the bundle.
> _Note: This script should ONLY be run against an empty database as it will delete pre-existing data._
8.	 Select the OWF database, and execute the script.

#4   Security Setup
OWF provides a modular security approach that is based on Spring Security. All of the provided options supply both a Spring Security configuration file and Java classes that are written to Spring’s security interfaces in order to perform authentication and authorization. For more details, please refer to the [OWF Security](OWF-7-Configuring-OWF-Security) page. 

##Installing the Security Module
The OWF-security files, provided in the distribution bundle, offer multiple examples of security options. These are intended as examples and should in no way be used in a production environment. The default security implementation provides an X509 certificate authentication with CAS fallback. When using the default security module in a testing environment, the user must present a valid X509 certificate, or a valid CAS login, in order to gain access to OWF. Some of the CAS fields can be customized using the `OzoneConfig.properties` (see the section **Customizing CAS** on the [OWF Security](OWF-7-Configuring-OWF-Security) page).

For each available security option, there is a specific XML file which must be installed. Installing a new security module is accomplished in just a few simple steps. For more details, please refer to the [OWF Security](OWF-7-Configuring-OWF-Security) page. 

#5   Operating OWF From Different/Multiple Ports
Initial OWF configuration is set up so that Tomcat can be run from a local installation.

Throughout this document, `servername:port` implies a `localhost:8080` or `localhost:8443` location. The example below shows how to set up OWF so that it can be used on `5050/5443` through the default security module. 
To enable ports other than `8080/8443` while using Spring Security, the desired ports need to be explicitly edited in Web server configuration file: **conf/server.xml**.

> _Note: In the event that OWF is running on a server where a port number is already in use, OWF must run from a different port number. Two applications cannot bind to the same port._

1.	For example, in Tomcat, change the port numbers in **conf/server.xml**from: 
        Connector port="5050" protocol="HTTP/1.1" 
               connectionTimeout="20000" 
               redirectPort="5443" />

 To:

        Connector port="5443" protocol="HTTP/1.1" SSLEnabled="true"
               maxThreads="150" scheme="https" secure="true"
               keystoreFile="certs/keystore.jks" keystorePass="changeit"	       
               clientAuth="false" sslProtocol="TLS" />
 * A.	Ports 5050 and 5443 are just examples and can be changed to whatever is needed.
If OWF was running on a server where a port number was already in use, the `shutdown` port must also be changed. To do this, change the port number in the Tomcat Web server configuration file **\apache-tomcat-7.0.21\conf\server.xml** to another port, in the following example the default shutdown port was changed from 8005 to 8006:

            Server port="8006" shutdown="SHUTDOWN"
 * B.	Ensure that the port value used in the Web server configuration file matches the port value used in `\apache-tomcat-7.0.21\lib OzoneConfig.properties` which is shown below, displaying the default port and host information:

            ozone.host = localhost
            ozone.port = 5443
            ozone.unsecurePort = 5050
2.	Save both files. 
3.	Restart the OWF server.

#6   Adding Marketplace or Metrics Service To OWF
The flexible and scalable nature of OWF allow for applications used in concert (such as Marketplace or the Metrics Service) to be included in OWF’s deployment for testing purposes.  This allows a user to develop with the products working together, without having to activate multiple ports via configuration.

To include Marketplace or Metrics Service in the OWF bundle, do the following:

1.	Unpack the zipped bundles containing the applications to be included.
2.	Navigate to `apache-tomcat-7.0.21/webapps` in each unpacked bundle.
3.	 Copy the appropriate WAR files into the `apache-tomcat-7.0.21/webapps` directory where OWF was deployed.
4.	Restart the OWF server.

>Note: If using a Marketplace release earlier than version 5, the following file must also be copied to the deployed OWF’s `/apache-tomcat-7.0.21/lib` directory:  
**/apache-tomcat-7.0.21/lib/MPsecurityContext.xml**

#7   Server Certificate Creation and Installation
Valid server certificates are needed for configuring the server to allow https authentication. 

> _Note: Self-signed certificates will produce warnings in a user’s browser. This is because a self-signed certificate, not signed by a recognized certificate authority, has no one authorizing its validity. In a production environment, certificates should be signed by a recognized certificate authority, such as an organization’s internal certificate authority._

##Generating a New Self-Signed Server Certificate
A new self-signed certificate can be generated by navigating to the \etc\tools directory and executing `create-certificates.bat` or `.sh`, depending on the operating system in use.

Follow the on-screen prompts and create the necessary certificates for the installation. 

Make sure to enter the FULLY QUALIFIED server name. This needs to match the hostname of the machine exactly or the certificate will not work correctly.

If  using an IP address as the Common Name (CN), an entry must be added to the Subject Alternative Name entry in the certificate. The better alternative to using an IP address is to add a name/IP pair to the hosts file and register the name as the CN. 

##Configuring OWF For a Different Truststore/Keystore
1.	For server-to-server calls (OWF-to-CAS communications, for example) the newly created self-signed certificate should be imported into the truststore. If the truststore is a separate file from the keystore, the certificate can be copied from the keystore to the truststore as follows:
    * A.	Export the certificate from the KeyStore into a file: 
`keytool -export -file servername.crt -keystore servername.jks -alias servername`
    * B.	Import the file into the Truststore:
`keytool -import -alias servername –keystore mytruststore.jks -file servername.crt`
2.	Modify the JVM Parameters that are used to start the Web application server in order to use the new Truststore shown above. If a Tomcat server is being used, the parameters can be found in the `setenv.bat` (or `.sh`, depending on the operating system in use) script found within the `\apache-tomcat-7.0.21\bin` folder inside of the unpacked **OWF-bundle-7-GA.zip**. If an application server other than Tomcat is being used, the parameters will need to be added to the JVM parameters which are loaded when the application server is started. 

<b>Table: Custom JVM Parameters</b>

<table>
    <tr>
      <th>Parameter</th>
      <th>Note</th>
    </tr>
    <tr>
      <td>-Djavax.net.ssl.keyStore= "%CATALINA_HOME%\certs\keystore.jks"</td>
      <td>Replace ‘certs/keystore.jks’ with the path and filename to the keystore.</td>
    </tr>
    <tr>
      <td>-Djavax.net.ssl.trustStore= "%CATALINA_HOME%\certs\keystore.jks"</td>
      <td>Replace ‘certs/keystore.jks’ with the path of the truststore (May be the same as the keystore).</td>
    </tr>
    <tr>
      <td>-Djavax.net.ssl.keyStorePassword= changeit </td>
      <td>Replace ‘changeit’ with the keystore’s password (if applicable) </td>
    </tr>
    <tr>
      <td>-Djavax.net.ssl.trustStorePassword=changeit</td>
      <td>Replace 'changelt' with the truststore's password.</td>
    </tr>
</table>

Finally, the server configuration must be modified to use the new KeyStore/Truststore in SSL. Below is the relevant section from the Tomcat configuration script found in **\apache-tomcat-7.0.21\conf\server.xml**:

```xml
    Connector port="8443"
    protocol="HTTP/1.1"
    SSLEnabled="true"
    maxThreads="150"
    scheme="https"
    secure="true"
    keystoreFile="certs/keystore.jks" 
    keystorePass="changeit"
    truststoreFile=”certs/truststore.jks”
    truststorePass=”changeit”
    clientAuth="want"
    sslProtocol="TLS" /
```