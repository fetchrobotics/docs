Tutorial: Robot Teleop
======================

Starting the Teleop
-------------------
To use the teleop, launch the gazebo simulation using the steps in the :doc:`previous tutorial</gazebo>`.

The keyboard teleop is launched from the ``fetch_gazebo`` package:

::

	>$ rosrun fetch_gazebo teleop_freight.py

A prompt similar to the one below will appear and your keyboard will now operate the robot.
::
	Reading from the keyboard  and Publishing to Twist!
	---------------------------
	Moving around:
	   u    i    o
	   j    k    l
	   m    ,    .

	q/z : increase/decrease max speeds by 10%
	w/x : increase/decrease only linear speed by 10%
	e/c : increase/decrease only angular speed by 10%
	anything else : stop

	CTRL-C to quit

.. todo:: JOYSTICK TELEOP
