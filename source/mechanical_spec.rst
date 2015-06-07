Mechanical Specification 
------------------------ 

Do not operate Fetch or Freight before reviewing the mechanical
specifications listed below.

Environmental
+++++++++++++

The Fetch & Freight Research Edition Robots are indoor laboratory
robots. Operating outside this type of environment could cause
damage to the Fetch & Freight robots, and injury or death to
operators.

Drive Surface
'''''''''''''
 - The drive surface of the Fetch must be capable of supporting the
   entire weight of Fetch, about 250 lbs (113.3 kgs). If the surface is too
   soft, Fetch can get stuck and fail to drive. A commercial carpet or
   tile is recommended.
 - The drive surface of the Freight must be capable of supporting the
   entire weight of the Freight about 150 lbs (68 kgs) plus the weight
   of the payload. If the surface is too soft, Freight can get stuck
   and fail to drive. A commercial carpet or tile is recommended.

Incline Surface
'''''''''''''''
 - Fetch & Fright are ready for ADA-compliant ramps, which are at no more
   than a 1/12 slope. Ramps that are steeper than a 1/12 slope are unsafe
   and may be a tip-over hazard.

Water
'''''
 - Fetch & Freight have not been tested for any type of contact with water
   or any other liquid. Under no circumstances should Fetch nor Freight
   come in contact with water from rain, mist, ground water (puddles)
   and any other liquid. Water contact can cause damage to the electrical
   circuitry and the mechanism.

Temperature and Humidity 
''''''''''''''''''''''''
 - Fetch & Freight are designed to run in environments between 15C and 35C.
 - Keep Fetch & Freight away from open flames and other heat sources.
   Never use Fetch or Freight around stoves or ovens.

Forces and Torques 
++++++++++++++++++ 

Joint position, velocity, and force limits are implemented in the
Fetch & Freight URDF file as well as in firmware. Firmware implements
additional power limits. These joint limits
control the range of travel of the mechanism and the allowable velocity
to prevent over-travel. These limits are enforced by the controller,
and are designed to prevent poorly commanded control efforts from
damaging the robot or harming operators.

The limits below are from the Fetch & Freight URDF files. If a
velocity or torque limit is not specified, no value is enforced.

====================== ========== ============ =====
Joint                  Velocity   Torque/Force Power
====================== ========== ============ =====
*_wheel_joint          17.4rad/s  8.85Nm       120W
torso_lift_joint       0.1m/s     450N         TBD
head_pan_joint         1.57rad/s  0.32Nm       TBD
head_tilt_joint        1.57rad/s  0.68Nm       TBD
shoulder_pan_joint     1.25rad/s  33.82Nm      TBD
shoulder_lift_joint    1.45rad/s  131.76Nm     TBD
upperarm_roll_joint    1.57rad/s  76.94Nm      TBD
elbow_flex_joint       1.52rad/s  66.18Nm      TBD
forearm_roll_joint     1.57rad/s  29.35Nm      TBD
wrist_flex_joint       2.26rad/s  25.70Nm      TBD
wrist_roll_joint       2.26rad/s  7.36Nm       TBD
*_gripper_finger_joint 0.05m/s    60N            --
====================== ========== ============ =====

Joint Limits and Types
++++++++++++++++++++++

The position limits for the Fetch & Freight are specified below. These
"hard limits" are the maximum travel for the mechanism.

====================== ========== =========== ==========
Joint                  Type       Limit (+)   Limit (-)
====================== ========== =========== ==========
*_wheel_joint          continuous    --          --
torso_lift_joint       prismatic   400mm       0mm
head_pan_joint         revolute    90°         90°
head_tilt_joint        revolute    90° (down)  45° (up)
shoulder_pan_joint     revolute    92°         92°  
shoulder_lift_joint    revolute    87°         70°
upperarm_roll_joint    continuous    --           --
elbow_flex_joint       revolute    129°        129°
forearm_roll_joint     continuous    --           -- 
wrist_flex_joint       revolute    125°        125°
wrist_roll_joint       continuous    --           --
*_gripper_finger_joint prismatic   50mm       0mm
====================== ========== =========== ==========
