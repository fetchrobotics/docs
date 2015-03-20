Tutorial: Robot Teleop
======================

Moving the Base with your Keyboard
----------------------------------

To teleoperate the robot base, we recommend using the ``teleop_twist_keyboard.py``
script from `teleop_twist_keyboard <http://wiki.ros.org/teleop_twist_keyboard>`_
package.

By default this script outputs to a topic called ``cmd_vel``, but you will want
to remap this to ``base_controller/command``:

::

	>$ rosrun teleop_twist_keyboard teleop_twist_keyboard.py cmd_vel:=base_controller/command

.. todo:: JOYSTICK TELEOP
