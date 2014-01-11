#Accessing Marketplace
# 1 Marketplace
Marketplace, similar to a commercial application store, operates as a thin-client registry of applications and services. From the Marketplace widget in OWF, users can browse, download and use a variety of applications.

##Accessing Marketplace

Provided that OWF has been configured to recognize an instance of Marketplace, clicking the Marketplace button on the toolbar will open the Marketplace Switcher which may offer connections to multiple Marketplaces. 

![Marketplace Switcher](OWFImages/OWF7/mp_switcher.png)

<b>Figure: Marketplace Switcher</b>

In the Marketplace Switcher, users must click on a Marketplace to launch it. If only one Marketplace is available, it will open automatically when the Marketplace button is clicked in the toolbar. Following proper authentication, the user can browse Marketplace listings and add any of the listings that have been designated OWF aware. For listings to appear in OWF, they must be approved and enabled in Marketplace.

## Adding Widgets from Marketplace

Users can add a Marketplace listing to their instance of OWF by selecting the listing, clicking the drop-down Actions button and selecting Add Widget. 

![Adding Widgets from Marketplace](OWFImages/OWF7/adding_widgets_from_mp.png) 

<b>Figure: Adding Widgets from Marketplace</b>

##Pending Approval Widgets

When a user selects a widget it is automatically added to the user’s Launch Menu, unless, the system requires that an administrator approve it before use. If administrator approval is required, the widget will be visible in the Launch Menu. However, it will be grayed out, as shown in the following figure. Once approved, the gradient will be removed and the user can launch the widget. 

> _Note: If a user tries to launch a pending widget, an error message will appear._

# 2 Required Widgets
Some widgets will not function (or will have limited functionality) if they launch without other widgets. OWF automatically adds Required widgets when a user adds a widget that needs them. For example:  A user adds the Navigating Widget. The Navigating Widget requires the Satellite Widget and the Coordinate Calculator Widget. The user has not requested the additional two widgets but they are automatically added because the Navigating Widget requires them. 

![Adding Required Widgets](OWFImages/OWF7/adding_required_widgets.png)

<b>Figure: Adding Required Widgets</b>

Some things to consider: 

* A user must add all Required widgets from Marketplace. Users do not have the option to deselect any of the Required widgets. 
* A widget’s Required widgets will appear in the Launch Menu if its Visible menu field is set to true. 

##Deleting Required Widgets

Like any other widget, required widgets can be deleted from the Widget Settings window which is located by clicking the Settings button on the toolbar and then choosing Widgets. However, if a user or administrator deletes a Required widget, any widgets that require that widget will automatically be deleted after the system displays a warning notification. Other widgets that are related to the dependent widgets will remain. For example, the Navigating Widget requires the Satellite Widget and the Coordinate Calculator Widget. If the Coordinate Calculator is deleted, the Navigating Widget will be deleted but the Satellite Widget will remain because it does not require the Coordinate Widget. 