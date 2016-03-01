Tutorial: Navigation
====================

Once you have Fetch or Freight running, you can start navigating.
Fetch and Freight ship with configurations for using the
ROS Navigation Stack. A number of tutorials related to navigation
can be found in the documentation on the
`ROS Wiki <http://wiki.ros.org/navigation>`_.

Running Navigation in Gazebo Simulation
---------------------------------------

To run navigation in simulation, launch the navigation launch file
from the ``fetch_gazebo_demo`` package:

::

	>$ roslaunch fetch_gazebo_demo fetch_nav.launch

Running Navigation on a Real Robot
----------------------------------

When running navigation on a robot, first you will need to build a map,
See the next section for a how-to. Then you will need to supply the map
to the navigation launch file from the ``fetch_navigation`` package:

::

    >$ roslaunch fetch_navigation fetch_nav.launch map_file:=/path/to/map.yaml


Building A Map
--------------

The launch file for navigation in Gazebo depends on a pre-built
map of the environment. In order to use navigation in the real world,
you will need to first build a map of your environment:

::

    >$ roslaunch fetch_navigation build_map.launch

Once you launch build_map, you will want to
:doc:`tele-operate the robot </teleop>` the robot around and build
the map, which can be visualized in RVIZ.

.. note:: The build_map.launch file is not intended to be run at the same time
    as fetch_nav.launch

While driving the robot around, you can view the map in RVIZ.
Once you are happy with the map, you can save the map:

::

    >$ rosrun map_server map_saver -f <map_directory/map_name>

The map saver will create two files in the specified
``map_directory``. The directory must already exist.
The two files are map_name.pgm and map_name.yaml.
The first is the map in a ``.pgm`` image format, and
the second is a YAML file that specifies metadata for the image.
These files can then be served by the map_server:

::

    >$ rosrun map_server map_server <map.yaml>

The fetch_nav.launch file used above launches an instance of map_server. It
has three arguments which control the behavior:

================= ================================
Argument          Meaning
================= ================================
map_file          YAML file containing map metadata
map_keepout_file  Additional YAML file containing metadata for a keepout map
use_keepout       Whether to load and use a keepout map (default: False)
================= ================================

You can either pass the arguments from the command line, like:

::

    >$ roslaunch fetch_navigation fetch_nav.launch map_file:=/path/to/map.yaml

Or create a new launch file in your own package which includes launch
file and passes in arguments:

::

    <launch>
      <include file="$(find fetch_navigation)/launch/fetch_nav.launch" >
        <arg name="map_file" value="$(find my_package)/maps/my_map.yaml" />
        <arg name="map_keepout_file" value="$(find my_package)/maps/my_keepout_map.yaml" />
        <arg name="use_keepout" value="true" />
      </include>
    </launch>

The "keepout" map can be created by copying the YAML file of your saved map,
editing the name of the ``.pgm`` file and then copying the ``.pgm`` file.
You can then open the ``.pgm`` file in an image editor, such as GIMP, and
black out areas that you do not want the robot to drive through. This must be
done in a separate map that is only used for planning so that the edits do
not disturb the functionality of localization (AMCL).

Sending Waypoints
-----------------

The easiest way to send a goal to the navigation stack is using RVIZ and the
``2D Nav Goal`` button. See the tutorial on using RVIZ with navigation in the RVIZ
`documentation <http://wiki.ros.org/navigation/Tutorials/Using%20rviz%20with%20the%20Navigation%20Stack>`_

However, you probably want to program your robot. There is a
`tutorial <http://wiki.ros.org/navigation/Tutorials/SendingSimpleGoals>`_
on commanding the robot with C++. For examples in Python, look at the demo.py
code in the ``fetch_gazebo_demo`` package.
