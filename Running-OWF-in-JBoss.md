# Running OWF in JBoss

## 1 Introduction
This document describes how to run OWF 7 in JBoss. It is intended to serve as an example of hosting OWF in a Java Servlet container other than the default, Apache Tomcat. The steps that follow will configure OWF to use x509 certificate authentication only. Consult JBoss documentation for information on performance tuning and security lock-down.

## 2 Requirements
1. You must have a properly built OWF 7 distribution. For the purpose of this document _**[owfBundle]**_ refers to the _**staging**_ directory in your OWF source tree.

2. Download the JBoss Application Server package (i.e. jboss-5.1.0.GA.zip, jboss-as-7.1.1.Final.zip, etc.). Unzip the contents to your desired installation location. The root directory of your unzipped JBoss package will be referred to as _**[jBossHome]**_ below.

## 3 OWF Deployment

The following subsections describe how to configure and run OWF in certain versions of JBoss.

### JBoss 7

#### 1. Create a module for configuration files

- Create a _**ozone/configuration/main**_ directory under the _**[jBossHome]/modules**_ directory.

- Copy the following files and directories from the _**[owfBundle]/apache-tomcat-7.0.21/lib**_ directory to the _**[jBossHome]/modules/ozone/configuration/main**_ directory:

        OwfConfig.groovy
        owf-override-log4j.xml
        OzoneConfig.properties
        users.properties
        js-plugins/
        ozone-security-beans/

- Copy the _**[owfBundle]/owf-security/OWFsecurityContext_cert_only.xml**_ file to the _**[jBossHome]/modules/ozone/configuration/main**_ directory. Said file configures OWF to use certificate only authentication.

    > NOTE: You must delete the default _**OWFsecurityContext.xml**_ file from the _**main**_ directory if you copied it there in the previous step.

- In the _**[jBossHome]/modules/ozone/configuration/main**_ directory create a _**module.xml**_ file with the following content:

        <?xml version="1.0" encoding="UTF-8"?>
        <module xmlns="urn:jboss:module:1.1" name="ozone.configuration">
            <resources>
                <resource-root path="."/>
            </resources>
            <dependencies>
            </dependencies>
        </module>

#### 2. Setup the OWF web application

- Create a _**owf.war**_ directory in the _**[jBossHome]/standalone/deployments**_ directory.

- Unwar (unzip) the contents of the _**[owfBundle]/apache-tomcat-7.0.21/webapps/owf.war**_ file into the _**[jBossHome]/standalone/deployments/owf.war**_ directory.

- In the _**[jBossHome]/standalone/deployments/owf.war/WEB-INF**_ directory create a _**jboss-deployment-structure.xml**_ file with the following content:

        <?xml version="1.0" encoding="UTF-8"?>
        <jboss-deployment-structure>
            <deployment>
                <!-- Do not use the built-in log4j that ships with JBoss -->
                <exclusions>
                    <module name="org.apache.log4j" />
                </exclusions>
                <!-- Include external configuration module for OWF -->
                <dependencies>
                    <module name="ozone.configuration"/>
                </dependencies>
            </deployment>
            <!-- Use log4j that ships with OWF -->
            <module name="deployment.log4j">
                <resources>
                    <resource-root path="log4j-1.2.16.jar" />
                </resources>
            </module>
        </jboss-deployment-structure>

- Remove invalid OSGI headers from the OWF application. Delete all lines except those beginning with **Manifest-Version** and **Created-By** from the _**[jBossHome]/standalone/deployments/owf.war/META-INF/MANIFEST.MF**_ file.

- Create an empty _**owf.war.dodeploy**_ file in the _**[jBossHome]/standalone/deployments**_ directory.

#### 3. Configure HTTPS

- Copy the _**[owfBundle]/apache-tomcat-7.0.21/certs/keystore.jks**_ file to the _**[jBossHome]/standalone/configuration**_ directory and rename it as _**owf-keystore.jks**_ (to avoid naming conflicts).

- In the _**[jBossHome]/standalone/configuration/standalone.xml**_ file find the _**subsystem**_ whose _xmlns_ is _**urn:jboss:domain:web:1.1**_ and add the following connector element as a child:

        <connector name="https"
         protocol="HTTP/1.1"
         scheme="https"
         socket-binding="https"
         secure="true">
            <ssl name="ssl"
             password="changeit"
             certificate-key-file="${jboss.server.config.dir}/owf-keystore.jks"
             protocol="TLSv1"
             verify-client="want"
             ca-certificate-file="${jboss.server.config.dir}/owf-keystore.jks" />
        </connector>

#### 4. (Optional) HSQL database setup

The OWF distribution is configured to use a HSQL database by default. The following step should only be performed if using the HSQL database.

- Copy the _**[owfBundle]/apache-tomcat-7.0.21/prodDb.script**_ file to the _**[jBossHome]/bin**_ directory.

    > NOTE: The HSQL database that ships with OWF is intended for development purposes. It should **not** be used in production. You can change the database in the _**[jBossHome]/modules/ozone/configuration/main/OwfConfig.groovy**_ file.

#### 5. Run JBoss

- Navigate to the _**[jBossHome]/bin**_ directory (via a command prompt or file explorer).

- Execute the _**standalone.sh**_ script (or _**standalone.bat**_).

    > NOTE: When starting the JBoss server the _**prodDb.script**_ file must be in the current working directory if using the HSQL database.

### JBoss 5 and 6

#### 1. Create a new server configuration for OWF

- Copy the contents of the _**[jBossHome]/server/default**_ directory to a new directory. It can have any name, but we will call it _**owf7**_ for the purpose of this guide.

    > NOTE: JBoss configurations other than _**default**_ should work fine as a template for OWF, although not every one has been tested. Please report any issues encountered on the Google group.

- Copy the following files and directories from the _**[owfBundle]/apache-tomcat-7.0.21/lib**_ directory to the _**[jBossHome]/server/owf7/conf**_ directory:

        OwfConfig.groovy
        OzoneConfig.properties
        users.properties
        js-plugins/
        ozone-security-beans/

- Copy the _**[owfBundle]/owf-security/OWFsecurityContext_cert_only.xml**_ file to the _**[jBossHome]/server/owf7/conf**_ directory. Said file configures OWF to use certificate only authentication.

    > NOTE: You must delete the default _**OWFsecurityContext.xml**_ file from the _**conf**_ directory if you copied it there in the previous step.

#### 2. Setup the OWF web application

- Create a _**owf.war**_ directory in the _**[jBossHome]/server/owf7/deploy**_ directory.

- Unwar (unzip) the contents of the _**[owfBundle]/apache-tomcat-7.0.21/webapps/owf.war**_ file into the _**[jBossHome]/server/owf7/deploy/owf.war**_ directory.

- Remove JTA library that conflicts with JBoss. Delete the _**[jBossHome]/server/owf7/deploy/owf.war/WEB-INF/lib/jta-1.1.jar**_ file.

#### 3. Configure HTTPS

- Copy the _**[owfBundle]/apache-tomcat-7.0.21/certs/keystore.jks**_ file to the _**[jBossHome]/server/owf7/conf**_ directory.

- Add the following connector entry to your _**[jBossHome]/server/owf7/deploy/jbossweb.sar/server.xml**_ file:

        <Connector
         protocol="HTTP/1.1"
         SSLEnabled="true"
         port="8443"
         address="${jboss.bind.address}"
         scheme="https"
         secure="true"
         clientAuth="want"
         keystoreFile="${jboss.server.home.dir}/conf/keystore.jks"
         keystorePass="changeit"
         truststoreFile="${jboss.server.home.dir}/conf/keystore.jks"
         truststorePass="changeit"
         sslProtocol = "TLS" />

#### 4. (Optional) HSQL database setup

The OWF distribution is configured to use a HSQL database by default. The following step should only be performed if using the HSQL database.

- Copy the _**[owfBundle]/apache-tomcat-7.0.21/prodDb.script**_ file to the _**[jBossHome]/bin**_ directory.

    > NOTE: The HSQL database that ships with OWF is intended for development purposes. It should **not** be used in production. You can change the database in the _**[jBossHome]/server/owf7/config/OwfConfig.groovy**_ file.

#### 5. Run JBoss

- Open a command prompt and navigate to the _**[jBossHome]/bin**_ directory.

- Start JBoss using the _owf7_ configuration defined in the previous sections. Enter one the following in your command prompt (depending on your platform):

        ./run.sh -c owf7

    _or_

        run.bat -c owf7

    > NOTE: When starting the JBoss server the _**prodDb.script**_ file must be in the current working directory if using the HSQL database.

## 4 Client Browser Configuration

Since we have configured OWF to use certificate only authentication above we must import the appropriate certificates into each web browser that will access OWF.

1. Open your web browser's certificate manager.

    > In Firefox:
    > * Open the _Preferences_ menu and go the _Advanced_ settings.
    > * Click the _View Certificates_ button in the _Encryption_ tab.

2. Import either the _**testUser1.p12**_ or _**testAdmin1.p12**_ certificate file. Said files must be unlocked using "password" (no quotes) as the password. The noted example certificates are located under the _**[owfBundle]/apache-tomcat-7.0.21/certs**_ directory.

    > NOTE: The certificate file you import into your browser must correspond to one that exists in the _**keystore.jks**_ (or _**owf-keystore.jks**_) file that JBoss is using for HTTPS.

3. When you access the OWF web application, via _https://localhost:8443/owf_ for example, you will be prompted to select the certificate from a list of those you have imported.