Electrical Overview
-------------------

Each joint has a dedicated motor controller board (MCB) with a dedicated
microcontroller and an RS-485 connection. The arm MCBs are on a single bus while
all other MCBs share the other bus. All MCB data travels to the mainboard,
located in the front of the robot (behind the laser). The mainboard is then
connected to the robot computer via Ethernet. The ``fetch_drivers`` package
provides an interface to these components.

Fetch and Freight both have two 12V Sealed Lead Acid (SLA) batteries located
in the robot base. These batteries are kept charged by the mainboard (see
:ref:`charging`).

Access Panel
++++++++++++

Fetch and Freight both have an access panel with 2 USB, an Ethernet, and an
HD Video port. All of these ports are connected directly to the onboard
computer. In addition, Fetch has an extra USB port on the head.

.. TODO:: add image of access panel
