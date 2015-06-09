Tutorial: Robot Teleop
======================

Using the Robot Joystick
------------------------
.. embed-pt
Each Fetch and Freight ship with a robot joystick.
Whenever the robot drivers are running, so is joystick teleop.
The joystick is capable of controlling the movement of the robot
base, torso, head and gripper.

.. TODO:: add image of joystick (http://wiki.ros.org/ps3joy)

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
hold position indefintely. Sometimes this is not desired. Holding button (4)
for 1 second will stop all controllers except the base controller and
the arm gravity compensation.

Moving the Base with your Keyboard
----------------------------------

To teleoperate the robot base in simulation, we recommend
using the ``teleop_twist_keyboard.py`` script from
`teleop_twist_keyboard <http://wiki.ros.org/teleop_twist_keyboard>`_
package.

::

	>$ rosrun teleop_twist_keyboard teleop_twist_keyboard.py
