Release Notes
=============

The following release notes detail the updates to packages available on
http://packages.fetchrobotics.com. For more details on the changes that
have occured in an individual package, please see the CHANGELOG within
the installed package.

For information on updating your robot to the latest packages, see
:ref:`updating`.

November 29, 2016
-----------------
This sync includes new upstream ROS packages. In addition it includes
an updated version of sixad that fixes an issue with logs filling the
disk. It is highly recommended that this is installed through the
following commands:

::

   sudo apt-get update
   sudo apt-get install sixad

Updated drivers improve battery balancing, which should improve battery
life. There are also a number of new features in this release:

 * The chrony time service is now installed by fetch-system-config.
 * fetch_moveit_config now includes an IKFast solver.
 * robot_controllers `adds the ability to dynamically load controllers <https://github.com/fetchrobotics/robot_controllers/pull/23>`__.
 * fetch_bringup includes a :ref:`software runstop feature<software_runstop>` that can turn your PS3 controller into a wireless runstop.

Updated Fetch Packages:

 * fetch-system-config: 0.8-4 -> 0.8-8
 * ros-indigo-fetch-bringup: 0.7.1-0 -> 0.7.3-0
 * ros-indigo-fetch-drivers: 0.7.11-0 -> 0.7.15-0
 * ros-indigo-fetch-depth-layer: 0.7.5-0 -> 0.7.9-0
 * ros-indigo-fetch-description: 0.7.5-0 -> 0.7.9-0
 * ros-indigo-fetch-maps: 0.7.5-0 -> 0.7.9-0
 * ros-indigo-fetch-moveit-config: 0.7.5-0 -> 0.7.9-0
 * ros-indigo-fetch-navigation: 0.7.5-0 -> 0.7.9-0
 * ros-indigo-fetch-teleop: 0.7.5-0 -> 0.7.9-0
 * ros-indigo-freight-bringup: 0.7.1-0 -> 0.7.3-0
 * ros-indigo-robot-controllers: 0.5.0-0 -> 0.5.2-0

A full list of new upstream packages can be found on
`discourse.ros.org <http://discourse.ros.org/t/new-packages-for-indigo-2016-11-27/898>`__

May 28, 2016
------------
This sync includes new upstream ROS packages. Notably this
release includes updates for a udev rule that maps the PS3
controller to /dev/ps3joy, therefore it is important that
you also install the latest fetch-system-config or
freight-system-config package depending on your robot model.
The :ref:`updating` instructions have been updated to note that
the correct update command is now:

::

   sudo apt-get update
   sudo apt-get install --only-upgrade ros-indigo-* f.*-system-config
   sudo service robot stop
   sudo service robot start

New drivers improve charge time and performance.
A number of improvements have been made to the fetch_depth_layer
including properly supporting deactivate/activate when plans
are not in progress.

Updated Fetch Packages:
 * fetch-system-config: 0.8-0 -> 0.8-4
 * ros-indigo-fetch-bringup: 0.6.0-0 -> 0.7.1-0
 * ros-indigo-fetch-drivers: 0.7.4-0 -> 0.7.11-0
 * ros-indigo-fetch-depth-layer: 0.7.0-0 -> 0.7.5-0
 * ros-indigo-fetch-description: 0.7.0-0 -> 0.7.5-0
 * ros-indigo-fetch-gazebo: 0.7.0-0 -> 0.7.1-0
 * ros-indigo-fetch-gazebo-demo: 0.7.0-0 -> 0.7.1-0
 * ros-indigo-fetch-maps: 0.7.0-0 -> 0.7.5-0
 * ros-indigo-fetch-moveit-config: 0.7.0-0 -> 0.7.5-0
 * ros-indigo-fetch-navigation: 0.7.0-0 -> 0.7.5-0
 * ros-indigo-fetch-teleop: 0.7.0-0 -> 0.7.5-0
 * ros-indigo-freight-bringup: 0.6.0-0 -> 0.7.1-0
 * ros-indigo-robot-controllers: 0.4.3-0 -> 0.5.0-0

A full list of new upstream packages can be found on the
`ROS mailing list <http://lists.ros.org/pipermail/ros-users/2016-May/070011.html>`__

January 21, 2016
----------------
This sync includes new upstream ROS packages. New drivers
include improvements to charge state estimation and a
tool for :ref:`in-field calibration of the torso<torso_calibration>`.
Auto docking includes several fixes for TF-related errors,
as well as a fix for reliability when the odom frame and dock
are aligned.

Updated Fetch Packages:
 * ros-indigo-fetch-drivers: 0.7.3-0 -> 0.7.4-0
 * ros-indigo-fetch-auto-dock: 0.1.0-0 -> 0.2.1-0

A full list of new upstream packages can be found on the
`ROS mailing list <http://lists.ros.org/pipermail/ros-users/2016-January/069795.html>`__

November 23, 2015
-----------------
This sync includes new upstream ROS packages as well
as minor bug fixes and improvements to drivers. Notably,
the deadman must now be held while tucking the arm, this
allows a user to stop the arm tucking should the robot
collide with an obstacle in the environment.

Of note, this release also fixes several inconsistencies
in the wrist_flex range of the robot. If your robot appears
to have an overly limited wrist_flex range, we recommend
recalibrating the robot from a clean URDF after updating
your packages.

Maps have been removed from the fetch_navigation package and
moved to their own package, fetch_maps.

Updated Fetch Packages:
 * ros-indigo-fetch-drivers: 0.7.1-0 -> 0.7.3-0
 * ros-indigo-fetch-depth-layer: 0.6.2-0 -> 0.7.0-0
 * ros-indigo-fetch-description: 0.6.2-0 -> 0.7.0-0
 * ros-indigo-fetch-gazebo: 0.6.2-0 -> 0.7.0-0
 * ros-indigo-fetch-gazebo-demo: 0.6.2-0 -> 0.7.0-0
 * ros-indigo-fetch-moveit-config: 0.6.2-0 -> 0.7.0-0
 * ros-indigo-fetch-navigation: 0.6.2-0 -> 0.7.0-0
 * ros-indigo-fetch-teleop: 0.6.2-0 -> 0.7.0-0

New Fetch Packages:
 * ros-indigo-fetch-maps: 0.7.0-0

A full list of new upstream packages can be found on the
`ROS mailing list <http://lists.ros.org/pipermail/ros-users/2015-November/069765.html>`__

November 12, 2015
-----------------
This sync includes new upstream ROS packages as well as
the first release of auto docking.

Please note that the MD5 checksum for the dock action
will have changed with this release.

Updated Fetch Packages:
 * ros-indigo-fetch-drivers: 0.6.3-0 -> 0.7.1-0
 * ros-indigo-fetch-auto-dock-msgs: 0.5.2-0 -> 0.6.0-0
 * ros-indigo-fetch-driver-msgs: 0.5.2-0 -> 0.6.0-0
 * ros-indigo-fetch-gazebo: 0.6.1-0 -> 0.6.2-0
 * ros-indigo-fetch-gazebo-demo: 0.6.1-0 -> 0.6.2-0

New Fetch Packages:
 * ros-indigo-fetch-auto-dock: 0.1.0

A full list of new upstream packages can be found on the
`ROS mailing list <http://lists.ros.org/pipermail/ros-users/2015-September/069629.html>`__

August 5, 2015
--------------
This sync includes new upstream ROS packages as well
as minor fixes to the URDF and calibration.

Updated Fetch Packages:
 * ros-indigo-fetch-drivers: 0.6.1-0 -> 0.6.3-0
 * ros-indigo-fetch-depth-layer: 0.6.1-0 -> 0.6.2-0
 * ros-indigo-fetch-description: 0.6.1-0 -> 0.6.2-0
 * ros-indigo-fetch-moveit-config: 0.6.1-0 -> 0.6.2-0
 * ros-indigo-fetch-navigation: 0.6.1-0 -> 0.6.2-0
 * ros-indigo-fetch-teleop: 0.6.1-0 -> 0.6.2-0

A full list of new upstream packages can be found on the
`ROS mailing list <http://lists.ros.org/pipermail/ros-users/2015-August/069564.html>`__

July 9, 2015
------------
This sync includes new upstream ROS packages as well as
tuck arm functionality from the robot joystick. This
release also includes charge level estimates for
Fetch and Freight robots.

Updated Fetch Packages:
 * ros-indigo-fetch-drivers: 0.5.3-0 -> 0.6.1-0
 * ros-indigo-fetch-depth-layer: 0.5.13-0 -> 0.6.1-0
 * ros-indigo-fetch-description: 0.5.13-0 -> 0.6.1-0
 * ros-indigo-fetch-driver-msgs: 0.5.1-0 -> 0.5.2-0
 * ros-indigo-fetch-gazebo: 0.5.0-0 -> 0.6.1-0
 * ros-indigo-fetch-gazebo-demo: 0.5.0-0 -> 0.6.1-0
 * ros-indigo-fetch-moveit-config: 0.5.13-0 -> 0.6.1-0
 * ros-indigo-fetch-navigation: 0.5.13-0 -> 0.6.1-0
 * ros-indigo-fetch-teleop: 0.5.13-0 -> 0.6.1-0
 * ros-indigo-robot-calibration: 0.4.0-0 -> 0.5.2-0
 * ros-indigo-robot-calibration-msgs: 0.4.0-0 -> 0.5.2-0

New Fetch Packages:
 * ros-indigo-fetch-auto-dock-msgs: 0.5.2-0

A full list of new upstream packages can be found on the
`ROS mailing list <http://lists.ros.org/pipermail/ros-users/2015-July/069516.html>`__

June 8, 2015
------------
First publicly available release.

New Fetch Packages:
 * ros-indigo-fetch-drivers: 0.5.3-0
 * ros-indigo-fetch-depth-layer: 0.5.13-0
 * ros-indigo-fetch-description: 0.5.13-0
 * ros-indigo-fetch-driver-msgs: 0.5.1-0
 * ros-indigo-fetch-gazebo: 0.5.0-0
 * ros-indigo-fetch-gazebo-demo: 0.5.0-0
 * ros-indigo-fetch-moveit-config: 0.5.13-0
 * ros-indigo-fetch-navigation: 0.5.13-0
 * ros-indigo-fetch-teleop: 0.5.13-0

A full list of new upstream packages can be found on the
`ROS mailing list <http://lists.ros.org/pipermail/ros-users/2015-June/069467.html>`__
