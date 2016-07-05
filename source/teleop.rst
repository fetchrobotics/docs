Tutorial: Robot Teleop
======================

Using the Robot Joystick
------------------------
.. embed-pt

Each Fetch and Freight ship with a robot joystick.
Whenever the robot drivers are running, so is joystick teleop.
The joystick is capable of controlling the movement of the robot
base, torso, head and gripper.

.. figure:: _static/joystick_numbered.png
   :width: 100%
   :align: center
   :figclass: align-centered

.. figure:: _static/joystick_numbered2.png
   :width: 100%
   :align: center
   :figclass: align-centered

======== =================================
Button # Function (details below)
======== =================================
 0       Open gripper
 1       Control robot turning
 2       Control forward/backward driving
 3       Close gripper
 4       Disable motor position holding
 5       Not used
 6       Arm tuck
 7       Not used
 8       Head control deadman
 9       Not used
 10      Primary deadman
 11      Not used
 12      Torso up
 13      Not used
 14      Torso down
 15      Not used
 16      Pair/unpair with robot
======== =================================

To pair the controller with the robot, press the middle button (16) once
the robot has powered on.  The controller will vibrate once successful.
To unpair, hold the button for 10 s.  The LED indicator on top will turn off.

To drive the robot base, hold the primary deadman button (button 10
above) and use the two joysticks. The left joystick controls turning
velocity while the right joystick controls forward velocity.

.. warning::

    Whenever driving the robot, always lower the torso and tuck
    the arm to avoid potentially unstable operation.

To control the head, release the primary deadman and hold the head
deadman (button 8). The left joystick now controls head pan while the right
joystick controls head tilt.

To move the torso up, hold the primary deadman and press the triangle
button (12). To move the torso down, hold the primary deadman and press
the X (14).

To close the gripper, hold the primary deadman and press the close
button (3). To open, hold the primary deadman and press the open
button (0).

Some controllers, such as the arm and head controllers, will attempt to
hold position indefinitely. Sometimes this is not desired. Holding button (4)
for 1 second will stop all controllers except the base controller and
the arm gravity compensation.

Moving the Base with your Keyboard
----------------------------------

.. note::

   You will need a computer with ROS installed to properly
   communicate with the robot. Please consult the `ROS Wiki <http://wiki.ros.org/indigo/Installation>`_
   for more information. We strongly suggest an Ubuntu machine
   with ROS Indigo installed.

To teleoperate the robot base in simulation, we recommend
using the ``teleop_twist_keyboard.py`` script from
`teleop_twist_keyboard <http://wiki.ros.org/teleop_twist_keyboard>`_
package.

::

  >$ export ROS_MASTER_URI=http://<robot_name_or_ip>:11311
  >$ rosrun teleop_twist_keyboard teleop_twist_keyboard.py


Software Runstop
----------------

In addition to the runstop button on the side of the robot, similar software
functionality is also available, allowing for button presses on the
PS3 controller or a program to disable the breakers.
This functionality is available in release 0.7.3 of the
fetch_bringup package. The teleop portion is disabled by default.

Using Software Runstop
~~~~~~~~~~~~~~~~~~~~~~

To activate the software runstop, publish True to the /enable_software_runstop
topic.

Alternately, with the teleop runstop enabled, pressing both of the right
trigger buttons (buttons 9 and 11) will activate the software runstop.
The software_runstop.py script in fetch_bringup can be modified to change
the button(s) for the software runstop.

Once activated, the software runstop can be deactivated by (1) toggling the
hardware runstop, or (2) disabling the software runstop by passing False to
the /enable_software_runstop topic.

Enable Teleop Software Runstop
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note::

   In order to edit the robot.launch file, you will
   need to use a terminal editor (such as nano or vim), or use the -X flag
   with SSH to use a graphical editor (such as gedit). Additionally, the editor
   must be launched with `sudo`. Instructions below use nano.

To enable the software runstop, first SSH into the robot, and then
modify the robot drivers launch file to use it.

We need to modify the robot.launch file to pass the correct arg to the
software runstop script:

::

  >$ sudo nano /etc/ros/indigo/robot.launch

In this file there should be a Software Runstop entry near the end. By default
this entry contains an args line, with a value of "-a -b -g". To add teleop
control, add the "-t" flag as well. This section will then look like the below.
If your robot is an older one and does not have a Software Runstop entry,
you will want to simply copy the block the below.

::

  <!-- Software Runstop -->                                                     
  <include file="$(find fetch_bringup)/launch/include/runstop.launch.xml">
    <arg name="flags" value="-a -b -g -t" />
  </include>

Note that the -a, -b, -g flags correspond to letting the software runstop
control the :ref:`arm, base and gripper breakers<breakers>`,
respectively.

Additionally, if completely disabling the software runstop functionality is
desired, the above section in robot.launch can be commented out or removed.

Finally, restart the drivers so that our changes take effect:

::

  >$ sudo service robot stop && sudo service robot stop
