Safety
======

Safety is extremely important to Fetch Robotics. Safe operation of
robots is important yet challenging and it is important to remember
that safety is a continual process that is shared by the robot
designer, operator, and administrator. The following section provides
an overview of the issues, safety-related design features, and a basic
set of guidelines to support safety when using the Fetch & Freight
R&D robots.

Safety Overview
---------------

When operating Fetch & Freight R&D robots users should always be
conscious of safety. Remember the robots are heavy pieces of equipment
and moving parts. As the robots travel through an environment they can
carry and manipulate a wide variety of objects. Since the Fetch &
Freight R&D robots are for applications development, their moves and
actions may not be entirely predictable. Both the Fetch & Freight
robots can cause significant damage if they fall on or run into a
person. There are also several ways that the robots can pinch, grab,
or twist fingers or other body parts (these regions are
labeled). Fetch can also manipulate dangerous objects and knock over
heavy objects. People should always be cautious and attentive around
Fetch & Freight R&D robots.

Design Features
---------------

While retaining the power of a R&D platform, both the hardware and
software of Fetch & Freight are designed to minimize risk. The
exterior of both Fetch & Freight clearly mark regions that could pinch
or injure while mechanism is in motion or being moved by hand. Both
Fetch & Freight have emergency stop buttons in case there is a need to
immediately stop the motion of the robot.

In software, low-level safety limits have been incorporated to limit
motor current, motor velocity, range of joint motion, and trajectory
deviations. High-level applications also integrate the various
on-board sensors to avoid obstacles when navigating or moving the arm.

These design features help make Fetch & Freight more robust. However a
R&D robot is **never** absolutely safe. The application developers'
safety, as well as the safety of others, depends on the developers'
constant attention. It is important for the user to be aware of
potential dangers and learn to anticipate and prevent problems.

General Usage Guidelines
------------------------

While many guidelines for safe use of a robot stem from common sense,
a basic set is listed below. It is important to follow these
guidelines, but please note that these guidelines alone do not
guarantee safety, only reduce risk.

* **Before operating** or working with a Fetch or Freight each user must:
 - Watch the safety video.
 - Read this user manual, specifically the entirety of Section 2 on Safety.

* **Supervise children, visitors**, and anyone who has not followed the previous guideline. In particular, make sure they: 

 - Do not come in range of Fetch or Freight R&D robots when active. 
 - Are aware that the robot could move unexpectedly and is potentially dangerous.
 - Are not alone with Fetch or Freight.  
 - Do not operate Fetch or Freight. 

* **Maintain a safe environment**. Safety is not only impacted by how a developer operates a robot, but the environment as well. The Fetch & Freight R&D robots are designed to operate in laboratory environments. 
 - Keep the robots **at least 5 meters from the top of a stairway or any other drop off**. 
 - Make sure the robots have adequate and level space for any expected or unexpected operation. 
 - If Fetch travels on a ramp, make sure that the spine is lowered and the arm is tucked so that the center of gravity is as low as possible. The slope of the ramp should not exceed 1:12. Also make sure that the robot cannot drive off the edge of the ramp. 
 - Make sure the environment is free of objects that could pose a risk if knocked, hit, or otherwise affected by the robots. 
 - Make sure that there are no ropes or cables that could get caught in the covers, wheels, or arm. 
 - Make sure that no animals are near the robots.
 - Keep fingers, hair, and clothing away from wheels, gears, and any location marked as a potential pinch point. 
 - Be aware of the location of emergency exits and ensure that the robots cannot block them. 
 - Do not operate the robots outdoors. 

* **The Fetch & Freight covers are flame-retardant**. However keep the robots away from open flames. Never use the robots around stoves or ovens.
\

* Do not allow the robot to come in contact with liquids (spilled drink, rain, etc.) If the robots do get wet, turn off the breaker switch at the back of the robot and contact Fetch Robotics.
\
 
* Before removing any covers, the robot should be unplugged and the breaker switch at the back of the robot should be off. 
\

* Make sure that the power cord is in good condition. Cord insulation must be intact with no crack or deterioration. Both connectors should be undamaged. If the power supply is damaged in anyway, it should be discarded and replaces with a new one from Fetch Robotics. 
\

* Do not run the robot without its covers, the covers help to protect users from internal mechanism pinch points and potential electrical shock.
\

* Use **common sense** when operating the Fetch & Freight R&D robots. 
 - Do not allow the robots to grab or hit any person.
 - Do not allow the robots to drive into contact with, or over, any body part. 
 - Do not allow the robot to interact with any sharp or dangerous items.
 - Do not allow the robot to operate potentially dangerous appliances (like stoves) or power tools. 
 - Pay attention to the **warning labels** on the robots.
 - **Do not modify or remove any part of the software safety features.**

Warning Labels
--------------

Below are pictures of all the warning labels that can be found on the
robot and associated safety issue.

.. TODO:: add images and descriptions... the table sucks.. 

.. csv-table:: 
   :widths: 50 50

   .. image:: _static/electrical_shock_charge.jpg, "**Electrical Shock** 
   Make sure that no foreign objects become lodged in the connector"
   .. image:: _static/pinch_point_head.jpg, **Pinch Point** Do not place fingers near the head while rotating
   .. image:: _static/pinch_point_torso.jpg, **Pinch Point** Do not place fingers under the torso skin while moving



