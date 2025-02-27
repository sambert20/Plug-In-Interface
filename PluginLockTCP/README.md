Lock TCP Plug-in for RoboDK
===========================

This example shows how to lock the TCP pose for a 6 axis robot mounted on a synchronized external axis.

This example adds a "Lock TCP" checkable menu item when right-clicking on a Tool.

![Lock TCP menu](./doc/menu.PNG)

Behaviour
---------

Locking the TCP will allow the external axis to move the robot base while keeping the tool position. New pose in limit cases, such as new joints configuration or robot fully extended, will be rejected.


|                                      |                                      |
| ------------------------------------ | ------------------------------------ |
| ![Locked pose 1](./doc/locked_1.PNG) | ![Locked pose 2](./doc/locked_2.PNG) |


Run from API
-------------

Here's a sample code to use this plugin through the API.

```
from robolink import ITEM_TYPE_TOOL, Robolink

RDK = Robolink()

item = RDK.ItemUserPick("Select TCP to lock", ITEM_TYPE_TOOL)
if not item.Valid():
    quit()

if RDK.PluginCommand("Lock TCP", "LOCK", item.Name()) != "OK":
    RDK.ShowMessage('Failed to lock TCP of %s. Ensure the plugin is enabled (Shift+I)' % item.Name())
    quit()
RDK.ShowMessage('Locked TCP of %s' % item.Name())

# Try it out!

if RDK.PluginCommand("Lock TCP", "UNLOCK", item.Name()) != "OK":
    RDK.ShowMessage('Failed to unlock TCP of %s' % item.Name())
RDK.ShowMessage('Unlocked TCP of %s' % item.Name())
```