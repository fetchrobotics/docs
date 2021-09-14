Tutorial: Calibrating Fetch
===========================

Calibrating your Fetch Research Edition Robot is essential to getting
the best performance. Fetch Robotics recommends re-calibrating the robot
after every shipping or travel excursion your robot undertakes.

.. note:: No calibration procedures are needed or exist for the Freight Research Edition Robot.
This page is only applicable to the Fetch.

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
file in `/etc/ros/melodic/robot.launch`. Therefore, the last step in calibration
is to update that launch file and restart the drivers. Currently, the
following aspects are updated:

 * The URDF file is copied to /etc/ros/melodic, and the name of the file is put
   into robot.launch. The calibration offsets are updated in the URDF file.
 * The camera calibration YAML files are copied to /etc/ros/melodic, and the
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
through a series of poses (about 100 poses) and upon completion of the calibration will update
the robot configuration in /etc/ros/melodic.  This typically takes about 10 minutes to complete:

::

    >$ calibrate_robot --arm --install

Finally, after the new calibration has been installed into /etc/ros/melodic,
you can view the calibration by opening RVIZ and seeing that the robot model
overlaps with the point cloud from the head camera. If for some reason, the
calibration is not good, you can restart from the `--reset` command or roll
back to the previous calibration with:

::

    >$ calibrate_robot --restore

.. _torso_calibration:

Calibrating Fetch Torso
-----------------------
When the torso controller board is first powered, it uses measurements from two different
position sensors to determine the absolute starting position of the torso.
Once the absolute starting position of the torso is determined, the position measurement
will retain millimeter precision as long torso remains powered.

To work properly, the two torso sensors must be calibrated together.
If the sensors are not properly calibrated, the calculation of the initial torso position
could be incorrect in some situations. This problem is more likely to occur if the torso is
first powered when in the "up" position.
A bad torso position should be easy to detect when using RVIZ since the torso position
shown in RVIZ will always be more than +/-10cm different than the true torso position.

The torso sensors are calibrated in production, so they will not usually need
to be recalibrated.  If there seems to be a torso positioning problem,
the torso calibration tool should be first used to verify the calibration of the torso.

In release 0.7.4 of fetch_drivers package there is a tool 
to verify or calibrate the torso sensors.
The tool has two options: verify and calibrate.
The verify option will only verify that the calibration is good,
it will not change any stored calibration parameters.
The calibrate option will calibrate the sensors and update the parameters
stored on the torso controller.

For both options, the torso will travel through its entire range of
motion while sensor data is collected.  While the tool is being run,
the robot drivers will be stopped and the robot arm will not hold its position.
Because of this, the arm should be tucked or soft fabric or cardboard
should be placed between arm and base to avoid scratching any covers.


Torso Calibration Procedure
^^^^^^^^^^^^^^^^^^^^^^^^^^^
.. warning::
    During torso calibration the arm will not hold position.
    Place cardboard or soft fabric between arm and base to avoid
    scratching covers during data collection.

Follow these steps in order to verify or calibrate the torso position
sensors:

1. Move torso to lowest position, and tuck the arm.

2. Place a protective barrier between the arm and top base cover.

3. Disable robot drivers by running : ``sudo service robot stop``

4. Run torso calibration tool:

  * To run calibration : ``rosrun fetch_drivers torso_calibrate calibrate``
  * **OR** to verify calibration : ``rosrun fetch_drivers torso_calibrate verify``

6. Wait for torso to collect sensor data.  The torso will move upwards in small increments through the entire range of motion.  A clicking sound will be produced by the torso while moving, and is normal.

7. Cycle Run-stop (optional).  Sometimes tool will request that run-stop be cycled
   after it completes.  Cycling run-stop will cycle power to the torso controller board,
   and is required in some situations.

8. Once tool has completed, restart robot drivers with ``sudo service robot start``

Calibration Output
^^^^^^^^^^^^^^^^^^
Once the tool has completed the calibration procedure it will check the expected results of calibration.
If everything checks out, the ``torso_calibrate calibrate`` will output something similar to::

  VERIFY PASSED : max sensor error of 0.0116824 is within acceptable limit

If there was a problem calculating good calibration parameters, the output might look like::

  VERIFY FAILED : max sensor error of 0.0501323 is larger than acceptable limit of 0.04

In case of failure, the torso sensor may be malfunctioning or damaged and a support ticket should be created.

.. note::
  The value for max sensor error is the mismatch between the two torso sensors.
  The accuracy of the torso position measurement is unrelated to this value.

Output When Verifying New Torso Calibration
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
``torso_calibrate verify`` will produce output stating whether sensors are well
calibrated. If the sensor calibration is good, then this command will
output something similar to::

  VERIFY PASSED : max sensor error of 0.0109411 is within acceptable limit

Otherwise it will produce output like::

  VERIFY FAILED : max sensor error of 0.0501323 is larger than acceptable limit of 0.04

When verification fails, run calibration produce.
