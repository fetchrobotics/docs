Tutorial: Navigation
====================

Once you have :doc:`Fetch running in Gazebo </gazebo>`, you can
start navigating.

Running Navigation
------------------

To run navigation, launch the navigation launch file from the
``fetch_navigation`` package:

::

	>$ roslaunch fetch_navigation navigate.launch


Building A Map
--------------

The navigation file above uses a pre-built map of the environment.
That map was created by running:

::

    >$ roslaunch fetch_navigation build_map.launch

Note that this should be run at the same time as the navigate.launch
file. Once you launch build_map, you will want to
:doc:`tele-operate the robot </teleop>` the robot around and build
the map, which can be visualized in RVIZ.

Once you are happy with the map, you can save the map:

::

    >$ rosrun map_server map_saver -f <map_directory/map_name>

The map saver will create two files in the specified
``map_directory``. The directory must already exist if it doesn't,
just run ``mkdir map_directory``. The two files are map_name.pgm and
map_name.yaml. The first is the map in a ``.pgm`` image format, and
the second is a YAML file that specifies metadata for the image. These
files can then be served by the map_server:

::

    >$ rosrun map_server map_server <map.yaml>

The navigation.launch file used above launches an instance of map_server.
To change the map that it uses, either edit the launch file, or pass
the filename in as a parameter:

::

    >$ roslaunch fetch_navigation navigate.launch map_file:=/path/to/map.yaml


Sending Waypoints
-----------------

The easiest way to send a goal to the navigation stack is using RVIZ and the
``2D Nav Goal`` button. See the tutorial on using RVIZ with navigation in the RVIZ
`documentation <http://wiki.ros.org/navigation/Tutorials/Using%20rviz%20with%20the%20Navigation%20Stack>`_

However, you probably want to program your robot. There is a
`tutorial <http://wiki.ros.org/navigation/Tutorials/SendingSimpleGoals>`_
on commanding the robot with C++. For examples in Python, look at the demo.py
code in the ``fetch_gazebo`` package.

