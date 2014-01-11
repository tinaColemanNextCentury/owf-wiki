# OWF Security
OWF allows an administrator to customize the type of security that is implemented for authentication and authorization. OWF uses a pluggable Spring Security 3.0.2 solution and ships with sample security plugins that can be used as a basis for building a custom security plugin. Familiarity with Spring Security will help administrators customize OWF.

#1 Basic Security Concepts and OWF
While this guide is not intended as a comprehensive guide to basic security concepts, Web security or Spring Security, there are a few key concepts that must be understood in order to use the sample OWF security plugins and the OWF security plugin architecture. 

First are the concepts of authentication and authorization, known colloquially as auth & auth. Authentication essentially means providing proof that the user is exactly who they are presenting themselves to be. Some authentication techniques include a username/password combination, an X509 certificate, a CAC card and card reader, or various biometric solutions. Authorization, on the other hand, is determining the specific access rights that an individual user should have. Consider the following:

* “Bill is allowed to log into the system – prove that you are Bill,” is a matter of authentication.
* “Bill has access to resources,” is a question of authorization.

By necessity, authentication occurs before authorization. Once authentication is satisfied, OWF moves to authorize. OWF has two authorization concepts at this time. First, OWF needs to know whether or not a user has OWF administrative access via `ROLE_ADMIN` or is only a regular user, via `ROLE_USER`. Administrative access provides a user access to the administrative widgets and the administrative console. Regular users have access only to the framework and their assigned dashboards. 

Second, OWF needs to know what external OWF user groups (if any) the user has been assigned. There are two kinds of user groups; automatic user groups, which are pulled in from an external authorization source, such as LDAP or a configuration file, and manual user groups, which are set up from within OWF. If an automatic user group is new to OWF, all of the automatic user groups’ details such as description, active/inactive status, contact email address, and name come from the external source. But after the initial creation of the group in OWF, no further updates to the description, status, etc. are made. 

#2 Requirements for Customizing Security

The Spring Security Framework allows individual deployments to customize the OWF backend. Developers can use the OWF security plugin to integrate with any available enterprise security solutions. When customizing the security plugin, it is important to remember OWF’s requirements for the plugin. Those five requirements are described in this section. 

> _Note: The OWF requirements are in addition to any general  Web application requirements relating to Spring Security._

1.	User principal implementing the `OWFUserDetails` interface
The security plugin must create an object which represents the signed-in user and implements the `OWFUserDetails` interface. To do this, set the object as the principal on the `Authentication` object stored within the active `SecurityContext`. 
In addition to the fields that can be set on a normal Spring `UserDetails` object, the `OWFUserDetails` interface supports access to the user’s OWF groups, display name, Organization, and Email. Including values for these fields is optional.
2.	OWF Groups accessible via `principal.getOwfGroups()`
OWF supports the ability to manage OWF groups via the security plugin. In order to use this feature, the `getOwfGroups()` method on the user principal must return a collection which includes an object implementing the `OwfGroup` interface for each group to which the user belongs. Any groups that OWF detects will be added to the OWF database as “Automatic” groups.
3.	`ROLE_USER` granted to all users
The user principal object’s `getAuthorities()` method must return a collection that includes the `ROLE_USER` GrantedAuthority. 
4.	`ROLE_ADMIN` granted to OWF administrators
The user principal object’s getAuthorities() method must return a collection that includes the `ROLE_ADMIN` GrantedAuthority if the user is to have administrative access to OWF.
5.	`OZONELOGIN` cookie set upon sign in and deleted on sign out
The OWF user interface performs a check for the existence of a cookie named `OZONELOGIN` during the page load. If the cookie does not exist, the interface will not load, but will instead present a message indicating that the user is not signed in. It is up to the security plugin to create this cookie when the user signs in, and to delete it when they sign out. 
This mechanism prevents users from signing out, and then pressing the browser’s Back button to get back into an OWF instance that cannot communicate with the server due to failed authentication. The sample security plug-in configurations shipped with OWF contain filters that manage this process. It is recommended that custom configurations include this default implementation of the cookie behavior by using the same ozoneCookieFilter and `OzoneLogoutCookieHandler` beans that are included in the sample configuration, in **OWFsecurityContext.xml** and **OWFLogInOutBeans.xml**.

#3   Custom Security Logout
The OWF sample security plugins can perform single sign out if the user signed in using CAS authentication. PKI authentication is handled by the browser and requires that the user close the browser to completely sign out, though their session with the application can be reset. To sign out from LDAP or a custom authentication, the system administrator must implement their own single sign out or instruct the user to close the browser after signout. Use the following lines in the OWF Security Context file to invoke CAS’s single sign out process. 

    <sec:custom-filter ref="casSingleSignOutFilter" after="LOGOUT_FILTER"/>

      <!—OWFCasBeans.xml contains the casSingleSignOutFilter bean definition -->
    <import resource="ozone-security-beans/OWFCasBeans.xml" />

#4   Production Deployments
The samples included with OWF are not production quality samples. They are intended to provide examples on how to easily integrate various security solutions with OWF, not to provide a comprehensive security solution out of the box or a comprehensive tutorial on Spring Security. It is expected that each organization using OWF will examine its security guidelines and enterprise-wide authentication/authorization solutions and produce an OWF security plugin that is both secure and meets its standards. That solution can then be shared among OWF deployments within the organization. 
Most of the examples provided contain various obvious security hazards—for example, the CAS-only, X509-only, and CAS + X509 plugins all contain a list of usernames, roles, and user groups on the hard drive in plain text in a properties file. <b>The CAS-only and CAS+X509 files contain the passwords in plain text. These are undeniable security hazards.</b> Keep this in mind when using the samples.

#5 Sample Plug-in Summary
OWF ships with four simple sample plugins:

##Default Authentication: CAS + X509
**OWFsecurityContext.xml** – This contains the default security implementation for OWF. It uses a PKI Certificate for authentication. If no certificate is provided, it redirects the user to sign in using CAS as a fallback. CAS stores valid usernames and passwords in a users.properties file on the server. Once the user has been authenticated, the authorization information (role and OWF user groups) is provided in the same properties file, `users.properties`.

##Basic Login + LDAP
**OWFsecurityContext_basic_ldap.xml** – Added in OWF 5, this security plugin demonstrates how to use an external LDAP database for user-authorization in conjunction with a simple username/password- request page for authentication.  If the username isn’t in the LDAP database, or the password is incorrect, the user will be denied access to OWF.

##X509 Only Security
**OWFsecurityContext_cert_only.xml** – This contains the X509-only security implementation for OWF. It uses a PKI certificate for authentication. If no certificate is provided, the user is denied access to system. Authorization, the users' roles (admin and user) and OWF user groups, are stored in `users.properties`. 

##CAS Only Security
**OWFsecurityContext_CAS_only.xml** – This contains the CAS-only security implementation for OWF. It eliminates certificate-based authentication. If the sign-in is invalid, the user will be denied access to the system. 

To use this authentication method, replace the active security-based XML files, (for example, **\apache-tomcat-7.0.21\lib\OWFsecurityContext.xml**) with the **\owf-security\OWFsecurityContext_CAS_only.xml** file.
The container in use may need to be adjusted to eliminate the prompt for a certificate. For example, the bundle’s Tomcat instance is set up to ask for certificate authentication, but not require it. To eliminate the certificate prompt, edit the **\apache-tomcat-7.0.21\conf\server.xml** file and change the `clientAuth` property to false:

    <Connector port="8443" protocol="HTTP/1.1" SSLEnabled="true"
       maxThreads="150" scheme="https" secure="true"
       keystoreFile="certs/keystore.jks" keystorePass="changeit"	       
       clientAuth="false" sslProtocol="TLS" 
    />

CAS stores valid usernames and passwords in a users.properties file on the server. Once the user has been authenticated, the authorization information (Role and OWF User Groups) is provided in the same properties file, `users.properties`.

###Customizing CAS
`OzoneConfig.properties` proxies some of the CAS properties that can be customized by specific organizations. To change where the default CAS server, CAS sign-in and CAS sign-out point, update the corresponding values in `OzoneConfig.properties`. For additional CAS instructions, see [CAS Documentation](http://globus.org/toolkit/docs/3.2/cas/). 

###CAS Modifications for use with Marketplace
Ozone Widget Framework (OWF) and Marketplace use some files that have the same name but different properties. `OzoneConfig.properties` is one of those files. If the local instance of OWF is deployed in the same application server as an instance of Marketplace, the server can only use one `OzoneConfig.properties` file. The file that is used must include CAS properties for both OWF and Marketplace. 

To update `OzoneConfig.properties` using the OWF version of the file:

1.	From the `apache-tomcat-7.0.21\lib` folders in Marketplace and OWF, open the `OzoneConfig.properties` file in both products.
2.	From the Marketplace `OzoneConfig.properties` file, copy:

        ozone.cas.marketplace.serverSecureReceptorLocation=marketplace/secure/receptor
        ozone.cas.marketplace.jSpringCasSecurityCheckLocation=marketplace/j_spring_cas_security_check
3.	Paste the two lines of code into the OWF `OzoneConfig.properties` file.
4.	Copy the updated OWF `OzoneConfig.properties` file onto the classpath of the server that is hosting both applications. Then, restart the server. 

##X509 with LDAP 
**OWFsecurityContext_cert_ldap.xml** – This contains an X509/LDAP security implementation that uses X509 for authentication and then performs an LDAP-based lookup to determine the user’s authorization. Authorization includes the user’s role (`ROLE_ADMIN` or `ROLE_USER`) and the user’s groups. 
The `owf-security` project directory contains the following supporting resource files:

* **conf/apache-ds-server.xml**, a sample XML file used by Apache Directory Server (ApacheDS, an open-source LDAP v3 compliant embeddable directory server) that sets up the initial directory service partitions with the test data. 
* **conf/testUsers.ldif**, an LDAP Data Interchange Format test file that can be imported to set up test entries that match the certificates bundled with OWF. This test data includes `testUser1` and `testAdmin1`, roles `ROLE_USER` and `ROLE_ADMIN`, and two example groups, `group1` and `group2`. It is designed to work with the sample user PKI Certificates that ship with OWF. 

##Basic Spring Login
**OWFsecurityContext_BasicSpringLogin.xml** – An example of a very simple security plugin configuration using a form-based sign-in page and inline user information. 

#6   Installing the Security Module
The OWF-security files offer multiple examples of security options. These are intended as examples and should in no way be used in a production environment. As mentioned previously, the default security implementation provides an X509 certificate authentication with CAS fallback. When using the default security module in a testing environment, the user must present a valid X509 certificate, or a valid CAS sign-in, in order to gain access to OWF.

For each available security option, there is a specific XML file which must be installed. Installing a new security module is accomplished in just a few simple steps: 

> _Note: The following instructions act as a summary for installing individual security modules. Depending on the module being used or tested, module-specific instructions may be needed. See **owf-security\owf-security-project.zip\readme.txt** for the installation details specific to each module type. Additionally the summary instructions below assume that the default installation is being used with Tomcat as the app server/container._

1.	Stop the application server. An administrator can accomplish this by clicking the
 `\apache-tomcat-7.0.21\bin\shutdown.bat` or `\shutdown.sh` file, depending on the operating system in use.
2.	Delete any security-based XML (**OWFsecurityContext*.xml**) files that might currently be present in the `\apache-tomcat-7.0.21\lib` directory.
3.	Remove CAS from the OWF instance if switching to a security plugin that does not use CAS. 
4.	Copy the appropriate XML file from `\owf-security` to the application server’s class path. When running Tomcat, the classpath is the `\apache-tomcat-7.0.21\lib` directory.
5.	Restart the application server by clicking either `\apache-tomcat-7.0.21\start.bat` or `\start.sh` file, depending on the operating system in use.<br>

  > *Note: The following instructions describe how to remove CAS from the OWF instance. This should only be done if switching to the X509 sample, the X509+LDAP sample, or a custom plugin that does not require CAS.* 

6.	Remove **CASSpringOverridesConfig.xml** from `\apache-tomcat-7.0.21\lib` if it was deployed there. 
7.	Delete the CAS deployment: Delete **cas.war** from `\apache-tomcat-7.0.21\webapps`.

##X509-Only Specific Instructions
The **OWFsecurityContext_cert_only.xml** file eliminates CAS as a fallback to authentication. If the user does not present a valid X509 certificate, they will be denied access to the system. Authorization is provided by the `users.properties` file. The format of this file is described in 4.1.1: Adding Users/Roles/Groups.
To use this security plugin, replace the active security-based XML file (e.g., **\apache-tomcat-7.0.21\lib\OWFsecurityContext.xml**) with the **OWFsecurityContext_cert_only.xml** file, which can be found in the `\owf-security` directory. Follow the directions to stop and restart OWF and follow the directions above, to remove CAS. 

##CAS-Only Specific Instructions
To use just the CAS server without any X509 certificate authentication, replace the provided **OWFsecurityContext.xml** file with **OWFsecurityContext_CAS_only.xml**, and follow the steps in the **Installing the Security Module** section to stop and restart the server. When using the CAS only security implementation, if the user fails authentication to the CAS, they will be denied access to the system.

When using the CAS only security implementation, the servlet in use may need to be adjusted to eliminate the prompt for a certificate. For example, the bundle’s Tomcat instance is set up to ask for certificate authentication, but not require it. To eliminate the certificate prompt, edit the `\apache-tomcat-7.0.21\conf` file and change `clientAuth` property to false:

    <Connector port="8443"
        protocol="HTTP/1.1"
        SSLEnabled="true"
        maxThreads="150"
        scheme="https"
        secure="true"
        keystoreFile="certs/keystore.jks" 
        keystorePass="changeit"
        clientAuth="false"
        sslProtocol="TLS" />

##X509/LDAP
The **OWFsecurityContext_cert_ldap.xml** file provides X509 client authentication with an LDAP-based lookup to determine the user’s authorization. The default configuration attempts to connect to a local installation of Apache Directory Server on port 10389, using the default system account. It determines the user’s authorization by searching on the full distinguished name presented in the X509 certificate.

Sample configuration files are provided to set up an Apache Directory Server with user information that matches the X509 certificates provided with OWF, including a server configuration **.xml** file and an LDAP Data Interchange Format file (*.ldif) which loads users to match the distinguished names in the certificates. For more information about LDAP, refer to [http://directory.apache.org/](http://directory.apache.org/). 

Included is a sample Apache DS **server.xml** file, called **\owf-security\owf-security-project\src\main\resources\conf\apache-ds-server.xml**. It adds the partition owf-1 to Apache DS. To do so, it adds the following line of XML to the XPATH `spring:beans/defaultDirectoryService/partitions`:

    <jdbmPartition id="owf-1" suffix="o=Ozone,l=Columbia,st=Maryland,c=US" /> 

It is also necessary to load the sample data into the directory service. The OWF team has provided a sample LDIF file, called `\owf-security\owf-security-project\src\main\resources\conf\testUsers.ldif`.
 
> *Note: Downloading the Apache Directory Studio may be helpful.*

It is straightforward to modify how the LDAP search is conducted for both user roles and user groups. No adjustment is required in order to run the plugin with the default data. However, to modify the plugin to run off of a different data set, adjust **ozone-security-beans\LdapBeans.xml**. It is recommended that the administrator get the plugin working off of the default data set before trying to migrate to a different data set by modifying the LDAP queries. 

To use the X509(cert)/LDAP security implementation, replace the provided **owf-security.xml** file with **OWFsecurityContext_cert_ldap.xml**, and follow the directions in the **Installing the Security Module** section to stop and restart the server and to remove CAS. 

#7   Custom Security and Sample Source Code
Along with the security-related XML files, there is also a ZIP file which contains the source and configuration files for the pluggable security modules. Additionally an Apache ANT build script is included. The build script allows for a quick and simple rebuild of the security project (JAR) files for greater customization, if needed. 

There are two packages in the security project. The first package is `ozone.securitysample`. This package contains the code required for the security sample projects. This code is probably not extremely reusable, or reusable only with modifications. 

The second package is called `ozone.security`. This package is very important, and is required by OWF to run. 

The most important classes are defined in the following sections. 

#8   OWFUserDetails
`Package:ozone.security.authentication`

This interface defines interactions for a data model that OWF requires in order to handle OWF user groups. Using an implementation of this interface (and implementations may vary) will ensure that OWF user groups work. 
This interface extends the classic `UserDetails` interface as defined by Spring Security 3.0. Please refer to the Spring Security UserDetails API to read about the interface `UserDetails`. In order to understand how `UserDetails` works in the Spring Security 3 program flow, refer to the Spring Security 3 guide. 

    public interface OWFUserDetails extends UserDetails{
	    /**
	     * getOwfGroups
	     * @return a Collection containing information about the OWF Groups that this user is a part of.
	     */
	    public Collection<OwfGroup> getOwfGroups();
	    /**
	     * getDisplayName
	     * @return String the Display Name of the user. This name is displayed in the upper right hand corner of the banner. If not set, the username is used instead. It is an optional field.
	     */
	    public String getDisplayName();
    }

##OWFUserDetailsImpl 
    ozone.security.authentication

This is a sample implementation of the `OWFUserDetails` interface. It is not mandatory to use this implementation, it is only a sample. 

> *Note: If a custom implementation is written, authorities must be write-accessible; create a setAuthorities method.*

##OWFUserDetailsImpl
    ozone.security.authorization.target

This interface describes a single OWF user group. A group is a way of collecting OWF users and being able to assign widgets and other behaviors to them collectively. Consider this class to be similar to the Spring Security class `GrantedAuthorities:
package ozone.security.authorization.target`;

    /** 
         * WidgetGroup
         * 
         *
         * This interface describes a single OWF user group. A group is a way of collecting
         * OWF users and being able to assign widgets and other behaviors to them collectively. 
         * 
         * A group has one attribute, a name that should not change. The other attributes are optional.
         * 
         * Consider this similar to GrantedAuthorities. 
         *
         */
        public interface OwfGroup {
        	/**
	         * 
	         * @return the name of the Owf Group
	         */
        	public String getOwfGroupName();
               /**
	         *
	         * @return a drescription of the OWF group
	         */
	        public String getOwfGroupDescription();
                /**
	         *
	         * @return an email address that will reach someone if there are problems with the group.
	         * This is displayed to a group administrator in OWF
	         */
	        public String getOwfGroupEmail();
	        /**
	         * @return true if this is an active group
	         */
	        public boolean isActive();
        }

##OwfGroupImpl
    ozone.security.authorization.model

This class implements an `OwfUserGroup`. It can be used as-is in a security implementation, or one can be created as-needed. 

##GrantedAuthorityImpl
    ozone.security.authorization.model

This class implements the Spring Security 3.0 interface `GrantedAuthority`. It can be used as-is in a security implementation, or one can be created as-needed. 
