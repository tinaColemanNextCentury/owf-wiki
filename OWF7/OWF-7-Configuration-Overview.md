This is an overview of the OWF Configuration Guide. 
#1 Overview
###Purpose
OWF is a set of tools, generally delivered in **OWF-bundle-7-GA.zip**. When deployed, OWF is used for organizing and displaying Web applications (widgets) in a browser window.

### Basic Architecture
OWF consists of a number of components that are designed to be independently deployed. The simplest deployment scenario places them all on the same physical machine. 

### Dependencies
The OWF Bundle is shipped with Tomcat 7.0.21 which requires JDK 1.6 or higher. If running OWF with a Web server other than Tomcat, see that Web server's documentation for requirements. 

#2 Components
## Ozone Widget Framework (OWF) Web Application
**owf.war** – This file contains the components which make up OWF. Whether a user logs in and accesses the framework, or an administrator logs in to modify preferences, the **owf.war** is the application that launches those pages to the browser.

## CAS Web Application
**cas.war** – This optional file is responsible for providing the Central Authentication Service (CAS). OWF ships with a customized version of CAS. 

> _Note: Jasig CAS is an independent project and is not directly related to OWF outside of security protocols. It is included as a convenience._

## Pluggable Security

OWF allows an administrator to customize the type of security that will be implemented for user authentication and authorization. Included within OWF’s `/owf-security` directory are XML files that provide examples of optional security configurations. **They are intended as examples and should in no way be used in a production environment.** However, they can be used as the basis for updating **\owf-security\ozone-security-beans\OWFCasBeans.xml** and **\owf-security\ozone-security-beans\OWFLogInOutBeans.xml** (home of common configuration information and bean definitions that are used by multiple plugins) to function in a production environment.
Along with the security-related XML files, there is also a ZIP file which contains the source and configuration files for the pluggable security modules. Additionally, an Apache ANT build script is included. The build script allows for a rebuild of the OWF security JAR file for customization. Also, **owf-security\owf-security-project\src\main\resources\conf\sample-log4j.xml** contains a subset of the **OWF-log4j.xml** file (found in the `apache-tomcat-7.0.21\webapps\owf\WEB-INF\classes` directory) that pertains to security settings. It demonstrates how to enable logging for OWF Security.

> _Note: In all of the pluggable security instances, user authorization can be configured to the default of an externalized text file._

> _Note: Refer to the [OWF Security Page](OWF-7-Configuring-OWF-Security) for more details about OWF Security._
  
### Default Authentication

**OWFsecurityContext.xml** - This contains the default security implementation for OWF. It uses a PKI certificate for authentication. If no authentication is provided, it redirects the user to sign in using CAS as a fallback. 

###X509-Only Security

**OWFsecurityContext_cert_only.xml** - This contains the X509-only security implementation for OWF. It uses a PKI certificate for authentication. If no authentication is provided, the user is denied access to the system. 

###CAS-Only Security
**OWFsecurityContext_CAS_only.xml** - This contains the CAS-only security implementation for OWF. If the sign-in is invalid, the user will be denied access to the system. 

###X509/LDAP

**OWFsecurityContext_cert_ldap.xml** - This contains an X509/LDAP security implementation that uses X509 for authentication and then performs an LDAP-based lookup to determine the user’s authorization.

###Basic Spring Login

**OWFsecurityContext_BasicSpringLogin.xml** - This contains a basic Spring security sign-in implementation that uses names populated in the XML file to determine the user’s access.

###OWF Security Project

**owf-security-project.zip** - This bundle contains the source code, configuration files and library files needed to build the security files which are used by OWF. Additionally, an Apache ANT build script is included for the building of the JAR file which is used by the following security XML files.

The **owf-security-project.zip** contains the following supporting resource files:

* **src/main/resources/conf/apache-ds-server.xml**, a sample XML file used by Apache Directory Server (ApacheDS, an open-source LDAP v3 compliant embeddable directory server) that sets up the initial directory service partitions for the test data.
* **src/main/resources/conf/testUsers.ldif**, an LDAP Data Interchange Format test file that can be imported to set up test entries that match the certificates bundled with OWF.
* **lib/spring-security-ldap-3.0.2.RELEASE.jar**, a file which provides LDAP functionality used by the Ozone-LDAP-Security plugin. 

> _Note: While the same PKI files used in the sections **Default Authentication** and **X509-Only Security** are used for the authentication of users, the LDAP files in the section **X509/LDAP** are used for their authorization._

##Sample Widgets

OWF provides sample widgets in the **owf-sample-widgets.zip** file and the `owf\examples` directory located inside the unpacked **owf.war**.

The samples employ various Web technologies. They can be used as a starting point for investigating different widget implementation strategies. The follow table references a few specific examples that demonstrate how to invoke or integrate JavaScript with different technologies. Additional example widgets are included in the `examples` directory in **owf.war**. Also, the OWF Developer’s Guide includes specific examples and walkthroughs regarding the widget APIs. 

<b>Table: Example Widgets </b>

<table style="text-align: left; width: 100%;"
 border="1" cellpadding="5" cellspacing="0">
  <tbody>
    <tr>
      <th>Widget</th>
      <th>Web Technology</th>
      <th>Description</th>
      <th>Widget Location</th>
    </tr>
    <tr>
      <td>DotNet</td>
      <td>NET</td>
      <td>A Web page for adding eventing channels and a Web service for storing received messages.</td>
      <td>owf-sample-widget.zip</td>
    </tr>
    <tr>
      <td>Flex Pan</td>
      <td>Flex</td>
      <td>Displays a large image of the Earth and allows users to zoom and scroll around the image.</td>
      <td>owf-sample-widget.zip</td>
    </tr>
    <tr>
      <td>Flex Direct</td>
      <td>Flex</td>
      <td>Connects to the Flex Pan widget via the eventing mechanism to control the panning and zooming; also displays the current mouse position.</td>
      <td>owf-sample-widget.zip</td>
    </tr>
    <tr>
      <td>Channel Shouter Flex</td>
      <td>Flex</td>
      <td>Demonstrates eventing and widget launcher APIs created in Flex.</td>
      <td>owf-sample-widget.zip</td>
    </tr>
    <tr>
      <td>Channel Listener Flex</td>
      <td>Flex</td>
      <td>Demonstrates eventing and widget launcher APIs created in Flex.</td>
      <td>owf-sample-widget.zip</td>
    </tr>
    <tr>
      <td>OWF Silverlight Demo</td>
      <td>Silverlight</td>
      <td>Allows a user to send messages to other widgets in the framework, register channels to listen on, and track the frequency of the messages within the registered channels on either a pie chart or a bar chart.</td>
      <td>owf-sample-widget.zip</td>
    </tr>
    <tr>
      <td>My Chess Viewer</td>
      <td>Java Applet</td>
      <td>Reads and animates a chess PGN file, incorporates it into the framework, broadcasts each forward move selected on a channel named “mychess”, and stores the current position in the game to the Preference Service.</td>
      <td>owf-sample-widget.zip</td>
    </tr>
    <tr>
      <td>Announcing Clock</td>
      <td>HTML</td>
      <td>A clock that broadcasts to an HTML page; optionally displays military time.</td>
      <td>owf-sample-widget.zip</td>
    </tr>
    <tr>
      <td>Stockwatcher</td>
      <td>GWT</td>
      <td>Broadcasts a message on the “stockwatcher” channel when stocks are added or removed; saves stock symbol picks to the Preference Service.</td>
      <td>owf-sample-widget.zip</td>
    </tr>
    <tr>
      <td>NYSE Widget</td>
      <td>GSP</td>
      <td>Part of the widget intents example, this widget sends “view” and “graph” intents to receiving widgets. </td>
      <td>owf.war</td>
    </tr>
    <tr>
      <td>Stock Chart</td>
      <td>GSP</td>
      <td>Part of the widget intents example, this widget receives data from graph intents.</td>
      <td>owf.war</td>
    </tr>
    <tr>
      <td>HTML Viewer</td>
      <td>GSP</td>
      <td>Part of the widget intents example, this widget receives data from view intents.</td>
      <td>owf.war</td>
    </tr>
  </tbody>
</table>