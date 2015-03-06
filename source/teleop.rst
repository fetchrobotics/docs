Tutorial: Robot Teleop
======================

Starting the Teleop
-------------------
The keyboard teleop uses ``teleop_twist_keyboard.py`` from `teleop_twist_keyboard <http://wiki.ros.org/teleop_twist_keyboard>`_.

It can be launched by running the script and remapping ``cmd_vel`` to ``base_controller/command``:
::

	>$ rosrun teleop_twist_keyboard teleop_twist_keyboard.py cmd_vel:=base_controller/command




.. todo:: JOYSTICK TELEOP
