# How to deploy OWF 7.0 in WebLogic 11g (10.3.3)


## 1 Install WebLogic

1. Go to the [Oracle WebLogic download page](http://www.oracle.com/technetwork/middleware/weblogic/downloads/wls-main-097127.html) and download the appropriate WebLogic version for your operating system and licensing requirements.

2. Install WebLogic on your machine. You can find detailed installation instructions at the Oracle Fusion Middleware Documentation Library ([version 11.1.1](http://download.oracle.com/docs/cd/E14571_01/index.htm)). See the WebLogic Server product area therein.

3. Configure a domain by running the _Configuration Wizard_ from the **Start Menu -> All Programs -> Oracle WebLogic -> WebLogic Server 10gR3 -> Tools** folder. Alternatively the wizard may be run from _[webLogicHome]_`/wlserver_10.3/common/bin/config.sh` or `config.cmd` depending on your operating system. The location you specify for your domain will be referred to as _[domainHome]_ for the remainder of this document. (The default domain location is _[webLogicHome]_`/user_projects/domains/` _[name]_.)

4. Start up WebLogic per the instructions in the documentation. Make sure it's running by accessing the administration console at [http://localhost:7001/console](http://localhost:7001/console), assuming you selected the default installation settings.


## 2 Configure SSL

The default OWF configuration requires SSL to be enabled on the application server. Said configuration will use port 8080 for HTTP and 8443 for HTTPS (in contrast to 7001 and 7002 which are the corresponding defaults for WebLogic).

1. Login to the administration console with the user and password you specified during domain creation.

    > The default is user _weblogic_ with password _weblogic_.

2. Click on the _Servers_ link from the _Environment_ section. Select the appropriate server that will be used for the deployment from the list.

3. In the _General_ tab check the **SSL Listen Port Enabled** checkbox.

4. Set the **SSL Listen Port** to 8443 (or a port of your choice).

5. Set the **Listen Port** to 8080 (or a port of your choice).

6. Click the **Save** button. (If you changed the standard listen port from say 7001 to 8080 with the changes you just made the console will bump you out and the URL will redirect back to the login page on the new listen port. Otherwise you will get the page back with confirmation messages of a successful change if all went well. If you got presented with the console login page due to port change please login again.)

7. Copy the _[owfBundle]_`/apache-tomcat-7.0.21/certs/keystore.jks` file to your _[domainHome]_ directory. Said file contains the OWF development certificates and will serve as both a keystore and truststore for a demo configuration.

8. Click the _Keystores_ tab and select the _Custom Identity and Custom Trust_ option from the dropdown. Then click **Save**.

9. Enter the path and/or filename, type, and password for both the _Identity_ and the _Trust_. The path must either be absolute or relative to where the server was booted. Click **Save**.

10. Click the _SSL_ tab. Enter the appropriate **Private Key Alias** and corresponding passphrase. The development server certificate has an alias of _localhost_ and password of _changeit_.

11. Expand the _Advanced_ section in the _SSL_ tab. Select **Client Certs Requested But Not Enforced** from the **Two Way Client Cert Behavior** dropdown if you plan to use the default OWF security plug-in (X509 cert with CAS fall back). Select **None** in the **Hostname Verification** dropdown if you are using the development certs.

12. Set the keystore/trsustore path and passphrase for the JVM. For example, you can define the `SSL_VMARGS` variable in the _[domainHome]_/`startWebLogic.cmd` file as follows:

        set SSL_VMARGS=-Djavax.net.ssl.keyStore="keystore.jks" -Djavax.net.ssl.trustStore="keystore.jks" -Djavax.net.ssl.keyStorePassword="changeit" -Djavax.net.ssl.trustStorePassword="changeit"

    > * The sample above assumes the `keystore.jks` file is located in what will be the current working directory when the server is running.
    > * In order for SSL communication between OWF and CAS to succeed the truststore for the JVM that hosts CAS must include the certificate authority that signed the OWF server certificate.


## 3 Deploy OWF

1. Create a new _[domainHome]_`/autodeploy/owf.war` directory and unwar (unzip) the contents of the _[owfBundle]_`/apache-tomcat-7.0.21/webapps/owf.war` file into it.

2. Create a new _[domainHome]_`/autodeploy/owf.war/WEB-INF/weblogic.xml` file with the following content:

        <weblogic-web-app>
            <context-root>/owf</context-root>
            <container-descriptor>
                <prefer-web-inf-classes>true</prefer-web-inf-classes>
            </container-descriptor>
        </weblogic-web-app>

3. Additional OWF resources and configuration files must be added to the `CLASSPATH`. Copy the following files and directories from the _[owfBundle]_`/apache-tomcat-7.0.21/lib` directory to the _[domainHome]_ directory:

        owf-override-log4j.xml
        OwfConfig.groovy
        OWFsecurityContext.xml
        OzoneConfig.properties
        users.properties
        js-plugins/
        ozone-security-beans/

    > Alternatively you may use the [AppFileOverride](http://download.oracle.com/docs/cd/E12839_01/web.1111/e13702/config.htm#i1066493) feature of WebLogic deployment plans in order to host the above files and directories.

4. _**(Optional)**_ Copy the _[owfBundle]_`/apache-tomcat-7.0.21/prodDb.script` file to the _[domainHome]_ directory. This step is only necessary when using the development HyperSQL database.

    > The HyperSQL database system is **not** recommended for production use.


## 4 Deploy CAS

1. Create a new _[domainHome]_`/autodeploy/cas.war` directory and unwar (unzip) the contents of the _[owfBundle]_`/apache-tomcat-7.0.21/webapps/cas.war` file into it.

2. Create a new _[domainHome]_`/autodeploy/cas.war/WEB-INF/weblogic.xml` file with the following content:

        <weblogic-web-app>
            <context-root>/cas</context-root>
        </weblogic-web-app>


## 5 Starting OWF in WebLogic

1. Open a command prompt. Navigate to the _[domainHome]_ directory. Then execute the `startWebLogic.cmd` or `startWebLogic.sh` script.

2. Navigate to [https://localhost:8443/owf](https://localhost:8443/owf) in your web browser. Authenticate using client certificates or CAS.