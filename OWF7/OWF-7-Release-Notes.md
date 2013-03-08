# OWF 7 Release Notes 
OWF 7 Release Date: December 21, 2012

#Release Notes

##1 Installation Information

OWF installation instructions are found in the [Configuration Guide](Configuration-Guide-Home).

##2 Upgrade Information

Instructions for upgrading from older versions of OWF are found in the Configuration Guide Appendices.

##3 Compatibility with Marketplace

OWF has been tested against Marketplace versions 2.5 and 5.

##4 OWF 7 Epics

###Epic: OWF-5803: Stacks

* **OWF-5804** — As an Administrator, I would like to be able to create, edit, and delete stacks. 
* **OWF-5805** — As an Administrator, I would like to be able to add existing dashboards to a stack. 
* **OWF-5806** — As an Administrator, I would like to be able to assign groups to a stack.
* **OWF-5997** — As an End User, I would like to be able to switch from one OWF stack to another. 
* **OWF-6271** — As an Administrator, I would like to be able to have a URL for a stack. 
* **OWF-6327** — As an Administrator, when adding a stack to OWF, I would like to be able to specify a stack descriptor URL and have all of the stack, dashboard, and widget information (title, description, icon URLs, etc.) added automatically. 
* **OWF-6328** — As an Administrator, I would like to export stack information (title, dashboard definitions, widget definitions, etc.) to a file so that stacks can easily be added to other OWF instances or migrated from development to staging to production. 
* **OWF-6391** — As an Administrator, I would like to be able to assign users to a stack. 
* **OWF-6392** — As an Administrator, I would like to be able to see a list of the widgets for a stack. 
* **OWF-6497** — As an Administrator, I would like to be able to assign a specific order for dashboards in a stack. 
* **OWF-6881** — As an End User, I would like to be able to drag and drop reorder dashboards and stacks. 
* **OWF-6896** — As an End User, I would like to be able to restore a dashboard for a stack. 
* **OWF-6897** — As an End User, I would like to be able to restore a stack including dashboards, widgets, etc.

###Epic: OWF-6036: IE 7 & 8 Tuning

Performance is 9 to 38 percent faster depending on the complexity of the dashboards.

##5 Additional User Stories

* **OWF-2023** — As an Administrator, I would like to be able to export a widget so that I can import it into another instance. 
* **OWF-3763** — As a Developer, I would like to modify widget titles using the Widget Chrome API. 
* **OWF-6115** — As a Developer, I would like to specify a widget title when launching a widget using Launching API. 
* **OWF-6535** — As an Administrator, I would like to be able to create, edit, and delete widget intents on the Intents tab for a widget.

##6 Improvements

* **OWF-3687** — Refresh the administration managers automatically when adding, editing, or deleting items with the administration editors. 
* **OWF-4226** — Add a confirmation message when adding a widget from Marketplace. 
* **OWF-4296** — Theme the CAS log in and log out screens. 
* **OWF-6231** — Documentation styling improvements. 
* **OWF-6403** — Add multiple zIndexManagers to represent the various floating layers (base, floating widget, banner, dashboard designer and tooltips). 
* **OWF-6526** — Add descriptor files for all standard OWF example widgets. 
* **OWF-6530** — Add better error handling when the setActiveItem method in BufferedCardLayout.js returns false. 
* **OWF-6534** — Add descriptions in the descriptor files for the sample intents widgets.  
* **OWF-6594** — When a user edits a dashboard, they should be taken to it. 
* **OWF-6657** — Update OWF Overview video. 
* **OWF-6787** — Add help video for Widget Overview (intents, launch menu, customization). 
* **OWF-6795** — Add universal name to widget search. 
* **OWF-6799** — Update screenshots if needed.
* **OWF-6800** — In the Launch Menu, when selecting a current Instance of a widget, highlight it on the dashboard. 
* **OWF-6803** — Add help video for Dashboard Switcher. 
* **OWF-6843** — Add help video for 508 Accessibility Features. 
* **OWF-6863** — Add help video for Drop-down User Menu. 
* **OWF-6873** — Add help video for Dashboard Designer. 
* **OWF-6885** — Add help video for User Manager Overview. 
* **OWF-6895** — Add a slight delay to the user pull down in the toolbar like there is for the hover on the toolbar buttons. 
* **OWF-6985** — Add way for developers to know if a widget is launched via Intents API. 
* **OWF-6992** — Make the paths in OWF relative. 
* **OWF-6994** — Add help video for Marketplace Overview for OWF Users. 
* **OWF-7024** — Add an indicator that the changes I've made have been saved upon hitting "Apply" in the admin editor widgets. 
* **OWF-7042** — Update the example widgets that come with OWF. 
* **OWF-7067** — Open the Marketplace widget if there is only one in the Marketplace selector window. 
* **OWF-7094** — Update OwfConfig.groovy to hide unnecessary files in the Help section of the UI and add htm as an output type. 
* **OWF-7102** — Update OWF docs to show that you can launch a widget by universal name. 
* **OWF-7105** — Document how to send an Intent directly to widgets in Developer Guide. 
* **OWF-7108** — Change divider tooltip on the Dashboard Designer screen. 
* **OWF-7197** — Improve clarity of Stack Editor and Widget Editor text. 
* **OWF-7219** — Make the widget fields editable when importing a widget from a descriptor. 
* **OWF-7221** — Improve the instructions for using shims in the Configuration Guide. 
* **OWF-7234** — Improve message when restoring a dashboard. 
* **OWF-7249** — Update OWF Overview video for OWF 7 release. 
* **OWF-7310** — Include universal name in OWF.getOpenedWidgets.

##7 Fixes
* **OWF-2320** — Tool tip for paging and refresh shows at top of widget instead of near the button. 
* **OWF-2438** — Importing a dashboard that includes inaccessible widgets and then bringing up the eventing window for that user, causes an undefined error. 
* **OWF-2449** — In the "Add Preferences" dialog box the "Value" field is cut off on the bottom. 
* **OWF-2739** — Most combo boxes in system are either blank to begin or go blank when user selects the drop-down arrow. 
* **OWF-3836** — Search breaks in all admin widgets if the user scrolls down first in the current grid. 
* **OWF-4088** — Trying to save a new Tabbed dashboard produces an error of "TypeError : g is undefined". 
* **OWF-4434** — Dashboard Import does not fill in description text. 
* **OWF-4691** — If you open any of the Settings windows with background widgets open and use the SHIFT+ALT+W shortcut to close it, it will close the last focused widget in the background. 
* **OWF-4869** — Tool tip for toolbar shows behind toolbar if the toolbar is in floating state and at bottom of browser window. 
* **OWF-5553** — Calendar icon in Widget Views widget moves one pixel to left on mouse over and two pixels left on select while using Large Text theme. 
* **OWF-5568** — Scroll bar for Widgets grid breaks when you go to second page and return to first page in Widget Views widget. 
* **OWF-5966** — Firebug error when you mouse over a widget name in Widget Views widget cloud tab that contains white space. 
* **OWF-6006** — Widget Views widget tag cloud highlights incorrect widget when multiple widgets with same name are listed. 
* **OWF-6039** — The 'ant init-build' script no longer runs without ant-contrib JAR file. 
* **OWF-6111** — Dashboards modal window allows focus to leave the window through the keyboard. 
* **OWF-6113** — Tooltips are not showing for icons in several modal windows. 
* **OWF-6129** — The user's display name in the user menu and all information in the user's profile window should be encoded to prevent HTML injection. 
* **OWF-6134** — Tags column in Widget Settings window allows sorting.
* **OWF-6138** — There is a mismatch between the length of the description in OWF and Marketplace. 
* **OWF-6162** — Help icon on Widget Editor is incorrect for descriptor URL. 
* **OWF-6183** — When launching a widget from the launch menu by pressing the enter key a user can no longer click to drop the widget. 
* **OWF-6200** — Selecting row should not select a checkbox in the NYSE widget. 
* **OWF-6202** — Remove white space on Widget Editor widget when descriptor file is loaded. 
* **OWF-6205** — HTML Viewer widget shows incorrect color scheme for tabs in widget. 
* **OWF-6206** — Widget properties tab has horizontal scrollbar in Google Chrome. 
* **OWF-6251** — Remove intentWidget1_descriptor.html from bundle. 
* **OWF-6257** — Example template descriptor file different from descriptor examples in bundle. 
* **OWF-6293** — Pop out banner can appear in front of the mask of modal windows, allowing further interaction. 
* **OWF-6468** — Update OWF documentation regarding installation of ruby/compass/sass, instructions not fully correct. 
* **OWF-6478** — With the White on Black theme, users can not read every other record in the sample NYSE widget. 
* **OWF-6481** — Launch Menu Launch button text is difficult to read when using keyboard navigation. 
* **OWF-6517** — The order of widgets from background to foreground is not persisted. 
* **OWF-6518** — Metrics widget throws errors on mouse over of widget name with special characters in it. 
* **OWF-6527** — OWF Configuration Guide Theming section updates for clarification. 
* **OWF-6579** — Add menu configuration text box runs beyond widgets boundaries. 
* **OWF-6580** — The OWF watermark on the access alert page is offset to the top of the screen. 
* **OWF-6582** — Removing any menu item from widget chrome sample widget causes an error in IE 7.
* **OWF-6584** — With quirks mode off (Internet Explorer 9 standards) the Channel Shouter and Listener do not work properly. 
* **OWF-6588** — Cannot remove the description of a dashboard even though it is not a required field. 
* **OWF-6590** — The collapse option in a portal dashboard breaks if scrolling is needed in IE 7. 
* **OWF-6592** — Administration editor widgets allow focus to leave Add window. 
* **OWF-6593** — Marketplace shortcut/keyboard navigation (ALT + SHIFT + M) doesn't work to close the Marketplaces Switcher. 
* **OWF-6599** — If a widget launches another widget from inside a fit pane, the location of the widget it launches will be stuck in the fit pane.

##8 Security

* **OWF-5838**, **OWF-6128**, **OWF-7265**, **OWF-7266**, **OWF-7269** — Corrected a set of potential XSS vulnerability areas. 
* **OWF-6973** — Widget descriptor allows HTML Injection and XSS scripting in description field. 
* **OWF-7130** — XSS Vulnerability in example widgets Channel Shouter, HTML Viewer, NYSE, and Stock Chart. 
* **OWF-7311** — Dashboard Editor window has XSS vulnerability. 
* **OWF-7312** — Add Dashboard to Group window has XSS vulnerability. 
* **OWF-7317** — User Editor's invocation of the Dashboard editor from its Dashboard tab (via edit button) has an XSS exploit in the title. 
* **OWF-7291** — Widget Chrome API allows widgets to inject html and JavaScript into the container.

## 9 Known Issues

None