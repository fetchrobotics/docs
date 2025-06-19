Tutorial: Auto Docking
======================

Fetch Robotics has released a ROS package for automatically docking your robot
with a Fetch charging dock. This package uses the scanning laser range finder
to detect the profile of the charge dock and steers the robot onto the dock.
Since the profile of the charge dock must be clearly visible, it is important
that there is separation between docks and there are not any laser-height obstacles
on either side of the dock.

Running the Docking Node
-------------------------

But default, the auto docking node is launched at robot startup (via
`/etc/ros/noetic/robot.launch`)

A PS4 controller can be used to initiate docking and undocking as described below:

 * To dock your robot, point the robot at the charge dock and press the "circle"
   button on the PS4 controller. Docking works best when the robot is about 0.75-1.0
   meters away from the dock and pointed directly at it, however docking should work
   from a variety of angles.
 * To undock your robot when it is on a charge dock, press the "square" button
   on the PS4 joystick and the robot will back off the dock and then turn in place
   so it is pointed away from the charge dock.

.. warning::

    The docking controller does not have collision avoidance. Do not
    leave obstacles on the charge dock.


Manually Running the Auto Docking Nodes
---------------------------------------
To manually start the auto docking node:

::

    roslaunch fetch_auto_dock auto_dock.launch

This will bring up three ROS nodes. The first ROS node is the auto docking action
server. This node can be asked to dock with a charging dock through a ROS action
interface. A second and third nodes monitor the PS4 joystick in order to trigger
docking/undocking.

Auto Docking Programmatically
-----------------------------

The auto dock node exposes a ROS `action interface <http://wiki.ros.org/actionlib/DetailedDescription#Action_Interface_.26_Transport_Layer>`_
which can be used to dock the robot. This action interface is also used by the
demonstration python script.

This action is in the `dock` namespace and accepts a
`fetch_auto_dock_msgs/Dock <https://github.com/fetchrobotics/fetch_msgs/blob/master/fetch_auto_dock_msgs/action/Dock.action>`_
action message.

There are several fields in the goal:

 * ``dock_pose`` is a geometry_msgs/PoseStamped message which specifies where the
   dock center is located. This can be in any valid frame as the action server
   node will use TF to transform the pose into the odometry frame.
 * ``use_move_base`` is not currently implemented.

The result includes a single boolean ``docked`` which tells whether the robot has
actually docked and is charging.

The following Python code will dock the robot with a dock that is 1.0 meters
in front of it:

::

    #!/usr/bin/env python
    import rospy
    import actionlib
    from fetch_auto_dock_msgs.msg import DockAction, DockGoal

    # Create a ROS node
    rospy.init_node("dock_the_robot")

    # Create an action client
    client = actionlib.SimpleActionClient("/dock", DockAction)
    client.wait_for_server()

    # Create and send a goal
    goal = DockGoal()
    goal.dock_pose.header.frame_id = "base_link"
    goal.dock_pose.pose.position.x = 1.0
    goal.dock_pose.pose.orientation.z = 1.0
    client.send_goal(goal)

The fetch_auto_dock node also provides an ``undock`` action interface which
can be used to undock the robot from the charge dock. The goal to undock
has a single field

 * ``rotate_in_place`` if set to true, the robot will back off the dock and
   then rotate 180 degrees so it is facing off the dock. This can be very
   useful since navigation probably cannot get the robot off the dock when
   it is facing at the dock.
