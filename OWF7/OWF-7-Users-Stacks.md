#Stacks

##1   Overview
A stack is a collection of dashboards and widgets. Stacks compile OWF resources and make them easy to access and restore. Stacks and their dashboards appear in the Switcher. Administrators can use stacks to separate and categorize widgets and dashboards for specific users, groups or projects. For example, an administrator for a disaster recovery organization might create a stack that relates to a specific disaster. A stack for a specific hurricane could include dashboards relating to the region’s road access, local and federal relief centers and cell phone coverage.
 
* Users assigned to a stack can customize the stack’s dashboards and widgets. Those changes will only affect their instance of the stack.
* If an administrator updates a stack, users will receive the change(s) when they restore their instance of the stack.

Restoring a stack returns the stack to its current default state. If an administrator updated the stack after it was added to a user’s instance of OWF, the restored version may look different than the one the user originally received. 

##2   Using Stacks
A user’s list of stacks appears intermingled with dashboards under the Switcher button on the toolbar. When a user selects a stack, a list of dashboards associated with that stack appears below it. If an administrator removes a user from a stack or deletes it, the stack including its dashboards and widgets will disappear from the user’s instance of OWF. If a user deletes the stack from their instance of OWF, its dashboards and widgets will be removed unless the stack is assigned to one of the user’s groups. In that case, the user cannot remove the stack.  

###Switching Stacks
When a user selects a stack, a list of dashboards associated with the stack appear below it, as shown in the following figure:

![Dashboards in a Stack](OWFImages/OWF7/stack_example.png)

<b>Figure: Dashboards in a Stack</b>

1. To switch to differt stack, open the Switcher by clicking the Switcher button on the toolbar.
2. Click a stack to select it.
3. Click one of the dashboards from the stack.

###Reordering Stacks
To reorder stacks in the Switcher, select the stack and drag it to the new location on the Switcher.

###Restoring Stacks

When a user receives a stack, they receive copies of the dashboards and widgets that are associated with the stakc. From their intance of OWF, a user can customize their version of the tack's dashboards and widgets. The restore feature allows the user to cancel those customizations and returns the dashboards and widget to the <i>current default state</i> in the stack. If any of the dashboards or widgets associated with the stack changed after they were added to the user’s instance of OWF, the current default state may differ from the one that originally appeared in the user’s Switcher.

To restore a stack to its <i>current default state</i>:

1.	Click the   button in the toolbar to open the Switcher, click the Manage button. 
2.	Select the stack, editing buttons will appear under it. Click the Restore button.
3.	The stack (including all of its dashboards and widgets) will return to its current default state.

#3 Deleting Stacks

Users cannot add stacks. They have to ask administrators for access to them. Users can, however, delete their copies of stacks. To delete a stack:

1.	Click the Switcher button in the toolbar to open the Switcher, click the Manage button. 
2.	Select the stack, editing buttons will appear under it. Click the Delete button.
3.	After a warning, the stack (including all of its dashboards and widgets) will be removed from the user’s instance of OWF.
