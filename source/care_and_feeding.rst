Care And Feeding
================

Charging
--------

TODO

Updating Your Robot
-------------------

Your robot has been pre-configured with ROS Indigo and the appropriate
Apt repositories. Upgrading to the latest packages is as easy as:

::

   sudo apt-get update
   sudo apt-get install --only-upgrade ros-indigo-*
   sudo service robot stop
   sudo service robot start

.. note::

    New releases of the `fetch-drivers` package may include updated firmware
    for your robot. When restarting the robot service, there may be a slight
    delay before the drivers are fully operational if a new firmware upgrade
    is included.

Cleaning Your Robot
-------------------

To clean finger prints, dirt, and smudges from the skins Fetch &
Freight use a clean soft cloth and isopropyl alcohol or windex. Make
sure to wet the cloth with the isopropyl alcohol or windex then gently
clean the skins of the robot. Do not spray/pour isopropyl alcohol or
windex directly on the skins of the robot, this may damage the skins
or worse cause fluids to enter the robot. 

To clean the sensor optics of Fetch & Freight use the lens cloth
provided in the tool kit. Do not use windex, acetone, or abrasive
cloths, as this may cause damage to the lens. Lens tissues or cotton
swabs are also good options for cleaning the optics of the robot.

.. TODO:: check that windex works for cleaning the robot as well as
isopropyl, do we want to put something in here about the cleaning the
fan?
