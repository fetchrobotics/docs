Computer Overview and Configuration
-----------------------------------
Both Fetch and Freight have an internal computer

BIOS
++++

Networking 
++++++++++ 

The majority of communication between components onboard the Fetch &
Freight happens via an onboard ethernet network, referred to as the
"robot internal network". This internal network can be accessed
indirectly via the internal computer via either wired connection
(through the access panel), or wireless connection.

The 10.42.42.0 subnet is the primary network used internally by the
computer on the robot. Additionally many of the ethernet-based
devices, such as the mainboard board, gripper, and laser, are given
addresses on this subnet.

Home Directories
++++++++++++++++

Storage
+++++++

Formatting Drives
+++++++++++++++++

Drive Maintenance
+++++++++++++++++

Clock Synchronization
+++++++++++++++++++++

udev
++++

Upstart Jobs
++++++++++++
