#Deploying OWF to an Existing Tomcat Instance

The OWF development team uses Tomcat 7.0.21 for all internal testing. The following instructions explain how to deploy a new instance of OWF to an already established Tomcat instance. For the purposes of documentation, we have named the tomcat instances “production” and “temporary.” 

1.	Unzip the OWF bundle into a directory called `/owf-temp`. Some of the files from this bundle will be used in the Tomcat installation named production. 
2.	Copy `/owf-temp/apache-tomcat-7.0.21/bin/setenv.bat` into the corresponding folder in the production Tomcat installation.
3.	Copy `/owf-temp/apache-tomcat-7.0.21/webapps/owf.war` to the production Tomcat webapps directory. 
4.	If the security bundle requires CAS, copy `/owf-bundle/apache-tomcat-7.0.21/webapps/cas.war` to the production Tomcat webapps directory.
5.	To use the sample key store and client certificate in a local development or test environment, copy the `/owf-temp/apache-tomcat-7.0.21/certs` directory to the production Tomcat `certs` directory (This may need to be created.).  
6.	Modify the production Tomcat file with the following configurations. Ensure that the file contains the <b>“Connector”</b> configuration (In the example below, port 8443 has been used.): 

        <Connector port="8443" protocol="HTTP/1.1" SSLEnabled="true"
               maxThreads="150" scheme="https" secure="true"
               keystoreFile="certs/keystore.jks" keystorePass="changeit"	       
               clientAuth="want" sslProtocol="TLS" />
 The default security module uses the user’s client certificate for authentication if it is available. The default security will revert to CAS if the certificate is missing or invalid. 

 To use the default security module (PKI only security) OR a custom security module with a user’s client certificate for authorization, set the clientAuth to `want` or `true`. True requires a client certificate like the PKI only security module. It should only be used if a fallback authentication scheme such as CAS is unnecessary.

 Set the key store and trust store parameters to the values that are appropriate for the production environment. The example above is using the default key store shipped with OWF. It is <b>only</b> appropriate for local development and testing environments.
7. Start production Tomcat which allows it to unpack the WAR files.
8.	Stop Tomcat.
9.	Copy the following from the temporary `apache-tomcat-7.0.21/lib` directory in the distribution bundle to the production Tomcat `webapps/owf/WEB-INF/classes` directory:
  * `OwfConfig.groovy`
  * `OwfSecurityContext.xml`
  * `Owf-override-log4j.xml`
  * `OzoneConfig.properties`
  * `Ozone-security-beans directory`
10.	To deploy CAS, copy `/owf-temp/etc/override/CASSpringOverrideConfig.xml` to the production `Tomcat webapps/cas/WEB-INF/classes` directory.
11.	If the sample security modules are in use, copy `/owf-temp/apache-tomcat-7.0.21/lib/users.properties` to the production `/lib` directory. 
12.	Copy the themes, help, and js-plugins directories from temporary `apache-tomcat-7.0.21/lib` folder to the production `apache-tomcat-7.0.21/lib` folder.
13.	Start Tomcat.