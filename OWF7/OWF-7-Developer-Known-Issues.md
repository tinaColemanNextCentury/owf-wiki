#Known Issue
#1   User Interface Issues

**Changes in screen resolution may render widgets un-viewable.**

The positioning of the widgets is absolute. This means that when changing from a larger monitor to a smaller monitor, or when changing from a higher screen resolution to a lower screen resolution, some floating windows may be either partially or fully off the viewable region of the screen. Currently there is no remedy for this issue. As a workaround, close the widget. Then, re-add it from the Launch Menu. This will reset its position and therefore, render it viewable again.

**Large widgets in Accordion layout may cause unexpected behavior.**

The accordion layout currently has a propensity to enter an unexpected state when widgets with height exceeding the maximum screen real estate are added to the right upper region. This can be remedied with a system administrator modifying the Dashboard state and will be fixed in a future release.

#2   Widget Technology Issues

**Java Applet Widgets always sit on top of other widgets (z-index issue).**

There is a documented issue with Java applets not obeying proper z-indexing; the effect being that an applet will appear over everything else in OWF:

http://bugs.sun.com/bugdatabase/view_bug.do;jsessionid=6a434ce1408465ffffffff87e84af5d233a32?bug_id=6646289

**Flex Widgets always sit on top of other widgets (z-index issue).**

Flex has a known issue with DHTML and z-index ordering. The default wmode for flex is window with two other options; transparent and opaque. In order for Flex Widgets to adhere to the proper z-index ordering the wmode must be set to something other than the default.

**Silverlight Widgets always sit on top of other widgets (z-index issue).**

Silverlight has a known issue with DHTML and z-index ordering. The default windowless mode for Silverlight is false. In order for Silverlight widgets to adhere to the proper z-index ordering the windowless mode must be set to true.

**Google Earth Plugin Widgets always sit on top of other widgets (z-index issue).**

The Google Earth browser plugin currently does not conform to the normal z-index rules of html. This will cause the plugin to remain on top of any other floating windows that may be on the screen. If using this plugin, it is recommended not to utilize it in the desktop layout. It can be used in any of the other static layouts but windows launched from the toolbars may be rendered unreachable by the plugin.

#3   Database Issues

**Oracle scripts should be executed via the SQL*Plus command line.**

There have been reported issues using Oracle's browser-based administration console to upload and run the OWF create and update scripts. Stray characters are getting inserted into the database, causing JSON parsing errors at runtime. Executing the scripts through the SQL*Plus command line utility eliminates this issue.
