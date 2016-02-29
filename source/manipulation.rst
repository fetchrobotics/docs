Tutorial: Manipulation
======================

Once you have Fetch running, you can start moving the arm with MoveIt!

Getting Started Demo
--------------------

The easiest way to run MoveIt! is to run the demo launch file,
which does not require any simulator or robot and brings up a
fully configured RVIZ instance:

::

    >$ roslaunch fetch_moveit_config demo.launch

Within this demo you can use the sliders of the joint state
publisher window to move the joints to new starting positions
and use interactive markers to create new locations to plan
to and from.

Running the Pick and Place Demo
-------------------------------

See :ref:`mm_demo`.

Running MoveIt! on a Robot
-----------------------------

To run MoveIt! on a real or simulated robot, launch the
move_group.launch file from the ``fetch_moveit_config`` package:

::

  >$ roslaunch fetch_moveit_config move_group.launch

Once launched you can send commands to move the arm using
the `MoveIt! Rviz Plugin <http://docs.ros.org/indigo/api/moveit_ros_visualization/html/doc/tutorial.html>`_ or use the programming interface, ``move_group_interface``, in either `C++ <http://docs.ros.org/indigo/api/pr2_moveit_tutorials/html/planning/src/doc/move_group_interface_tutorial.html>`_ or `Python <http://docs.ros.org/indigo/api/pr2_moveit_tutorials/html/planning/scripts/doc/move_group_python_interface_tutorial.html>`_.


More information and Tutorials on MoveIt!
-----------------------------------------

`General information <http://moveit.ros.org/>`_, `Documentation <http://moveit.ros.org/documentation/>`_ and `Tutorials <http://moveit.ros.org/documentation/tutorials/>`_ available at moveit.ros.org

