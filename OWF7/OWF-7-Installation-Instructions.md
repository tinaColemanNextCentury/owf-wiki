Use the following instructions to build OWF. 

#Instructions
##Objectives
The purpose of this document is to describe how to build the following projects:

* **OWF Server** – A local copy of the bundled (owf-server.war + cas-server.war + owf-samples + Tomcat) ZIP file as well as the release version.
* **OWF Security JAR** – A new version of the owf-security JAR file.
* **Build-Base** – A common set of files used by all the other OZONE project builds. Its role is described in the [Build Base](OWF-7-Build-Base). 

##Requirements
This document is targeted to widget developers and assumes a basic familiarity with the target development environment, be it Microsoft Windows or Linux. Before any of the build tasks can run, the developer must install Ant 1.7.1, Ant Contrib 1.0b3 and Grails 1.3.7. The following sections list the tools, the version requirements for recent OWF releases and nominal configuration elements. Instructions provided below assume a Microsoft Windows development environment for illustrative purposes only. 

###Download and Install Applications
OWF Development requires the use of the Java Development Kit (JDK), Apache Ant, Apache Ant Contrib, Ruby, RubyGems, Compass and Sass, as well as Groovy. The following table lists the versions of each tool required by the last few OWF and Marketplace releases.

**Table: OWF Development Tools and Version Numbers**

<table>
 <tr> 
<th>Application</th>
<th>JDK</th>
<th>ANT</th>
<th>Ant Contrib</th>
<th>GRAILS</th>
<th>RUBY</th>
<th>RubyGem*</th>
<th>COMPASS*</th>
<th>SASS*</th>
<th>GROOVY</th>
</tr>
<tr> 
<td> OWF 4 </td>
<td> 1.6 </td>
<td> 1.7 </td>
<td> - </td>
<td> 1.3.7 </td>
<td> 1.8.7 </td>
<td> 1.8.16 </td>
<td> 0.11.3 </td>
<td> 3.1.3 </td>
<td> - </td>
</tr>
<tr> 
<td> OWF 5 </td>
<td> 1.6 </td>
<td> 1.8 </td>
<td> - </td>
<td> 1.3.7 </td>
<td> 1.8.7 </td>
<td> 1.8.16 </td>
<td> 0.11.3 </td>
<td> 3.1.3 </td>
<td> - </td>
</tr>
<tr> 
<td> OWF 6 </td>
<td> 1.6 </td>
<td> 1.8 </td>
<td> 1.0b3 </td>
<td> 1.3.7 </td>
<td> 1.9.2 </td>
<td> 1.8.16 </td>
<td> 0.11.3 </td>
<td> 3.1.3 </td>
<td> 1.8.8 </td>
</tr>
<tr> 
<td> OWF 7 </td>
<td> 1.6 </td>
<td> 1.8.3 </td>
<td> 1.0b3 </td>
<td> 1.3.7 </td>
<td> 1.9.2 </td>
<td> 1.8.16 </td>
<td> 0.11.3 </td>
<td> 3.1.3 </td>
<td> 1.8.8 </td>
</tr>
</table>
</br>

> *RubyGem is provided by the Ruby Installation. The Compass and Sass configuration is described in the **Configuring Ruby Gems (Compass and Sass)** section.

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


###Setting Environment Variables
The build environment uses Apache Ant for most tasks. For Ant to run properly, it should discover the locations of the other supporting tools. This is accomplished by setting appropriate environment variables describing the install directory of each tool. On Windows 7, the following steps will set the `ANT_HOME` variable, assuming an install location of `C:\Apache_Ant\apache-ant-1.8.38`.

1. Go to the Start menu and select Control Panel.
2. Click the System icon and select the Advanced System Settings link in the resulting window.
3. Click on the Advanced tab in the resulting pop-up and then select the Environment Variables button. For the following steps, if Administrator rights are available, use the System Variables section. If not, use the User variables section.
4. Create/Edit a variable named `ANT_HOME`. Set its value to `C:\Apache_Ant\apache-ant-1.8.3`. Save the new variable. On your system, the value should be the location where Ant was actually installed.
5. Create/Edit the Path variable. If the Path variable already contains the value `%ANT_HOME%/bin`, click Cancel. If the Path doesn’t contain the variable, append `;%ANT_HOME%/bin` to the end of the Path variable. Click OK until the system properties dialog is closed.
6. Download and install the Ant Contrib ZIP file in a Windows environment:
<br>
       A. Download `ant-contrib-1.0b3-bin.zip` from [http://sourceforge.net/projects/ant-contrib/files/ant-contrib/1.0b3/](http://sourceforge.net/projects/ant-contrib/files/ant-contrib/1.0b3/).<br>
       B. Unzip the contents of the file on the hard drive of the local machine. The result should be a folder named `ant-contrib` on the hard drive.<br>
       C. Copy `ant-contrib-1.0b3.jar` to the lib directory of the local Ant installation.
This method should be repeated to set a `JAVA_HOME`, `ANT_HOME`, `GRAILS_HOME`, `GROOVY_HOME` and `RUBY_HOME` environment variable for each of their installation folders, respectively.

###Configuring Ruby Gems (Sass and Compass)
Configuring the required Ruby gems requires completion of the previous sections. Assuming a correct Ruby installation and Ruby being available on the Path variable, the following steps will install Compass and Sass:

1. Open a new Command Prompt window and enter the following:

        gem install compass –version 0.11.3 

2. There should be a response similar to the following:

        C:\Users\myusername>gem install compass -version 0.11.3
        Fetching: sass-3.1.15.gem (100%)< 
        Fetching: chunky_png-1.2.5.gem (100%) 
        Fetching: fssm-0.2.9.gem (100%)
        Fetching: compass-0.11.3.gem (100%) 
        Successfully installed sass-3.1.15 
        Successfully installed chunky_png-1.2.5 
        Successfully installed fssm-0.2.9 
        Successfully installed compass-0.11.3 
        4 gems installed 
        Installing ri documentation for sass-3.1.15...
        Installing ri documentation for chunky_png-1.2.5... 
        Installing ri documentation for fssm-0.2.9... 
        Installing ri documentation for compass-0.11.3... 
        Installing RDoc documentation for sass-3.1.15... 
        Installing RDoc documentation for chunky_png-1.2.5... 
        Installing RDoc documentation for fssm-0.2.9... 
        Installing RDoc documentation for compass-0.11.3... 
        C:\Users\ myusername> 

3. Then run the following command:

        gem install sass—version 3.1.3

4. There should be a response similar to:

        C:\Users\myusername>gem install sass --version 3.1.3
        Fetching: sass-3.1.3.gem (100%)
        Successfully installed sass-3.1.3
        1 gem installed
        Installing ri documentation for sass-3.1.3...
        Installing RDoc documentation for sass-3.1.3...
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

###Verify Tool Installations
To verify the installation and version of the tools, use the version command for each tool in a Command Prompt Window. Example commands and output for an OWF 7 environment follow:

1. Enter java –version

        C:\Users\myusername>java –version
        java version "1.6.0_32-ea"
        Java(TM) SE Runtime Environment (build 1.6.0_32-ea-b03)
        Java HotSpot(TM) 64-Bit Server VM (build 20.7-b02, mixed mode)

2. Enter ant –version

        C:\Users\myusername>ant –version
        Apache Ant(TM) version 1.8.3 compiled on February 26 2012

3. Enter grails –version

        C:\Users\myusername>grails -version
        Welcome to Grails 1.3.7 - http://grails.org/
        Licensed under Apache Standard License 2.0
        Grails home is set to: C:\Grails\grails-1.3.7

4. Enter groovy –version

        C:\Users\myusername>groovy –version 
        Groovy Version: 1.8.8 JVM: 1.6.0_32

5. Enter ruby –v

        C:\Users\myusername>ruby –v
        ruby 1.9.2p290 (2011-07-09) [i386-mingw32]

6. Enter gem –v

        C:\Users\myusername>gem –v
        1.8.16

7. Enter sass –v

        C:\Users\myusername>sass –v
        Sass 3.1.3 (Brainy Betty)

8. Enter compass –v

        C:\Users\myusername>compass -v
        Compass 0.11.3 (Antares)
        Copyright (c) 2008-2012 Chris Eppstein
        Released under the MIT License. Compass is charityware. 
        Please make a tax deductible donation for a worthy cause: http://umdf.org/compass