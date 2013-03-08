# Allowing Remote Access to OWF

To run OWF remotely, and NOT from a localhost environment, execute the following steps:

1.	Identify a server name.
2.	Generate a server certificate.
3.	Install the server certificate.
4.	Modify configuration files.

## 1   Identify a Server Name
The server name can be chosen arbitrarily and entered into the users’ HOST files, or it can be obtained from DNS. This quick start guide will refer to the selected server name as `servername` and to OWF as **https://servername:port/owf/**.

##2   Generate a Server Certificate

The certificates that ship with OWF are configured with a domain (`servername`) of `localhost`. If the domain name is changed, new certificates are required. The server certificate must reflect the `servername`. 

Navigate to the `\etc\tools` folder and execute **create-certificates.bat** or **.sh**, depending on the operating system in use. Once this is done, the default user p12 certificates ( *testUser1* and *testAdmin1* ) will no longer be compatible. To correct this, create new user certificates using **create-certificates.bat** (or **.sh**). 

Follow the prompts on screen and create the necessary certificates for the installation.

##3   Install the Server Certificate

The OWF start script, located at **apache-tomcat-7.0.21\bin\setenv.bat** ( **apache-tomcat-7.0.21\bin\setenv.sh** on \*nix systems ) must be edited to point to the new keystore (defined while answering the prompts discussed in section **2 Generate a Server Certificate**) file found in **setenv.bat/setenv.sh**. Edit the `servername` domain (found in lines 1 and 2 in the code below) to reflect the certificate.

        1 set CATALINA_OPTS=-Djavax.net.ssl.trustStore="%CATALINA_HOME%\certs\servername.jks" -
        2 Djavax.net.ssl.keyStore="%CATALINA_HOME%\certs\servername.jks" -
        3 Djavax.net.ssl.keyStorePassword=changeit -Djavax.net.ssl.trustStorePassword=changeit server -
        4 Xmx1024m -Xms512m -XX:PermSize=128m -XX:MaxPermSize=256m %JAVA_OPTS% 

The Tomcat configuration file, located at **apache-tomcat-7.0.21\conf\server.xml**, must also be edited to point to the new Keystore file. This section can be found below the “Define a SSL…” section of the XML file:

```xml
          <Connector port="8443" protocol="HTTP/1.1" SSLEnabled="true"
                        maxThreads="150" scheme="https" secure="true"
                        keystoreFile="certs/servername.jks" keystorePass="changeit"	       
         	truststoreFile="certs/servername.jks" truststorePass="changeit"
                       clientAuth="want" sslProtocol="TLS" /> 
```

## 4   Modify the Externalized Configuration Files

In order to access OWF from remote computers, externalized configuration files must point to the correct location. This is done by changing a properties file that is referenced by the following two configuration files: 

*	**apache-tomcat-7.0.21\lib\OwfConfig.groovy** 
*	**etc\override\CASSpringOverrideConfig.xml**
 
By default, the configuration files allow access from localhost but not from other locations. To access other locations:

1.	Copy **CASSpringOverrideConfig.xml** from the `etc\override` to `apache-tomcat-7.0.21\lib`. By default, **OwfConfig.groovy** is located on the classpath. Therefore, it does not need to be moved. 
2.	In the **apache-tomcat-7.0.21\lib\OzoneConfig.properties** file, replace `localhost` with `servername` for the `ozone.host` property.
3.	Restart the server. 