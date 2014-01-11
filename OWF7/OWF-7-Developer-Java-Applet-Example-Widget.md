#  Java Applet Example

The applet example demonstrates how a Java applet could be implemented as a widget within OWF. It takes Michael Keating’s [MyChessViewer](http://www.mychess.com/), an applet that reads and animates a chess **.PGN** file, and incorporates it into the framework. It has been modified to do the following:

* Broadcast each forward move selected on a channel named **mychess**.
* Store the current position in the game to the Preference Service.

After deploying the widget to OWF, the sample Channel Listener widget can be used to monitor the **mychess** channel. Clicking on the next button within the applet will send a message about the move. Coming back to the widget after closing the browser will return it to the last move performed. 

#1   Technologies

The following is required to build/deploy this example:

* A JDK installation of 1.6 or higher.
* Apache ANT 1.7 or higher.
* A Web server such as Apache or IIS

#2   Building/Compilation

1. Extract **\java-applet-widget.zip** into a new directory.
2. Replace all occurrences of `https://servername:port` with the name of the server where OWF is running, for example, `https://www.yourcompany.com:8443`. Additionally, be sure to verify that the windowname library paths point to the local installation.
3. Open a command prompt and navigate to the directory created in Step 1.
4. Type `ant`. The resulting **owf-sample-applet.war** file will be in the target directory and can be deployed to the widget server.
5. By default, the widget looks for the framework JavaScripts on localhost. Accordingly, change the location of the source in the **\java-applet-widget\src\main\webapp\widget.jsp** file to reflect the actual location of the OWF server: 

```html
        <script type="text/javascript" src="https://localhost:8443/owf/js/config/config.js"></script>
        <script type="text/javascript" src="https://localhost:8443/owf/js/util/error.js"></script>
        <script type="text/javascript" language="javascript" src="https://localhost:8443/owf/js-min/owf-widget-min.js"></script>
```

To test that the widget properly publishes data, do the following: 

1. Follow the steps on the [Adding a Widget to OWF](OWF-7-Developer—Adding-a-Widget-to-OWF) in order to create widget definitions which point to **widget.jsp**, assign the widget to a user, and then apply the widget to one of the user’s dashboards. Use the following widget definitions:

 **Table: JavaApplet Widget Definition Text**

<table>
  <tr>
    <th>Definition</th>
    <th>Data Input Field</th>
  </tr>
  <tr>
    <td>URL</td>
    <td>http://widget-server-name:port/owf-sample-applet/widget.jsp</td> 
  </tr>
  <tr>
    <td>Large Icon</td>
    <td>http://widget-server-name:port/owf-sample-applet/images/chess.gif</td> 
  </tr>
  <tr>
    <td>Small Icon</td>
    <td>http://widget-server-name:port/owf-sample-applet/images/white-queen.gif</td> 
  </tr>
  <tr>
    <td>Width</td>
    <td>670</td> 
  </tr>
  <tr>
    <td>Height</td>
    <td>655</td> 
  </tr>
</table>

2. Enter OWF and select the dashboard which contains the widgets mentioned in the steps above.
3. Launch the Listener Widget and the Chessboard Widget created in Step 1.
4. Add the **mychess** channel to the Listener Widget. Do not include the quotations.
5. As moves are applied to the chess game, the listener will display the appropriate information.

#3   Known Issues

The applet needs to access the browser's JavaScript object, which requires some additional security. The easiest way to accomplish this is to sign the **.jar**. The security directory contains a keystore and a DOS batch file to create a new one. During the build process, this keystore is used to sign the **.jar** file. The first time the applet is run, the user will be prompted to trust the test certificate. Allowing it will avoid further prompting.

The classes needed to access the JavaScript object are part of the normal Sun JDK in the **plugin.jar**. For simplicity, the .jar has been copied into this project's lib directory from the `Java JDK v1.6.0_07`. Verify that the **plugin.jar** exists on the classpath when using a custom deployment scenario.

There is a documented issue with Java applets not obeying proper z-indexing, the effect being that an applet will appear on top of everything else in the widget framework:
[http://bugs.sun.com/bugdatabase/view_bug.do;jsessionid=6a434ce1408465ffffffff87e84af5d233a32?bug_id=6646289](http://bugs.sun.com/bugdatabase/view_bug.do;jsessionid=6a434ce1408465ffffffff87e84af5d233a32?bug_id=6646289).