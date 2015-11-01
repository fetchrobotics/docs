Tutorial: Manipulation
======================

Once you have Fetch running, you can start moving the arm with MoveIt!

Getting Started
---------------

The easiest way to run MoveIt! is to run the demo launch file,
which does not require any simulator or robot and brings up a
fully configured RVIZ instance:

::

    >$ roslaunch fetch_moveit_config demo.launch

Within this demo you can use the sliders of the joint state
publisher window to move the joints to new starting positions
and use interactive markers to create new locations to plan
to and from.

Running MoveIt!
---------------

To run MoveIt! on a real or simulated robot, launch the
move_group.launch file from the ``fetch_moveit_config`` package:

::

	>$ roslaunch fetch_moveit_config move_group.launch

Running the Pick and Place Demo
-------------------------------

See :ref:`mm_demo`.


More information and Tutorials on MoveIt!
-------------------------------

`General information, Documentation<http://moveit.ros.org/documentation/>`_ and `Tutorials
<http://moveit.ros.org/documentation/tutorials/>`_ available at moveit.ros.org

