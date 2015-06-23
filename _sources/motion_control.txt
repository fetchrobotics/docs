Motion Control
--------------

Each joint has a dedicated motor controller board (MCB) with a dedicated
microcontroller. The real-time components of the controls run on the
MCBs, while the robot computer streams commands to the MCBs.

.. figure:: _static/motion_control_overview.png
   :width: 80%
   :align: center
   :figclass: align-centered

All motors are brushless and each MCB runs an effort controller at 17.5kHz.
Each MCB can also run an optional velocity controller which takes a desired
velocity and outputs a control into the effort controller. Further, each
MCB can run a position controller which can feed into the velocity controller.
The position and velocity controllers each run at 1kHz, and the default
rate for the commands streaming from the robot computer is 200Hz.
Each MCB can then receive any of the following types of commands:

 * Desired position, desired velocity, and desired effort
 * Desired velocity and desired effort
 * Desired effort

Each MCB returns the measured effort, velocity and position of the joint it
is controlling.

Most users will want to use the high-level :ref:`arm_api` ROS API, however,
users can also create their own controllers as ROS plugins that run on the
robot computer and send commands to the MCBs using the
robot_controllers_interface package.
