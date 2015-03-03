Tutorial: Gazebo Simulation
===========================

Starting the Simulator
----------------------
The ``fetch_gazebo`` package includes several launch files:

 * simulation.launch spawns a robot in an empty world.
 * playground.launch spawns a robot inside a lab-like test environment.
   This environment has some tables with items that may be picked up
   and manipulated. It also has a pre-made map which can be used to
   test out robot navigation.

To start the simplest environment:

::

    >$ roslaunch fetch_gazebo simulation.launch

.. figure:: _static/gazebo.png
   :width: 100%
   :align: center
   :figclass: align-centered

Note that all of the environments will prepare the robot by tucking the
arm and giving the head an initial command.

Visualizing with RVIZ
---------------------
Even though Gazebo has a graphical visualization, RVIZ is still the preferred
tool for interacting with your robot.

::

    >$ rosrun rviz rviz

.. todo:: ADD IMAGE OF RVIZ

You can now `manually set up your RVIZ visualization 
<http://gazebosim.org/tutorials?tut=drcsim_visualization&cat=drcsim#VisualizingtheRobotmodel>`_
or re-run RVIZ with a configuration file using the command line.

The default ``.rviz`` configuration file for Fetch can be loaded using:
::
	>$ roscd fetch_navigation
	>$ rviz navigation.rviz

.. todo:: ADD IMAGE OF DEFAULT CONFIG

Simulation vs. Real Robots
--------------------------
The simulated robot may not be identical to the real robot. In fact, the
real robot is likely quite a bit better behaved. Also:

 * The simulator does include the IMU. Therefore, there is also no
   base odometry fusion with IMU data, and the base_controller publishes
   all required TF data directly.
