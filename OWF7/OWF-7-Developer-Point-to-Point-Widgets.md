#  Additional Widgets
#   Point-to-Point (RPC) Widget

Included with the widgets that ship in the OWF bundle are the point-to-point Color Server and the point-to-point Color Client. Together, these two widgets showcase point-to-point eventing.

A brief description of these two widgets and how they work together can be found below:

#1   Color Server Widget

![Color Client Widget](OWFImages/OWF7/color_server_widget.png)

**Figure: Color Server Widget**

The Color Server Widget performs two functions, each shown in the code block which follows. The `getColors()`function returns a list of all supported colors. The second function, `changeColor(color)`, can change the background color. On load of this widget, both functions are registered via the `Ozone.eventing.clientInitialize()` function, enabling them to be called remotely. In the example below, they are be called by a user from the Color Client Widget shown in section 2: **Color Client Widget**.

The code for the Color Server Widget is shown below:

![Section 15.1.1 codeblock](OWFImages/OWF7/dev_guide_15.1.1_codeblock.png)

#2   Color Client Widget

![Color Client Widget](OWFImages/OWF7/color_client_widget.png)

**Figure: Color Client Widget**

The Color Client widget contains a button that, when clicked, calls the Color Server’s `getColors()` function to populate the adjacent dropdown list with the colors supported by the Color Server Widget. When a user selects a color from the dropdown menu , the client calls the server’s `changeColor()` method to change the server widget’s background color. The function is wrapped inside the `Ozone.eventing.importWidget()` function to obtain a reference to the remote server endpoint.

The code for the Color Client Widget is shown below:

![Section 15.1.2 codeblock 1](OWFImages/OWF7/dev_guide_15.1.2_codeblock_1.png)
![Section 15.1.2 codeblock 2](OWFImages/OWF7/dev_guide_15.1.2_codeblock_2.png)