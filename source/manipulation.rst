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

Simple MoveIt! Disco Example
----------------------------

This python script will run the robot through a simple disco dance motion.

::

  #!/usr/bin/env python

  # simple_disco.py: Move the fetch arm through a simple disco motion
  import rospy
  from moveit_msgs.msg import MoveItErrorCodes
  from moveit_python import MoveGroupInterface, PlanningSceneInterface

  # Note: fetch_moveit_config move_group.launch must be running
  # Safety!: Do NOT run this script near people or objects.
  # Safety!: There is NO perception.
  #          The ONLY objects the collision detection software is aware
  #          of are itself & the floor.
  if __name__ == '__main__':
      rospy.init_node("simple_disco")

      # Create move group interface
      move_group = MoveGroupInterface("arm_with_torso", "base_link")

      # Define ground plane
      planning_scene = PlanningSceneInterface("base_link")
      planning_scene.removeCollisionObject("my_front_ground")
      planning_scene.removeCollisionObject("my_back_ground")
      planning_scene.removeCollisionObject("my_right_ground")
      planning_scene.removeCollisionObject("my_left_ground")
      planning_scene.addCube("my_front_ground", 2, 1.1, 0.0, -1.0)
      planning_scene.addCube("my_back_ground", 2, -1.2, 0.0, -1.0)
      planning_scene.addCube("my_left_ground", 2, 0.0, 1.2, -1.0)
      planning_scene.addCube("my_right_ground", 2, 0.0, -1.2, -1.0)

      joint_names = ["torso_lift_joint", "shoulder_pan_joint",
                     "shoulder_lift_joint", "upperarm_roll_joint",
                     "elbow_flex_joint", "forearm_roll_joint",
                     "wrist_flex_joint", "wrist_roll_joint"]
      disco_poses = [[0.0, 1.5, -0.6, 3.0, 1.0, 3.0, 1.0, 3.0],
                     [0.133, 0.8, 0.75, 0.0, -2.0, 0.0, 2.0, 0.0],
                     [0.266, -0.8, 0.0, 0.0, 2.0, 0.0, -2.0, 0.0],
                     [0.385, -1.5, 1.1, -3.0, -0.5, -3.0, -1.0, -3.0],
                     [0.266, -0.8, 0.0, 0.0, 2.0, 0.0, -2.0, 0.0],
                     [0.133, 0.8, 0.75, 0.0, -2.0, 0.0, 2.0, 0.0],
                     [0.0, 1.5, -0.6, 3.0, 1.0, 3.0, 1.0, 3.0]]

      for pose in disco_poses:
          if rospy.is_shutdown():
              break
          move_group.moveToJointPosition(joint_names, pose, wait=False)
          move_group.get_move_action().wait_for_result()
          result = move_group.get_move_action().get_result()
          if result.error_code.val == MoveItErrorCodes.SUCCESS:
              rospy.loginfo("Disco!")
          if not result:
              rospy.logerr("Arm goal in state: %s",
                           move_group.get_move_action().get_state())
          rospy.sleep(0.1)
      move_group.get_move_action().cancel_all_goals()

More information and Tutorials on MoveIt!
-----------------------------------------

`General information <http://moveit.ros.org/>`_, `Documentation <http://moveit.ros.org/documentation/>`_ and `Tutorials <http://moveit.ros.org/documentation/tutorials/>`_ available at moveit.ros.org

