Mechanism Terminology
---------------------

The Fetch & Freight kinematics are defined by using the concepts of
joints, links, and frames. Each of these is defined and represented in
code, as well as having a unique name. A link is a rigid body in the
kinematic tree, and will have a coordinate frame, but not all frames
are associated with links. ”Fixed” joints are allowed, so some rigid
bodies that could be considered one link are considered to be two
links rigidly joined together. This is done mostly at locations where
there is a physical interface between components.

Link 
++++ 

A link is considered to be a rigid body within the robot. It generally
has geometry to define visual and collision-space representations, has
inertial properties, and has a name. The links for the Fetch & Freight
are defined in the URDF description that can be found in the
fetch_description or freight_description package respectively.

Frame
+++++

Frames are geometric entities that represent coordinate frames in
space. Every link has an associated frame, but frames are also used to
represent other things, such as the optical frame of a camera, the
origin of global map, or the location of a detected object. Frames are
always defined relative to one another, and relationships and
transformations between them are tracked using the tf package.

Joint
+++++

A joint is considered to be part of the robot, and define the
relationship between links. The joints for the Fetch & Freight are
defined in the URDF description that can be found in their respective
description package. The Fetch & Freight mostly have rotational
joints, but the torso is translational, and there are also a number of
”fixed” joints used to represent the notion that two links are part of
the same rigid body. Rotational and translational joints are generally
represented in the same way in the system, and are referred to as
joint ”effort” instead of force or torque, as well as using position,
and velocity to represent both linear and angular movement.

Fetch Home Pose
+++++++++++++++

In order to describe the Fetch robot pose and joint positions in a
consistent manner, a home pose of the robot has been defined. At the
home pose, all joint angles are considered to be at zero. In the home
pose the arms is straight out in front of the robot, the gripper is
closed, and the head is centered and level. For most joints the
calibration reference point is not at the home pose, or zero
position. The URDF of the Fetch contains the offsets between the zero
positions and the home positions of the joints.

Coordinate System
+++++++++++++++++

The coordinate frames for all links of the Fetch & Freight are defined
to aligned with a world coordinate frame of positive z-axis up,
positive x-axis forward, and positive y-axis robot-left when Fetch
is in the home pose. All joint angle conventions are chosen so that
from the home position, positive motion of the joint causes positive
motion around one of the positive axes of the world coordinate frame.


Naming Conventions
++++++++++++++++++

In general, the names for a link and the associated frame will be
similar (e.g. forearm_link and forearm_frame). For components such
drive wheels that are included in the robot in multiple locations, a
short prefix is used to indicate which location is referred.

TODO include image of fetch and freight naming scheme