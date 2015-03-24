Introduction
============

This documentation shows how to use the Fetch simulator preview. It
also provides some basic tutorials on using the robot. Please also
refer to the documentation at http://wiki.ros.org

Installation
------------
At this time, the preview repository is only available from source. We
recommend using a standard installation of
`ROS Indigo on Ubuntu 14.04 <http://wiki.ros.org/indigo/Installation/Ubuntu>`_.

Once you have installed ROS, the following set of commands will create
a new ROS workspace with just the preview repository inside, and then
install the remaining dependencies from debian packages:

::

   mkdir ~/catkin_ws/src
   cd ~/catkin_ws/src
   git clone https://github.com/fetchrobotics/preview.git
   git clone https://github.com/mikeferguson/moveit_planners.git
   cd ~/catkin_ws
   source /opt/ros/indigo/setup.bash
   rosdep install --from-paths src --ignore-src --rosdistro indigo -y
   catkin_make

Note: the above instructions currently build moveit_planners from source,
while this is not required, it is highly recommended until certain patches
are moved upstream to fix extremely long planning times with OMPL. We also
recommend making sure your gazebo_ros_pkgs and rviz installs are up to date
as we have recently patched some issues with both:

::

    sudo apt-get update
    sudo apt-get install ros-indigo-rviz ros-indigo-gazebo-plugins
