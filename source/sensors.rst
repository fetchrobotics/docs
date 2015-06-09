Sensor Overview
---------------

Base Laser
++++++++++

Both Fetch & Freight have a SICK TIM571 scanning range finder. The
laser has a range of 25m, 220° field of view, 15hz update rate
and angular resolution of 1/3°. The laser publishes both distance
and RSSI (Received Signal Strength Indication)
to the **base_scan** topic.

IMU
+++

The mainboard of Fetch and Freight have a 6-axis inertial measurement
unit (IMU). The gyroscope within the IMU is capable of measuring
+/-2000 degrees per second, while the accelerometers are capable of
measuring +/-2g. See :ref:`imu_api` for details on the ROS API.

Speakers
++++++++

The mainboard of Fetch and Freight contains a USB audio device.
While the device enumerates as a standard Linux audio device, we recommend
using the `sound_play ROS package <http://wiki.ros.org/sound_play>`_ to
access the speakers. ``sound_play`` is automatically started as
an :ref:`upstart service<upstart_services>` when the robot starts.
This service is pre-configured to have the correct group-level access
to the audio system. If using the speakers directly through a Linux
interface, be sure to add your user to the ``audio`` group in order
to actually access the speakers.

Head Camera
+++++++++++

Fetch has a Primesense Carmine 1.09 short-range RGBD sensor. This
camera is best calibrated in the 0.35-1.4m range. See :ref:`camera_api`
for details on the ROS API.

Gripper Sensors
+++++++++++++++

In addition to the position and effort feedback of the gripper joint, the
gripper incorporates a 6-axis interial measurement unit (IMU). The gyroscope within
the IMU is capable of measuring +/-2000 degrees per second, while the
accelerometers are capable of measuriing +/-2g.
See :ref:`imu_api` for details on the ROS API.
