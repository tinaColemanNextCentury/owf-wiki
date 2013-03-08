#OWF Build Instructions 
#OWF6 and 7 - Grails, Ext JS infrastructure

## 1 Objectives
The purpose of this document is to describe how to build the following project:

* **OWF Server** – A local copy of the bundled (owf-server.war + cas-server.war + owf-samples + Tomcat) ZIP file as well as the release version.


## 2 Requirements
This document is targeted to OWF server/container developers and assumes a basic familiarity with the target development environment, be it Microsoft Windows or Linux. Before any of the build tasks can run, the developer must install Ant, Ant Contrib 1.0b3 and Grails 1.3.7. The following sections list the tools, the version requirements for recent OWF releases and nominal configuration elements. Instructions provided below assume a Microsoft Windows development environment for illustrative purposes only. 

### Download and Install Applications
OWF Development requires the use of the Java Development Kit (JDK), Apache Ant, Apache Ant Contrib, Ruby, RubyGems, Sass and Compass, as well as Groovy. The following table lists the versions of each tool required by OWF releases.

**Table: OWF Development Tools and Version Numbers**

<table>
 <tr>
    <th>Application</th>
    <th> OWF 6 </th>
    <th> OWF 7 </th> 
 </tr>
 <tr>
   <td>JDK</td>
   <td>1.6</td>
   <td>1.6</td>
 </tr>
 <tr>
   <td>ANT</td>
   <td>1.8</td>
   <td>1.8.3</td>
 </tr>
 <tr>
   <td>Ant Contrib</td>
   <td>1.0b3</td>
   <td>1.0b3</td>
 </tr>
 <tr>
   <td>GRAILS</td>
   <td>1.3.7</td>
   <td>1.3.7</td>
 </tr>
 <tr>
   <td>RUBY</td>
   <td>1.9.2</td>
   <td>1.9.2</td>
 </tr>
 <tr>
   <td>RubyGem*</td>
   <td>1.8.16</td>
   <td>1.8.16</td>
 </tr>
 <tr>
   <td>COMPASS*</td>
   <td>0.11.3</td>
   <td>0.11.3</td>
 </tr>
 <tr>
   <td>SASS*</td>
   <td>3.1.3</td>
   <td>3.1.3</td>
 </tr>
 <tr>
   <td>GROOVY</td>
   <td>1.8.8</td>
   <td>1.8.8</td>
 </tr>
</table>

</br>

> *RubyGem is provided by the Ruby Installation. The Sass and Compass configuration is described in the section <b>Configuring Ruby Gems (Sass and Compass)</b>.

Obtain installation media and instructions for the various operating systems from the primary websites for each tool or trusted download source. The default locations are provided below. Also, install the tools in the order listed below. Once all tools have been installed, the following sections will describe how to configure the environment.

**Table: Tool Provider Websites**

<table>
<tr>
<th> Application </th>
<th> Location </th>
</tr>
<tr>
<td> JDK </td>
<td><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="http://www.oracle.com/technetwork/java/javase/downloads/index.html">http://www.oracle.com/technetwork/java/javase/downloads/index.html</a></td>
</tr>
<tr>
<td>ANT</td>
<td><a href="http://projects.apache.org/projects/ant.html" target="http://projects.apache.org/projects/ant.html">http://projects.apache.org/projects/ant.html</a></td>
</tr>
<tr>
<td>Grails</td>
<td><a href="http://www.grails.org/" target="http://www.grails.org/">http://www.grails.org/</a></td>
</tr>
<tr>
<td>Groovy</td>
<td><a href="http://groovy.codehaus.org/" target="http://groovy.codehaus.org/">http://groovy.codehaus.org/</a></td>
</tr>
<tr>
<td>Ruby</td>
<td><a href="http://www.ruby-lang.org/en/" target="http://www.ruby-lang.org/en/">http://www.ruby-lang.org/en/</a></td>
</tr>
</table>


### Setting Environment Variables
The build environment uses Apache Ant for most tasks. For Ant to run properly, it should discover the locations of the other supporting tools. This is accomplished by setting appropriate environment variables describing the install directory of each tool. On Windows 7, the following steps will set the **ANT\_HOME** variable, assuming an install location of **C:\Apache_Ant\apache-ant-1.8.3**.

1. Go to the Start menu and select Control Panel.
2. Click the System icon and select the Advanced System Settings link in the resulting window.
3. Click on the Advanced tab in the resulting pop-up and then select the Environment Variables button. For the following steps, if Administrator rights are available, use the System Variables section. If not, use the User variables section.
4. Create/Edit a variable named **ANT_HOME**. Set its value to **C:\Apache_Ant\apache-ant-1.8.3**. Save the new variable. On your system, the value should be the location where Ant was actually installed.
5. Create/Edit the Path variable. If the Path variable already contains the value **%ANT_HOME%/bin**, click Cancel. If the Path doesn’t contain the variable, append **;%ANT_HOME%/bin** to the end of the Path variable. Click OK until the system properties dialog is closed.
6. Download and install the Ant Contrib ZIP file in a Windows environment:

   A. Download **ant-contrib-1.0b3-bin.zip** from **http://sourceforge.net/projects/ant-contrib/files/ant-contrib/1.0b3/**.

   B. Unzip the contents of the file on the hard drive of the local machine. The result should be a folder named ant-contrib on the hard drive.

   C. Copy **ant-contrib-1.0b3.jar** to the lib directory of the local Ant installation.
This method should be repeated to set a **JAVA_HOME**, **ANT_HOME**, **GRAILS_HOME**, **GROOVY_HOME** and **RUBY_HOME** environment variable for each of their installation folders, respectively.

### Configuring Ruby Gems (Sass and Compass)
Configuring the required Ruby gems requires completion of the previous sections. Assuming a correct Ruby installation and Ruby being available on the Path variable, the following steps will install Sass and Compass:

1. Open a new Command Prompt window and enter the following:

        gem install sass --version 3.1.3 

2. There should be a response similar to the following:

        C:\Users\myusername>gem install sass --version 3.1.3
        Fetching: sass-3.1.3.gem (100%)
        Successfully installed sass-3.1.3
        1 gem installed
        Installing ri documentation for sass-3.1.3...
        Installing RDoc documentation for sass-3.1.3...
        C:\Users\myusername>

3. Then run the following command:

        gem install compass --version 0.11.3

4. There should be a response similar to:

        C:\Users\myusername>gem install compass --version 0.11.3
        Fetching: chunky_png-1.2.5.gem (100%)
        Fetching: fssm-0.2.9.gem (100%)
        Fetching: compass-0.11.3.gem (100%)
        Successfully installed chunky_png-1.2.5
        Successfully installed fssm-0.2.9
        Successfully installed compass-0.11.3
        3 gems installed
        Installing ri documentation for chunky_png-1.2.5...
        Installing ri documentation for fssm-0.2.9...
        Installing ri documentation for compass-0.11.3...
        Installing RDoc documentation for chunky_png-1.2.5...
        Installing RDoc documentation for fssm-0.2.9...
        Installing RDoc documentation for compass-0.11.3...
        C:\Users\myusername>

5. Ensure that the correct Ruby, Sass and Compass versions are installed.
6. From a Command Prompt window, run the following command:

        sass –v

   There should be a response that Sass 3.1.3 (Brainy Betty) is being used.

If a different version is running or a Sass error is displayed (e.g., “no such file to load”), execute the following steps to correct the Sass install:

1. In the Command Prompt window enter:

        gem uninstall sass

   Then choose which version to uninstall. 

        C:\Users\myusername>gem uninstall sass
        Select gem to uninstall:
 	    1. sass-3.1.3
 	    2. sass-3.1.15
	    3. All versions
	    > 2
	    Remove executables:
	    Scss in addition to the gem? [Yn]  y
	    Removing scss
	    Successfully uninstalled sass-3.1.15 

2. Run the sass -v again; see the example below: 
        
        C:\Users\myusername>sass -v
        Sass 3.1.3 (Brainy Betty) 
        C:\Users\myusername>

### Verify Tool Installations
To verify the installation and version of the tools, use the version command for each tool in a Command Prompt window. Example commands and output for an OWF 7 environment follow:

1. Enter java -version

        C:\Users\myusername>java -version
        java version "1.6.0_32-ea"
        Java(TM) SE Runtime Environment (build 1.6.0_32-ea-b03)
        Java HotSpot(TM) 64-Bit Server VM (build 20.7-b02, mixed mode)

2. Enter ant -version

        C:\Users\myusername>ant -version
        Apache Ant(TM) version 1.8.3 compiled on February 26 2012

3. Enter grails -version

        C:\Users\myusername>grails -version
        Welcome to Grails 1.3.7 - http://grails.org/
        Licensed under Apache Standard License 2.0
        Grails home is set to: C:\Grails\grails-1.3.7

4. Enter groovy -version

        C:\Users\myusername>groovy -version 
        Groovy Version: 1.8.8 JVM: 1.6.0_32

5. Enter ruby -v

        C:\Users\myusername>ruby -v
        ruby 1.9.2p290 (2011-07-09) [i386-mingw32]

6. Enter gem -v

        C:\Users\myusername>gem -v
        1.8.16

7. Enter sass -v

        C:\Users\myusername>sass -v
        Sass 3.1.3 (Brainy Betty)

8. Enter compass -v

        C:\Users\myusername>compass -v
        Compass 0.11.3 (Antares)
        Copyright (c) 2008-2012 Chris Eppstein
        Released under the MIT License. Compass is charityware. 
        Please make a tax deductible donation for a worthy cause: http://umdf.org/compass

## 3   Building
If changes are being made to the server code, the developer does not normally need to run build tasks to test them. Instead, use the standard grails scripts to run or test the server code. Use the Ant build when there is the need to build a server bundle, i.e. package the WAR files, along with a Tomcat instance into a ZIP file that can then be distributed to an end user. To build a server bundle, open a Command Prompt window and ‘ **cd** ’ into the server’s base directory. 

To build the bundle, type the following on the command line and press Enter:

        C:\owf-server>ant bundle

The bundle task will do a clean and build of the server code (retrieving any dependencies), run the server tests (both unit and integration) and then build the zipped bundle. The results of the build are written to the staging directory within the server directory. The staging directory of a successful build should contain the zipped bundle, as well as the unzipped contents of the bundle. The latter is provided as a convenience to test the bundle by running the start.bat (or **start.sh** on Linux systems) in the **staging/apache-tomcat-x.x.x** directory. This will start the Tomcat server which is initially configured to load the Ozone server and the CAS server WAR files.

### Additional Build Command Line Options
When running the build, use any (or all) of the following command line parameters:
* **-logfile build.log** – This will redirect the output of the build to the specified log file. This can be useful when there are problems with the build because the output is often too verbose to be completely captured by the Command Prompt window.
* **-Dno-test=true** – This will prevent the grails unit and integration tests from running. Often, they’ve already run. Using this option will speed up the build.
* **-Dno-jsdoc=true** – This will prevent the generation of the JavaScript documentation. Generating the documentation is time consuming and slows the build progress.
* **-Dgroovy\_all** – This property can be used to manually set the location of groovy-all.jar. This property needs to be set correctly when building to the **GROOVY_HOME** environment variable. The purpose of this property is to allow building on systems where Groovy was installed in such a way that the **GROOVY_HOME** variable is not set, such as Linux systems that installed Groovy using a centralized package manager. See below for an example: 

        ant bundle -Dgroovy_all=/usr/share/java/groovy-all.jar

### Troubleshooting
* Grails plugins used by the applications have their own dependencies. In some cases these are not required for the base application; e.g. In Alpha/Beta releases these may be experimental or partially built-out capabilities. If a plugin is causing issues,  it may be removed by:
   * Modifying the **[root]/application.properties** file and commenting out the line beginning with ‘ **plugins.[pluginName]** ’.
   * Moving the **[root]/plugins/[pluginName]** directory out of the project.

> _Note: Other references to the plugin may exist in places and this procedure may be insufficient to avoid all possible errors._

* Testing Grails compilation outside of the Ant script can be useful for diagnosing Grails-level configuration issues without executing all other aspects of the build process. To do this, run the following from a Command Prompt Window:

        grails compile -DOFFLINE_REPO= c:/path/to/ivy-repo/no-namespace

* If the following build failure occurs,  

        c:\Development\GitFlip\owfBuildTest\build.xml:227: The following error occurred while executing this line:
        c:\Development\GitFlip\owfBuildTest\tools\TestDbConversion\build.xml:23: 
        c:\Development\GitFlip\owfBuildTest\tools\TestDbConversion\${env.GROOVY_HOME}\embeddable not found.

  ensure that **GROOVY_HOME** is set in your environment. 

## 4 Other Prebuilt Artifacts
### CAS Server War
The CAS Server WAR provides a very simple login form interface to CAS, a single sign-on solution provided by jasig.  Previously built distributions of this artifact are now made available through Nexus.  As this is considered useful for packaged delivery, but not actually part of OWF's capabilities, build support for this artifact is not currently supported.  Consult the [CAS](http://www.jasig.org/cas) project within the jasig community for further guidance.

### Tomcat-OWF-Custom
Changing the configuration of this artifact is not currently supported.  Previously built distributions of this artifact are now made available through Nexus.

## 5 Contact Information
For additional support, see [Support Guidance](https://github.com/ozoneplatform/owf/wiki/Support-Guidance).  Specifically, seek out the group for developers.