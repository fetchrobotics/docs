Issues and Support
==================

When you encounter an issue
---------------------------

As a first step, we recommend checking out the :doc:`FAQ </faq>`.

Reporting software bugs
-----------------------

If you've identified a specific issue in the open source code from Fetch Robotics,
Pull Requests with proposed fixes or Issues describing the issue on Github are welcome.

Contacting Fetch Support
------------------------

Reaching Fetch Support
~~~~~~~~~~~~~~~~~~~~~~
When purchasing robots, customers will have accounts created on the
`Fetch Support Website <http://support.fetchrobotics.com:8080/>`_.
Logging in and creating a ticket here is the preferred method for support requests.

If you did not receive this login information, or need to requesting additional
research support logins, please reach out to your sales contact for more information.

How do I create a good support ticket?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Please note which robot you are working with (e.g. Fetch 4) and describe the issues
you are seeing, as well as any possibly related hardware modifications you have made.
You can also attach the debug-snapshot zip file to help debugging via the process below.

* Make sure the robot is not runstopped and then run the following commands on your local computer (Not the robot!)

::

   sudo apt update && sudo apt install ros-melodic-fetch-tools
   declare -x ROS_MASTER_URI="http://*RobotHostNameGoesHere*:11311"
   fetch debug-snapshot

* Create a new support ticket and attach the zip file that was created

* Clearly state problem you are having in the ticket so we can better serve you
