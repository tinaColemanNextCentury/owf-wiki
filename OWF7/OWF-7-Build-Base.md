All of the Ozone project build files use Ivy ([http://ant.apache.org/ivy](http://ant.apache.org/ivy), version 2.1.0) for their transitive dependency management as well as a set of Subversion (SVN) Ant tasks for executing release tasks. Rather than have each project contain duplicate build information pertaining to the installation and configuration of Ivy and the SVN Ant tasks, the build-base directory in the Ozone project trunk contains the build tasks and files that are common across all of the Ozone projects. Build-base doesn’t need to be checked out from SVN despite the other projects dependence on it. The Ozone Ivy SVN repository contains a zipped and versioned instance of build-base and each Ozone project treats build-base as a dependency. The first time an Ozone project is checked out from the GOSS repo, the Ant task ‘`init-build`’ needs to be run from within the project directory. This task does the following:

1. Retrieves the correct version of the **build-base.zip** file from the Ivy repo and unzips it into the project directory; This creates a sub-directory named `build-base-\<version>`.
2. Runs the ‘`init-ivy`’ task which is located in the **build-base.xml** file in the newly installed build-base directory. This task installs the correct version of Ivy as well as the necessary JAR files for the SVN Ant tasks. 
Once ‘`init-build`’ runs, the developer can run the project-specific build tasks as described below:

#1   OWF and Server Builds
If changes are being made to the server code, the developer does not normally need to run build tasks to test them. Instead, use the standard grails scripts to run or test the server code. Use the Ant build when there is the need to build a server bundle, i.e. package the **WAR** files, along with a Tomcat instance into a **ZIP** file that can then be distributed to an end user. To build a server bundle, open a Command Prompt window and ‘`cd`’ into the server’s base directory. Verify that the ‘`init-build`’ task ran, as described in the previous section:

        C:\owf-server>ant init-build

To build the bundle, type the following on the command line and press Enter:

        C:\owf-server>ant bundle

The bundle task will do a clean and build of the server code (retrieving any dependencies), run the server tests (both unit and integration) and then build the zipped bundle. The results of the build are written to the staging directory within the server directory. The staging directory of a successful build should contain the zipped bundle, as well as the unzipped contents of the bundle. The latter is provided as a convenience to test the bundle by running the start.bat (or `start.sh` on Linux systems) in the `staging/apache-tomcat-x.x.x` directory. This will start the Tomcat server which is initially configured to load the Ozone server and the CAS server **WAR** files.

##Additional Build Command Line Options
When running the build, use any (or all) of the following command line parameters:
* **-logfile build.log** – This will redirect the output of the build to the specified log file. This can be useful when there are problems with the build because the output is often too verbose to be completely captured by the Command Prompt window.
* **-Dno-test=true** – This will prevent the grails unit and integration tests from running. Often, they’ve already run. Using this option will speed up the build.
* **-Dno-jsdoc=true** – This will prevent the generation of the JavaScript documentation. Generating the documentation is time consuming and slows the build progress.
* **-Dgroovy\_all** – This property can be used to manually set the location of groovy-all.jar. This property needs to be set correctly when building to the **GROOVY_HOME** environment variable. The purpose of this property is to allow building on systems where Groovy was installed in such a way that the **GROOVY_HOME** variable is not set, such as Linux systems that installed Groovy using a centralized package manager. See below for an example: 

        ant bundle -Dgroovy_all=/usr/share/java/groovy-all.jar

##Building Offline
When building the Marketplace or OWF projects on a network that is not externally connected, try the following steps:

1. Download the Ozone Ivy repo from:  [https://owfgoss.org/svn/repos/ozone/ivy-repo](https://owfgoss.org/svn/repos/ozone/ivy-repo)
This is a very large (~2GB) download.
2. Modify `application.properties` to include the following property:
`offline\_repo=c:/path/to/ivy-repo/no-namespace`
This provides the Grails pointer to the offline repo. The value must contain the ‘`no-namespace`’ portion of the path.
3. Add a flag to the Ant command line: `-Ddisconnected=true`.
This switches the build process to use ivy properties from **build-base/ivysettings\_offline.xml**. 
4. If it is not already there, add a version of the **ivysvnresolver*.jar** to the Ant classpath. The version found in the following location can be copied and placed under the **ant/lib** directory: `ivy-repo/no-namespace/org.apache/ant-custom/zips/ant-custom-1.7.1.zip/lib`.
This provides a SvnResolver implementation for Ivy.
5. Modify file **build-base/ivysettings\_offline.xml**: if the token `${env.OFFLINE\_REPO}` exists, replace it with `${offline\_repo}`
The `ivy:settings` task has visibility to the declared Ant properties, but not the environmental properties that the parent project has within its scope.
6. [Optional] Run any grails command explicitly by adding the command line flag:  
`-DOFFLINE_REPO= c:/path/to/ivy-repo/no-namespace`.

##Troubleshooting
* Cannot connect to the OWF GOSS SVN download repository? 
    * Investigate the use of an HTTP Proxy.
    * Verify the use of a valid GOSS username and password, issued as a Contributor account. The password can be reset through the “Account Management” link on the [http://owfgoss.org](http://owfgoss.org) homepage. 
* Grails plugins used by the applications have their own dependencies. In some cases these are not required for the base application; e.g. In Alpha/Beta releases these may be experimental or partially built-out capabilities. If a plugin is causing issues,  it may be removed by:
   * Modifying the `[root]/application.properties` file and commenting out the line beginning with ‘`plugins.[pluginName]`’.
   * Moving the `[root]/plugins/[pluginName]` directory out of the project.

> _Note: Other references to the plugin may exist in places and this procedure may be insufficient to avoid all possible errors._

* Testing Grails compilation outside of the Ant script can be useful for diagnosing Grails-level configuration issues without executing all other aspects of the build process. To do this, run the following from a Command Prompt Window:

        grails compile -DOFFLINE_REPO= c:/path/to/ivy-repo/no-namespace

#2   Ozone Security Jar
If a new release of the security **JAR** file is needed, take the following steps:

1. Go to the **JAR**’s project directory ( `…\commons\ozone-security` ) and edit the **build.properties** file, incrementing the **JAR**’s version number.
2. From the project’s command line, run the following two commands:

        C:\commons\ozone-security>ant init-build -f owf-build.xml
        C:\commons\ozone-security>ant pre-release -f owf-build.xml

   Because the security project gets distributed with a project **ZIP** file, the normal ‘ **build.xml** ’ is only used to build the **JAR** file. Use the ‘ **owf-build.xml** ’ file to build new release versions of the **JAR** files. The ‘pre-release’ target does a full build of the project and then publishes the project’s artifact(s) to the local pre-release repo (`\.ivy2/local`).
3. To test the pre-release version of the **JAR**, go to the directory of the OWF or Marketplace server project and edit the server **application.properties** file to update the version number of the dependency (‘ **owf.security.rev** ’ and ‘ **mp.security.rev** ’ in the OWF and Marketplace projects, respectively).
4. Build the server bundle (Ant bundle). Go to the **staging/apache-tomcat-X.X.X/webapps/<server>.war**. Navigate the server **WAR** file and go to the **WEB-INF/libs** directory and verify that the new version of the security **JAR** is there. It is best to test the server app as well.
5. If there are problems with the new security **JAR**, make necessary modifications and repeat steps 2 through 4.
6. Once satisfied with the new **JAR**, go to the command line and run the release target.

        C:\commons\ozone-security>ant release -f owf-build.xml

> _Note: A Subversion 1.6 client must be used. Currently the JARS that Ant’s Subversion tasks use do not work with code that has been checked out with a 1.7 Subversion client. If a 1.6 client is not used, a vague exception will be thrown inside the Ant SVN tasks._

#3   CAS Server War
To make a new release of the CAS server **WAR** file, do the following:

1. Go the CAS server project directory and edit the **build.properties** file, incrementing the version number ( **cas.server.rev** ).
2. From the project’s command line, run the following two commands:

        C:\ozone\cas-server>ant init-build 
        C:\ozone\cas-server>ant pre-release

   The ‘pre-release’ target does a full build of the CAS server project and then publishes the project’s artifact(s) to the local pre-release repo ( **.ivy2/local** ).
3. To test the pre-release version of the **WAR**, go to the directory of a server project that uses this dependency (in this case **owf-server**) and edit the server **application.properties** file to update the version number of the CAS server ( **cas.server.rev** ).
4. Build the server bundle ( **ant bundle** ). Go to the `staging/apache-tomcat-X.X.X/webapps` directory. It should contain the CAS server **WAR** file. The file name should include the new CAS server version. Test the changes by running the server application.
5. If there are problems with the new **WAR**, make edits and repeat steps 2 through 4.
6. Once satisfied with the new JAR, go to the command line and run the release target:
**C:\ozone\cas-server>ant release**

#4   Tomcat-OWF-Custom
To make a new release of the **tomcat-owf-custom.zip** file:

1. Go the Tomcat server project directory and edit the **build.properties** file, incrementing the version number ( **tomcat.custom.version** ).
2. From the project’s command line, run the following two commands:

        C:\ozone\tomcat-owf-custom>ant init-build
        C:\ozone\tomcat-owf-custom>ant pre-release

   The ‘pre-release’ target does a full build of the **tomcat-owf-custom ZIP** file and then publishes it to the local pre-release repo ( **.ivy2/local** ).
3. To test the pre-release version of the **ZIP** file, go to the directory of the server project that uses this dependency (in this case **owf-server**) and edit the project’s **application.properties** file to update the version number of the CAS server ( **tomcat.custom.rev** ).
4. Build the server bundle ( **ant bundle** ). Go to the **staging/apache-tomcat-X.X.X** directory and verify that the new Tomcat changes are present.
5. If there are problems with the new Tomcat, make edits and repeat steps 2 through 4.
6. Once satisfied with the new Tomcat, go to the command line and run the release target:

        C:\ozone\tomcat-owf-custom>ant release
