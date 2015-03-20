Tutorial: Perception
====================

Head Camera Topics
------------------

The API for the head camera is documented under :ref:`camera_api`.

Some resources for accessing and processing camera data are:

 * `OpenCV <http://opencv.org/>`_ is a generic computer vision library
   which has good support within ROS.
 * `Point Cloud Library <http://pointclouds.org/>`_ allows manipulation
   of 3-dimensional images, or point clouds.
 * `cv_bridge <http://wiki.ros.org/cv_bridge>`_ is a ROS package that allows
   converting ROS image messages into OpenCV data structures in C++ or Python.
 * `pcl_conversions <http://wiki.ros.org/pcl_conversions>`_ is a ROS
   package for converting between ROS PointCloud2 messages and PCL data
   types in C++.
 * `pcl_ros <http://wiki.ros.org/pcl_ros>`_ is a ROS package that contains
   several nodelets for commonly used PCL components such as voxel grid
   filters for downsampling a point cloud or pass through filters for
   filtering out data beyond a certain distance.

Running the Pick and Place Demo
-------------------------------

See :ref:`mm_demo`.
