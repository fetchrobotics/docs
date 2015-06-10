Care And Feeding
================

.. _charging:

Charging
--------

.. TODO:: add information on charging

Updating Your Robot
-------------------

Your robot has been pre-configured with ROS Indigo and the appropriate
APT repositories from which to fetch package updates.
Upgrading to the latest packages is as easy as:

::

   sudo apt-get update
   sudo apt-get install --only-upgrade ros-indigo-*
   sudo service robot stop
   sudo service robot start

Each circuit board within the robot is equipped with a bootloader, allowing
new and updated firmware to be installed. New releases of the `fetch-drivers`
package may include updated firmware for your robot, which will automatically
be installed when the drivers are next started (typically by the robot upstart
service). When restarting the robot service, there may be a slight delay
before the drivers are fully operational if a new firmware upgrade is included.

Cleaning Your Robot
-------------------

To clean fingerprints, dirt, and smudges from the skin of Fetch &
Freight use a clean soft cloth and isopropyl alcohol or window cleaner
(i.e. Windex). Make sure to wet the cloth with the isopropyl alcohol
or windex then gently clean the skins of the robot.

.. warning::

    Do not spray or pour isopropyl alcohol or window cleaner directly
    on the skins of the robot, this may damage the skins or worse
    cause fluids to enter the robot.

To clean the sensor optics of Fetch & Freight use the lens cloth
provided in the tool kit. Lens tissues or cotton swabs are also good
options for cleaning the optics of the robot.

.. warning:: 

    Do not use window cleaner, acetone, or abrasive cloths,
    as this may cause damage to the lens.
