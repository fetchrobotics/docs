Getting Started
===============


What's In Box 
`````````````

The Fetch & Freight Research Edition robots each ship in reuseable ATA
cases. Inside each case you will find the robot, toolkit, and power
supply for charging the robot.


Fetch & Freight
~~~~~~~~~~~~~~~

Please watch the respective video for unpacking Fetch or Frieght. The
video covers unpacking the robot, connecting the batteries, turning on
the robot, and driving the robot via the provided joystick.

.. TODO:: PIC of robot in box

Toolkit
~~~~~~~

.. TODO:: PIC of kit

* Wireless Joystick 

* Hardware & Tools

* Finger Tip Covers

* Ethernet Cable

Robot Power Supply 
~~~~~~~~~~~~~~~~~~

.. TODO:: PIC of power supply


Running Fetch & Freight
```````````````````````

Turning on Fetch & Freight
~~~~~~~~~~~~~~~~~~~~~~~~~~

To turn on the robot, set the main power disconnect switch (the red one
on the lower back of the robot) to the ON position and then press the
power switch on the access panel until it lights up.

Logging In 
~~~~~~~~~~ 

Once the robot is turned on, ssh into the computer of the robot using
the default ``fetch`` user account:

:: 

	>$ ssh fetch@ROBOT_IP

ROBOT_IP will be either an IPv4 network address, or a network name, depending
on the configuration of your local network. If your computer
and network is setup for multicast DNS (mDNS) then you may be able to use
``fetchXYZ.local`` as the network name where XYZ will be the serial number
of your robot (remove any leading zeros from the serial number).

Then create your user account if you have not already done so as shown
below.

.. include:: computer.rst
   :start-after: embed-user-accounts-start
   :end-before: embed-user-accounts-end


Tucking Fetch's Arm
~~~~~~~~~~~~~~~~~~~

.. TODO:: add notes on tucking the arm

Driving Fetch & Freight with a Joystick
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. include:: teleop.rst
    :start-after: embed-pt

Visualizing Data
~~~~~~~~~~~~~~~~
.. include:: visualization.rst
   :start-after: embed-rviz-start

Putting Fetch & Freight Away
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Before turning the robot off, it is recommended that you tuck the arm.
When power is shut off, the arm will want to slowly fall and will be
more difficult to backdrive when in the off configuration.

To turn the robot off, press and hold the switch on the access panel
until it starts blinking. The switch will continue blinking until the
computer has successfully shut down, and then power will be disconnected.
