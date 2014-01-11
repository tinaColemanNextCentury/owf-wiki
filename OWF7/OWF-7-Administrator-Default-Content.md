# Default Content

OWF ships with a default user profile and default user group. Administrators can use the default profile and default group to add widgets, dashboards and stacks to a user or several users’ instance of OWF. 

<b>DEFAULT_USER</b> – A default user profile that ships with OWF. The DEFAULT_USER data will automatically be assigned to every new user of a particular OWF installation. 

When a new user enters OWF for the first time, the DEFAULT_USER data will be applied and copied to that user’s profile. After the initial login, any changes that the user makes will only impact their data from that point on. The DEFAULT_USER data remains unchanged and will continue to be applied to all new users. 

> _Note: If an administrator makes changes to the DEFAULT_USER data set, it will only impact the users who log in for the first time, following the change. Any users who received the data prior to the change will not be affected._ 

![User Dialog](OWFImages/OWF7/user_manager_dialog.png)

**Figure: User Dialog/DEFAULT_USER**

<b>OWF Users</b> – A default user group that ships with OWF. Every new user is automatically assigned to it. 

When a new user enters OWF for the first time, the OWF Users group data will be applied and copied to that user’s profile. After the initial login, any changes that the user makes will only impact their data from that point on. However, if an administrator changes the OWF Users Group, the change will be applied to all users who have access to the group. 

![Default OWF Users Group](OWFImages/OWF7/group_manager_default_users.png)

**Figure: Default OWF Users Group**

<b>OWF Administrators</b> - A default group that ships with OWF. Every new administrator is assigned to this group. 

Data from the OWF Administrators group is automatically applied to the administrator’s profile. Users cannot be assigned to this group and administrators cannot delete the editor and manager widgets populating this group.

> _Note:  The OWF Administrators and OWF Users groups cannot be deleted, renamed or deactivated. In the event that either group is single-selected, the delete button will be grayed out.  If either (or both) groups are selected along with other manual groups, the delete button will be active. However, upon clicking Delete, only the manual groups will be removed from the system._
