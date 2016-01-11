Tutorial: Calibrating Fetch
===========================

Calibrating your Fetch Research Edition Robot is essential to getting
the best performance. Fetch Robotics recommends re-calibrating the robot
after every shipping or travel excursion your robot undertakes.

Understanding Calibration
-------------------------

The `fetch_calibration` package provides a method of making sure that the
hand-eye coordination of the robot is well calibrated. Calibration involves:

 * Moving the arm to a series of poses
 * At each pose, recording the joint_angles reported by the
   drivers. Calibration then blinks the gripper LEDs several times to
   find their pose in the camera frame and records it.
 * Performing a non-linear optimization which adjusts joint offsets and
   the head camera pose to minimize the error between the expected pose of the
   the LEDs based on projection of the kinematics of the arm and the actual
   pose seen by the camera.
 * Updating the URDF and robot launch files with newly determined offsets.

The :ref:`upstart_services` that start the robot will use the launch
file in `/etc/ros/indigo/robot.launch`. Therefore, the last step in calibration
is to update that launch file and restart the drivers. Currently, the
following aspects are updated:

 * The URDF file is copied to /etc/ros/indigo, and the name of the file is put
   into robot.launch. The calibration offsets are updated in the URDF file.
 * The camera calibration YAML files are copied to /etc/ros/indigo, and the
   name of the files are put into robot.launch.
 * The head_camera driver has two parameters, z_offset_mm and z_scale which
   are calibrated. Their updated values are stored in robot.launch.

Calibrate Robot Tool
--------------------

The `fetch_calibration` package provides a tool called `calibrate_robot`
which fully automates tasks related to calibration. Once you have sourced
the ROS setup.bash, running `calibrate_robot` without any arguments will
show the list of valid arguments:

::

    >$ calibrate_robot
    usage: calibrate_robot [-h] [--arm] [--base] [--install] [--reset] [--restore]
                           [--date] [--directory DIRECTORY]

    Calibrate the robot, update files in /etc/ros

    optional arguments:
      -h, --help            show this help message and exit
      --arm                 Capture arm/head calibration data
      --base                Capture base calibration data
      --install             Install new calibration to /etc/ros (restarts drivers)
      --reset               Reset the calibration to factory defaults (restarts
                            drivers)
      --restore             Restore the previous calibration
      --date                Get the timestamp of the current calibration
      --directory DIRECTORY
                            Directory to load calibration from or backup to

A useful command to note is the `--date` option, which will return the date
that the current calibration was generated (or 'uncalibrated' if the robot
has not yet been calibrated):

::

    >$ calibrate_robot --date
    2015-06-06 23:20:18

Running Calibration
-------------------

.. warning::

    Calibration will cause the arm to move through the environment. Raise the
    torso to full extension and be sure that the robot has at least 1 meter
    of free space all around it.

The first step to calibrate the robot is to reset the calibration to factory
defaults:

::

    >$ calibrate_robot --reset

This command might ask for your password, as it requires sudo to update the
files in /etc/ros/. This will also restart the drivers to
make the changes take effect.

.. warning::

    When calibrating, make sure that no other applications are subscribed
    to the head_camera topics. Other applications, even RVIZ, connecting
    to the head_camera driver between the restart of drivers and the start
    of calibration may adversely affect the auto_exposure settings of the
    camera.

The robot is now ready to calibrate. The following command will move the arm
through a series of poses and upon completion of the calibration will update
the robot configuration in /etc/ros/indigo:

::

    >$ calibrate_robot --arm --install

Finally, after the new calibration has been installed into /etc/ros/indigo,
you can view the calibration by opening RVIZ and seeing that the robot model
overlaps with the point cloud from the head camera. If for some reason, the
calibration is not good, you can restart from the `--reset` command or roll
back to the previous calibration with:

::

    >$ calibrate_robot --restore

