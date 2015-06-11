Sensor Overview
---------------

Base Laser
++++++++++

Both Fetch and Freight have a SICK TIM571 scanning range finder. The
laser has a range of 25m, 220° field of view, 15Hz update rate
and angular resolution of 1/3°. The laser publishes both distance
and RSSI (Received Signal Strength Indication)
to the **base_scan** topic.

IMU
+++

The mainboard of Fetch and Freight have a 6-axis inertial measurement
unit (IMU). The gyroscope within the IMU is capable of measuring
+/-2000 degrees per second, while the accelerometers are capable of
measuring +/-2g. See :ref:`imu_api` for details on the ROS API.

Head Camera
+++++++++++

Fetch has a Primesense Carmine 1.09 short-range RGBD sensor. This
camera is best calibrated in the 0.35-1.4m range. See :ref:`camera_api`
for details on the ROS API.

Gripper Sensors
+++++++++++++++

In addition to the position and effort feedback of the gripper joint, the
gripper incorporates a 6-axis inertial measurement unit (IMU). The gyroscope within
the IMU is capable of measuring +/-2000 degrees per second, while the
accelerometers are capable of measuring +/-2g.
See :ref:`imu_api` for details on the ROS API.
