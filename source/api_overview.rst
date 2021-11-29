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

.. _arm_api:

Arm and Torso
-------------
The arm and torso of the robot are controlled by
`control_msgs/FollowJointTrajectory <http://docs.ros.org/api/control_msgs/html/action/FollowJointTrajectory.html>`_
actions. This `action interface <http://wiki.ros.org/actionlib/DetailedDescription#Action_Interface_.26_Transport_Layer>`_ is the output of packages such as MoveIt, and allows
the arm to execute a pre-defined trajectory. Three interfaces are provided:

 * `arm_controller/follow_joint_trajectory` to control just the seven joints of the arm.
 * `arm_with_torso_controller/follow_joint_trajectory` to control the seven joints of the arm plus the torso.
 * `torso_controller/follow_joint_trajectory` to control just the torso.

Only one controller is allowed to control a joint at a time.

.. warning::

    Fetch is tuned to work with smooth paths. The tuning performs best when paths are
    properly smoothed and timed, such as those generated from MoveIt Fetch has a number
    of mechanisms in place to prevent damage from improper trajectories. Improperly
    constructed paths may cause motor or breaker shutdown.

In addition to the trajectory controllers, the arm is always running a gravity
compensation controller.

.. _base_api:

Base Interface
--------------
Support for mobile bases is quite standard and robust in ROS, however it is one
of the older interfaces. As such, it is one of the few interfaces which is not
action-based.

The mobile base subscribes to `base_controller/command`, and accepts a
`geometry_msgs/Twist <http://docs.ros.org/api/geometry_msgs/html/msg/Twist.html>`_
message.

Only two fields are used in the message:

 * ``linear.x`` specifies the robot's forward velocity
 * ``angular.z`` specifies the robot's turning velocity

User applications will typically not connect directly to `base_controller/command`,
but rather to `cmd_vel`. A multiplexer is always running between `cmd_vel/teleop`
and `cmd_vel`. Whenever the deadman on the robot controller is held, `cmd_vel/teleop`
will override `cmd_vel`. The advantage of having your application publish to `cmd_vel`
rather than directly to `base_controller/command` is that you can override bad
commands by simply pressing the deadman on the robot controller.

The base controller implements a speed reduction when in the proximity of
obstacles. This will not entirely stop the robot if it is about to hit something,
but will prevent full speed collisions.

.. _head_api:

Head Interface
--------------
The head exposes two potential interfaces. The first is an `ActionServer <http://wiki.ros.org/actionlib#Client-Server_Interaction>`_
available on `head_controller/follow_joint_trajectory` which follows a joint trajectory as with the
arm and torso (described above).

The second interface is unique to the head, and allows the user to easily point the
head (and head sensors) at a point of interest. This action-based interface is
available on `head_controller/point_head`. It is of type
`control_msgs/PointHead <http://docs.ros.org/api/control_msgs/html/action/PointHead.html>`_.
Although the interface currently does not support any of the ``pointing_axis`` or ``pointing_frame``
fields, it points the `head_tilt_link` (which is very near the camera optical
axis) towards the `target` point to achieve a similar effect. A ``min_duration`` or ``max_velocity`` can also be specified.

.. _gripper_api:

Gripper Interface
-----------------
`gripper_controller/gripper_action` exposes a
`control_msgs/GripperCommand <http://docs.ros.org/api/control_msgs/html/action/GripperCommand.html>`_
ActionServer. The gripper command takes in ``position`` and ``effort`` as parameters. Generally,
the gripper is commanded to a fully closed or fully opened position, so
``effort`` is used to limit the maximum effort. As the gripper never fully reaches
the closed position, the grasp strength will be determined by the maximum
effort.

.. _camera_api:

Head Camera Interface
---------------------
The head camera exposes several topics of interest:

 * `head_camera/depth_registered/points` is a `sensor_msgs/PointCloud2 <http://docs.ros.org/api/sensor_msgs/html/msg/PointCloud2.html>`_
   which has both 3d and color data. It is published at VGA resolution (640x480)
   at 15Hz.
 * `head_camera/depth_downsampled/points` is a `sensor_msgs/PointCloud2 <http://docs.ros.org/api/sensor_msgs/html/msg/PointCloud2.html>`_
   which has only 3d data. It is published at QQVGA (160x120) resolution at
   15Hz and is intended primarily for use in navigation/moveit for obstacle
   avoidance.
 * `head_camera/depth/image_raw` is a `sensor_msgs/Image <http://docs.ros.org/api/sensor_msgs/html/msg/Image.html>`_.
   This is unit16 depth image (2D) in mm . It is published at VGA resolution (640x480)
   at 15Hz.
 * `head_camera/depth/image` is a `sensor_msgs/Image <http://docs.ros.org/api/sensor_msgs/html/msg/Image.html>`_.
   This is float depth image (2D) in m. It is published at VGA resolution (640x480)
   at 15Hz.
 * `head_camera/rgb/image_raw` is a `sensor_msgs/Image <http://docs.ros.org/api/sensor_msgs/html/msg/Image.html>`_.
   This is just the 2d color data. It is published at VGA resolution (640x480)
   at 15Hz.

.. _laser_api:

Laser Interface
---------------

`base_scan` is a `sensor_msgs/LaserScan <http://docs.ros.org/api/sensor_msgs/html/msg/LaserScan.html>`_
message published at 15Hz.

Note: the raw laser information as reported by the laser hardware is published to
`base_scan_raw`. The information published to `base_scan` is filtered to remove
shadow points.

.. _imu_api:

IMU Interface
-------------

`imu` is a `sensor_msgs/Imu <http://docs.ros.org/api/sensor_msgs/html/msg/Imu.html>`_
message published at 100Hz. This message contains the linear acceleration and
rotational velocities as measured by the IMU located in the base of the robot.

On Fetch robots, the gripper IMU publishes to `gripper_imu`. This is also
a `sensor_msgs/Imu <http://docs.ros.org/api/sensor_msgs/html/msg/Imu.html>`_
message published at 100Hz.

The IMUs are not present in the simulated robot.

.. _resetting_breakers:

Resetting Breakers
------------------

There are 3 breakers governing power on the fetch. One each for the arm, gripper
and base. The aux1 and aux2 breakers power the arm and gripper, respectively.
On the freight research base, aux1_breaker is connected to the aux power connector on
the robot's top right. On newer freight research bases with a second aux power
connector on the robot's top left, this power is controlled by the aux2 breaker.
(Note: previously with ROS Indigo, aux1 and aux2 breakers were named 'arm' and 'gripper')

To query the current state of the breakers, you can inspect the output of the command
``rosrun fetch_drivers read_board 0``.

If the motors are commanded to perform beyond their limits they will
shut down for safety. To reset them you will either need to toggle the e-stop or
use the following service calls:

 * $ rosservice call /base_breaker false && rosservice call /base_breaker true
 * $ rosservice call /aux1_breaker false && rosservice call /aux1_breaker true
 * $ rosservice call /aux2_breaker false && rosservice call /aux2_breaker true
