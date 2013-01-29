# Running OWF in JBoss

## Introduction
This document describes how to run OWF 7 in JBoss 5. It is intended to serve as an example of hosting OWF in a Java Servlet container other than the default, Apache Tomcat. The steps that follow will configure OWF to use x509 certificate authentication only. Consult JBoss documentation for information on performance tuning and security lock-down.

## Requirements
1. You must have a properly built OWF 7 distribution. For the purpose of this document _**[owfBundle]**_ refers to the _**staging**_ directory in your OWF source tree.

2. Download the Jboss 5.1 application server package (jboss-5.1.0.GA.zip). Unzip the contents to your desired installation location. The root directory of your unzipped JBoss package will be referred to as _**[jBossHome]**_ below.

## Creating an OWF Configuration in JBoss
1. Copy the contents of the _**[jBossHome]/server/default**_ directory to a new directory. It can have any name, but we will call it _**owf7**_ for the purpose of this guide.

    > NOTE: JBoss configurations other than _**default**_ should work fine as a template for OWF, although not every one has been tested. Please report any issues encountered on the Google group.

2. Copy the _**[owfBundle]/apache-tomcat-7.0.21/certs directory**_ to _**[jBossHome]/server/owf7/conf**_, such that you now have a _**[jBossHome]/server/owf7/conf/certs**_ directory containing the application default x509 certificates.

3. Copy the _**[owfBundle]/apache-tomcat-7.0.21/prodDb.script**_ file to the _**[jBossHome]/bin**_ directory. Said file defines the in-memory HSQL Database used for OWF development. It must be located in the directory where the JBoss server will be executed.

4. Copy the following files and directories from the _**[owfBundle]/apache-tomcat-7.0.21/lib**_ directory to the _**[jBossHome]/server/owf7/conf**_ directory:

        OwfConfig.groovy
        OzoneConfig.properties
        users.properties
        help/
        js-plugins/
        ozone-security-beans/
        themes/

5. Copy the _**[owfBundle]/owf-security/OWFsecurityContext_cert_only.xml**_ file to the _**[jBossHome]/server/owf7/conf**_ directory. Said file configures OWF to use certificate only authentication. Note that you must delete the default _**OWFsecurityContext.xml**_ file from the _**conf**_ directory if you copied it there in the previous step. Said file uses the CAS login package which does not work with JBoss.

6. Copy the _**[owfBundle]/apache-tomcat-7.0.21/webapps/owf.war**_ file to the _**[jBossHome]/server/owf7/deploy**_ directory. Said file contains the OWF web application.

7. Add the following connector entry to your _**[jBossHome]/server/owf7/deploy/jbossweb.sar/server.xml**_ file:

        <Connector
         protocol="HTTP/1.1"
         SSLEnabled="true"
         port="8443"
         address="${jboss.bind.address}"
         scheme="https"
         secure="true"
         clientAuth="want"
         keystoreFile="${jboss.server.home.dir}/conf/certs/keystore.jks"
         keystorePass="changeit"
         truststoreFile="${jboss.server.home.dir}/conf/certs/keystore.jks"
         truststorePass="changeit"
         sslProtocol = "TLS" />

    The connector defined above enables HTTPS and uses our application certificates.

## Removing Conflicting Libraries from OWF
1. Use either the Java Jar tool or a Zip utility to unzip the _**owf.war**_ in the _**deploy**_ directory such that you now have a _**[jBossHome]/server/owf7/deploy/owf**_ directory containing the OWF web application files. Said directory will be referred to as _**[appInstall]**_.

2. Delete the original _**owf.war**_ file from the _**deploy**_ directory.

3. Delete the _**[appInstall]/WEB-INF/lib/jta-1.1.jar**_ file.

4. Re-package the OWF application using one of the following methods.:

   a) Rename the _**[appInstall]**_ directory as _**owf.war**_.

   b) Re-package the directory as a proper WAR file using the Jar tool and then remove the _**[appInstall]**_ directory:

           jar -cvf owf.war *

   In either case JBoss must find something named _**owf.war**_ that it will then deploy as a web application.

## Running JBoss
Launch JBoss using the _**owf7**_ configuration we defined above. Open a command prompt and go the the _**[jBossHome]/bin**_ directory. Then execute:

        run -c owf7

## Client Browser Configuration
Since we have configured OWF to use certificate only authentication above we must import the appropriate certificates into each web browser that will access OWF.

1. Open your web browser's certificate manager.

    > In Firefox:
    > * Open the _Preferences_ menu and go the _Advanced_ settings.
    > * Click the _View Certificates_ button in the _Encryption_ tab.

2. Import either the _**testUser1.p12**_ or _**testAdmin1.p12**_ certificate file. Said files must be unlocked using "password" (no quotes) as the password. The noted example certificates are located under the _**[owfBundle]/apache-tomcat-7.0.21/certs**_ directory.

3. When you access the OWF web application, via _https://localhost:8443/owf_ for example, you will be prompted to select the certificate from a list of those you have imported.