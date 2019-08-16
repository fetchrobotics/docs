Getting Started
===============


What's In Box
`````````````

The Fetch and Freight Research Edition robots each ship in reusable ATA
cases. Inside each case you will find the robot, toolkit, and power
supply for charging the robot.


Fetch and Freight
~~~~~~~~~~~~~~~~~

Please watch the video below for unpacking Fetch or Freight. The
video covers unpacking the robot, connecting the batteries, turning on
the robot, and driving the robot via the provided joystick.

.. raw:: html

   <iframe src="https://player.vimeo.com/video/131612734" width="700" height="393"  frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen>
   </iframe>

Toolkit
~~~~~~~

The toolkit contains the tools, accessories, and fasteners needed to
use the Fetch and Freight. The picture below shows packaged toolkit.

.. figure:: _static/toolkit_in_box.png
   :width: 100%
   :align: center
   :figclass: align-centered

Inside the toolkit box you will find:

.. figure:: _static/toolkit_numbering.png
   :width: 100%
   :align: center
   :figclass: align-centered

====== ========================= ======= ===============================================================
Item # Item Name                 QTY     Purpose
====== ========================= ======= ===============================================================
 1     Metric Hex Key Set         1      For removing screws and attaching accessories
 2     Right Angle USB Connector  1      To prevent USB connector damage while driving
 3     Wireless Joystick	  1      For teleoperating the robot
 4     USB Cable		  1 	 For charging the wireless joystick
 5     Finger Tip Covers	  4	 To replace damaged finger tips
 6     M5x10mm SHCS		  4	 For attaching accessories to the base mount points
 7     M4x10mm SHCS		  4	 For attaching accessories to the head mount points
 8     M3x14mm Standoffs          4      For attaching accessories to the gripper
 9     3ft Ethernet Cable         1	 For connecting the robot to the network
 10    Fetch Robotics Stickers    5      For your laptop :)
 11    Mircofiber Lens Cloth      1      For cleaning optics of the robot
====== ========================= ======= ===============================================================


Robot Power Supply
~~~~~~~~~~~~~~~~~~
The robot power supply is shown below in the packaging:

.. figure:: _static/charger.JPG
   :width: 100%
   :align: center
   :figclass: align-centered

The robot plug end is shown below, when removing the charge plug from the
robot **always** grab the plug by the housing and not the cable.

.. figure:: _static/charge_plug.png
   :width: 100%
   :align: center
   :figclass: align-centered

.. warning::

    Pulling on the charge plug cable instead of the handle can cause
    damage to the cable assembly over time and could potentially cause
    injury to the robot or user.


Running Fetch and Freight
`````````````````````````

Turning on Fetch and Freight
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To turn on the robot, set the :ref:`power_disconnect` (the red one
on the lower back of the robot) to the ON position and then press the
power switch on the access panel until it lights up.

Logging In
~~~~~~~~~~

Once the robot is turned on and the robot is on the network, ssh
into the computer of the robot using the default ``fetch`` user
account:

::

	>$ ssh fetch@<robot_name_or_ip>

robot_name_or_ip will be either an IPv4 network address, or a network name, depending
on the configuration of your local network. If your computer
and network is setup for multicast DNS (mDNS) then you may be able to use
``fetchXYZ.local`` as the network name where XYZ will be the serial number
of your robot (remove any leading zeros from the serial number).

Connecting a Monitor (Optional)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
If you are unable to access the robot through ssh due to your network settings
you will need to connect an HDMI monitor, USB keyboard and USB mouse to the
side panel ports. Then use them to select your network from the networking
menu, it looks like an empty quarter circle pointed downward when disconnected,
in the upper right hand corner of the screen. Once it is set it should remain
connected through all reboots.

.. warning::
    Monitor cables that conform to HDMI specifications will fit the robot's
    monitor port. But some cheaper cables have overmolding that is too large
    given the spec and may not seat properly. Please ensure the HDMI cable you
    are using is the correct size.

.. note::

   If you are still having difficulty connecting to your robot you will need
   to contact your network administrator for specific instructions on how
   to connect the robot to your network.


Once connected then create your user account as shown below.

.. include:: computer.rst
   :start-after: embed-user-accounts-start
   :end-before: embed-user-accounts-end

Tucking Fetch's Arm
~~~~~~~~~~~~~~~~~~~

.. note::

   The tuck arm server is a new feature released in
   fetch_teleop and fetch_bringup 0.6.0. The deadman
   became required in fetch_teleop 0.7.0.

To tuck the arm, press and hold button 6, as shown in the image of the
controller below, for one second. This will trigger the tuck_arm server
to tuck the arm. While tucking the arm, Fetch will avoid collisions with
itself, however it will not be using any active perception, so be sure to
keep the space in front of the robot clear when running the tuck arm.
While the arm is tucking, you will have to hold the deadman. Releasing the
deadman will stop the tucking action.

Driving Fetch and Freight with a Joystick
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. include:: teleop.rst
   :start-after: embed-teleop-start
   :end-before: embed-teleop-end

Visualizing Data
~~~~~~~~~~~~~~~~
.. include:: visualization.rst
   :start-after: embed-rviz-start


Putting Fetch and Freight Away
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Before turning the robot off, it is recommended that you tuck the arm.
When power is shut off, the arm will want to slowly fall and will be
more difficult to backdrive when in the off configuration.

To turn the robot off, press and hold the illuminated power button on
the access panel until it starts blinking. The power button will
continue blinking until the computer has successfully shut down, and
then power will be disconnected.
