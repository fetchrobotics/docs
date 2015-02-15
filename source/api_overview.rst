API Overview
============

Fetch Robotics is committed to providing an exceptional out-of-the-box
experience for new robot owners. One of the ways in which we create a great
experience is by using standard ROS interfaces. This means that code you
might have written for other robots in the past should be easily portable
to your new robot.

Whenever possible, we have conformed to the
`ROS Enhancement Proposals (REPs) <http://www.ros.org/reps/rep-0000.html>`_.
These documents provide the foundation of standard ROS interfaces. In addition
to REP-compatible interfaces, we have adopted a number of the community-accepted
standard interfaces, such as those provided by the 
`control_msgs <http://wiki.ros.org/control_msgs>`_ package.

Arm and Torso
-------------
The arm and torso of the robot are controlled by
`control_msgs/FollowJointTrajectory <http://docs.ros.org/api/control_msgs/html/action/FollowJointTrajectory.html>`_
actions. This action interface is the output of packages such as MoveIt, and allows
the arm to execute a pre-defined trajectory. Three interfaces are provided:

 * `arm_controller/follow_joint_trajectory` to control just the seven joints of the arm.
 * `arm_with_torso_controller/follow_joint_trajectory` to control the seven joints of the arm plus the torso.
 * `torso_controller/follow_joint_trajectory` to control just the torso.

Only one controller is allowed to control a joint at a time.

Base Interface
--------------
Support for mobile bases is quite standard and robust in ROS, however it is one
of the older interfaces. As such, it is one of the few interfaces which is not
action-based.

The mobile base subscribes to `base_controller/command`, and accepts a
`geometry_msgs/Twist <http://docs.ros.org/api/geometry_msgs/html/msg/Twist.html>`_
message. Of the fields within the message, only ``linear.x`` and ``angular.z`` are
used, which specify the forward and turning velocities of the robot.

.. todo:: DESCRIBE MULTIPLEXOR

Head Interface
--------------
The head exposes two potential interfaces. The first is an action server available on
`head_controller/follow_joint_trajectory` which follows a joint trajectory as with the
arm and torso (described above).

The second interface is unique to the head, and allows the user to easily point the
head (and head sensors) at a point of interest. This action-based interface is
available on `head_controller/point_head`. It is of type
`control_msgs/PointHead <http://docs.ros.org/api/control_msgs/html/action/PointHead.html>`_.
The interface currently does not support any of the `pointing_axis` or `pointing_frame`
parameters, however it will point the `head_tilt_link` (which is very near the camera optical
axis) towards the `target` point. A min_duration or max_velocity can also be specified.

Gripper Interface
-----------------
`gripper_controller/command` exposes a
`control_msgs/GripperCommand <http://docs.ros.org/api/control_msgs/html/action/GripperCommand.html>`_
action server. The gripper command takes both a position and an effort as input. Generally,
the gripper is commanded to fully closed or fully opened position, and the
effort is used to limit the maximum effort. As the gripper never fully reaches
the closed position, the grasp strength will be entirely set by the maximum
effort.

Head Camera Interface
---------------------
The head camera exposes several topics of interest:

 * `head_camera/depth_registered/points` is a `sensor_msgs/PointCloud2 <http://docs.ros.org/api/sensor_msgs/html/msg/PointCloud2.html>`_
   which has both 3d and color data. It is published at VGA resolution (640x480)
   at 15hz.
 * `head_camera/depth_downsampled/points` is a `sensor_msgs/PointCloud2 <http://docs.ros.org/api/sensor_msgs/html/msg/PointCloud2.html>`_
   which has only 3d data. It is published at QQVGA (160x120) resolution at
   15hz and is intended primarily for use in navigation/moveit for obstacle
   avoidance.
 * `head_camera/rgb/image_raw` is a `sensor_msgs/Image <http://docs.ros.org/api/sensor_msgs/html/msg/Image.html>`_.
   This is just the 2d color data. It is published at VGA resolution (640x480)
   at 15hz.

Laser Interface
---------------
`base_scan` is a `sensor_msgs/LaserScan <http://docs.ros.org/api/sensor_msgs/html/msg/LaserScan.html>`_
message published at 15hz.

IMU Interface
-------------
The IMU is not present in the simulated robot.

.. todo:: DESCRIBE IMU TOPICS ON REAL ROBOT