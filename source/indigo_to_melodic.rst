ROS Melodic + Ubuntu 18.04
==========================

.. WARNING::
   As of 7-19-2019, some issues are still being worked out with some installs. You
   should ensure that your research needs will allow for a possible prolonged
   troubleshooting phase with your robot(s).

Fetch Robotics has recently started supporting ROS Melodic and Ubuntu 18.04 on
Fetch and Freight robots.  Other than the process of upgrading a robot, there
should be minimal effect on using your robot.  If you observe an issue, please
let us know via a support ticket.

Known issues
============

.. WARNING::
   The PS3 controller does not work as well on 18.04 as it did on 14.04. To achieve
   smooth control, the input from the controller will need to be continually varied.
   This can be done by continually moving or shaking the controller.  Alternately,
   you can `switch to using a PS4 controller <ps4.rst>`_.

.. WARNING::
   Gazebo9 and the Fetch have some bugs which we are currently aware of.
   If you use Gazebo, please check the status of this `issue on GitHub <https://github.com/fetchrobotics/fetch_gazebo/issues/37>`_.

Upgrading Your Robot to ROS Melodic + Ubuntu 18.04
--------------------------------------------------
.. WARNING::
   Read this document in full to ensure you understand the procedures.  It is
   not straightforward to go back to ROS Indigo/Ubuntu 14.04 after doing this.
   Ensure your colleagues are on board with doing this upgrade.

This document is a procedure for replacing the contents of your robot's SSD
with an Ubuntu 18.04 install and ROS Melodic.

Before Upgrade
++++++++++++++

Back up files from the robot!  There are a few categories of files to back up:

#. Calibration and other robot-specific files. By convention, these are
   all in ``/etc/ros/[indigo|melodic]/``
#. Files relating to your research work
#. A record of what packages you installed for ROS Indigo
#. Udev rules created for additional hardware (e.g. sensors) added to your robot
#. Network hardware configuration (for troubleshooting)

Below, we assume that after logging into the robot (e.g. via ``ssh``) you back up
files to a machine named HOST with username USER.

For (1), we recommend doing::

  tar -zcf fetch_robot_files.tar.gz /etc/ros/indigo/
  scp fetch_robot_files.tar.gz USER@HOST:~/

For (2), this may include workspaces, logs, and training data.  You might even
want to back up the entirety of ``/opt/ros/indigo`` if you are unsure.

For (3), you can easily record the list of packages you installed via::

  dpkg -l | grep ros-indigo > installed_indigo_packages.txt

As well, you might want to record what repositories are part of your workspaces.

For (4), such files are likely located in ``/etc/udev/rules.d/``, and should be saved.

For (5), this file may be useful for reference if the install process doesn't
automatically set up networking on your robot correctly::

  scp /etc/udev/rules.d/70-persistent-net.rules USER@HOST:~/$(hostname)_udev_net_rules

If you are using any additional hardware (sensors), be sure to record what network
or other hardware configuration changes were made to get them working.

AUTOMATED INSTALLER: 18.04 and ROS Melodic Install
++++++++++++++++++++++++++++++++++++++++++++++++++

.. IMPORTANT::
   Back up your files as described in the previous section

#. **Runstop the robot**, to avoid unexpected movement of the robot.
#. Create the installer USB flash drive on a separate computer:
  #. In a web browser, navigate to http://packages.fetchrobotics.com/images/ and click and
     download the latest fetch_ubuntu_*.iso
  #. Plug the flash drive into your computer.
  #. In a terminal, run ``sudo usb-creator-gtk``. This will open a utility for putting the
     install image onto the flash drive.  Select the fetch_ubuntu.iso file (you may have to
     browse via “Other”.  Verify the correct disk is selected in the second listbox, and then
     click "Make Startup Disk".
     (If usb-creator-gtk fails to work, you probably will need to format the disk using, e.g.,
     gParted.  After formatting the USB drive, retry usb-creator-gtk)

#. Install OS:
  #. Plug in the USB flash drive to the robot, as well as a monitor, keyboard and mouse.
  #. Turn the robot on with the power button, and press either F7 or F11 several times to get
     to the boot device selection window shown in the next step. If you fail to get to a
     screen like the below, restart the robot and try again:
  #. The name of the correct option in the boot menu varies based on the flash drive you used.
     Typically, it will be similar to "UEFI (FAT) FlashDrive Name". See the following images
     for what to expect and select:

.. |Boot selection| image:: _static/boot_selection.jpg

.. |Installer selection| image:: _static/install_selection.jpg

.. |Continue Install| image:: _static/install_continue.jpg

.. |Initial post-install prompt| image:: _static/install_prompt.jpg

  #. If the robot is not connected to the internet via an ethernet cable, you will next be
     prompted to connect to a wifi network in order to install needed packages.  Otherwise,
     you will be prompted whether to *also* connect to a wifi network.
  #. Next you will be prompted to give the robot's name.  A name other than fetchXX or freightXX
     will result in a non-robot install of Ubuntu 18.04 (with ROS also installed). We recommend
     keeping the same hostname for the robot, e.g. `fetch4`
  #. The `fetch` user will be automatically created, with password 'robotics'.
  #. Wait for the install to complete.  The post-install script will restart fairly quickly,
     and then resume running/installing after the reboot.  It will then reboot a second time
     at which point, the desktop should be blank, and the install is complete.

If the installer appears to get stuck, please send a picture of the screen to Support.


MANUAL APPROACH: 18.04 Install and Installing ROS/Fetch Packages
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

.. IMPORTANT::
   Back up your files as described in the previous section

#. **Runstop the robot**, to avoid unexpected movement of the robot.
#. **Install Ubuntu 18.04 on the robot.** Download the latest 18.04 Ubuntu installer from http://releases.ubuntu.com/18.04/
   (in these instructions we use the Desktop image, version 18.04.2).
   For help booting from USB, see `Accessing Boot Menu on Fetch Robots`_.

  #. We recommend keeping the same hostname for the robot, e.g. `fetch4`
  #. You can create the `fetch` user, or let it be automatically created later.
     (The typical password for the `fetch` user is 'robotics'.)

  - After install, you may need to unblock `apt`. Do this by clicking the App Store
    icon on the sidebar, which should trigger an update prompt you can close: |AppStore|
  - You'll probably want to install a few convenience packages such as openssh-server
    to enable SSH into your robot: ``sudo apt install openssh-server net-tools``.
    You might also want to install your favorite commandline text editor.

#. **Update your Ubuntu install:** ``sudo apt update && sudo apt dist-upgrade -y``
#. To make the robot works correctly when a monitor is not attached, run:
   ``sudo systemctl set-default multi-user.target``
#. **Install ROS Melodic** by following the instructions
   `on the ROS Wiki <http://wiki.ros.org/melodic/Installation/Ubuntu>`_.
   You will want to do steps 1.1 through 1.6. In writing/testing these instructions, we assume:

  - You use the **ROS-Base** setup, via the ``ros-melodic-ros-base`` package.
  - You're using bash, so step 1.6 for the fetch user is::

        echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
        source ~/.bashrc

    You can also make this apply for all new users:
    ``sudo su -c 'echo "source /opt/ros/melodic/setup.bash" >> /etc/bash.bashrc'``

#. **NOTE**: at a later time, Fetch may host and recommend its own mirror of ROS Melodic debians.
#. Run the following to **install Fetch research debians**:

   - General packages for Fetch robots::

       sudo apt install ros-melodic-fetch-calibration ros-melodic-fetch-open-auto-dock \
       ros-melodic-fetch-navigation ros-melodic-fetch-tools -y

   - Then install packages specific to the robot type::

       export ROBOTTYPE=$(hostname | awk -F'[0-9]' '{print $1}')
       # sudo apt install $ROBOTTYPE-melodic-config  # pending future availability
       wget http://packages.fetchrobotics.com/binaries/$ROBOTTYPE-melodic-config.deb
       sudo apt install ./$ROBOTTYPE-melodic-config.deb -y

     If you get an error regarding `chrony`, do `sudo apt install chrony`, and then try the
     melodic-config debian install again.

#. **Power cycle the robot**::

        sudo /sbin/reboot

.. |AppStore| image:: _static/app_store.jpg

Post-install Validation
+++++++++++++++++++++++
This is a direct continuation of the previous section's procedure. It is assumed
that your robot is still runstopped.

Verify that things are working.  All of the following steps assume that you are
``ssh``'d into the robot::

        ssh fetch@fetchXXXX

#. If your robot has not been upgraded in a while, it is likely that it will need to
   automatically upgrade the firmware on its boards. This can take several minutes
   to complete after you have rebooted the robot. You can monitor this by doing::

        sudo tail -f /var/log/ros/robot.log

   You may see messages like the following::

        [ WARN] [1554930321.086981030]: Updating wrist_roll_mcb from -1 to 101
        [ INFO] [1554930321.087023328]: Updating board 44
        [ WARN] [1554930321.094045845]: updating firmware loader for board 0x11
        [ WARN] [1554930323.609072063]: updating firmware loader for board 0x11
        [ WARN] [1554930323.614075007]: Unexpected response for board 17 :  recv_len=20 board_id=17 table_
        addr=16 data_len=16
        [ WARN] [1554930323.614149147]: Unexpected response for board 38 :  recv_len=20 board_id=38 table_
        addr=16 data_len=16

   If you see the second sort of message, the likely fix is to power cycle the robot again
   via ``rosrun fetch_drivers charger_power reboot``.


#. Verify that calibration is installed, e.g. a date should be output if you run the command below::

        fetch@fetch3:~$ calibrate_robot --date
        2018-11-26 14:48:04

#. Verify that the robot can ping the mainboard and the laser::

        ping 10.42.42.42  # mainboard
        ping 10.42.42.10  # laser

   If not, see `Ensuring robot's ethernet ports are configured correctly`_

#. Verify that the Primesense camera is working (if working with a Fetch robot)::

       rostopic list head_camera | wc -l

   This should output 32, if everything is working fine.

#. At this point, release the robot's runstop button.

#. The gripper should now have power, so we should be able to ping it::

       ping 10.42.42.43  # gripper

   If the gripper does not respond, please contact support. We are aware of an issue
   affecting some robots, and are gathering information to identify the cause and
   best solution.

#. The arm's "gravity compensation" should now be working. You should be able to
   freely move the arm by hand.

#. Check whether your PS3 controller pairs and controls the robot.

   **Important note**: The PS3 controller currently won't work with ROS by default.
   To fix this, run ``sudo ln -s /dev/input/js0 /dev/ps3joy``. We hope to fix this
   by fixing the corresponding udev rules eventually.

   - If you then verify that the /joy topic is publishing, you may need to do
     ``sudo service robot stop && sudo service robot start`` before the robot
     responds to teleop.
   - The previously described fix of creating /dev/ps3joy may reset on power-cycle.
     A more permanent hack is described
     `in this comment <https://github.com/fetchrobotics/docs/issues/66#issuecomment-485049854>`_.

   **Important note**: for 18.04 the robots have switched from using sixad to using
   PS3joy.  While you do not need to re-pair the controller to the computer, note that
   the utility for doing so is now located at ``/opt/ros/melodic/lib/ps3joy/sixpair``.
   Some other changes in behaviour you may see:

   - The LEDs on the PS3 controller may continually blink, even though it is connected.
   - Inputs may not be sent from the PS3 controller if the accelerometers in the
     controller do not detect motion. This can result in jerky motion when using
     the controller.

   We are hoping to determine fixes for these in the near future.

#. At this point the robot is probably working fine and is ready for use! (Unless you
   have additional customizations to restore; see next step)

#. If applicable, from your non-robot computer, restore the contents of
   ``/etc/ros/indigo`` to ``/etc/ros/melodic`` on the robot::

        scp fetch_robot_files.tar.gz fetch@fetchXXX:~/
        ssh fetch@fetchXXX
        sudo mkdir -p /etc/ros/melodic
        tar -xzf ~/fetch_robot_files.tar.gz /etc/ros/melodic/

   **Important**: You should modify ``/etc/ros/melodic/robot.launch`` to replace any
   instances of ``indigo`` with ``melodic``

   As well, you can restore any other saved files to the robot.

   This is the point at which some things may not work fully, e.g. if packages
   used in ROS Indigo need updates/replacements for ROS Melodic.


Compatibility of Other Computers Used with the Robot
----------------------------------------------------

For working with a robot running ROS Melodic, we recommend using an 18.04 Ubuntu
machine that also has ROS Melodic installed.

- In order for the robot to appear correctly in RViz, you will want to:

  - Ensure your computer is pointed at the packages.ros apt sources
  - Install ``ros-melodic-fetch-description`` and ``ros-melodic-freight-description``
    packages.  Addtionally you might want to install
    `ros-melodic-fetch-tools <https://github.com/fetchrobotics/fetch_tools>`_.
  - Ensure that these packages are included in your path (e.g.
    ``rospack find fetch_description`` returns a path)
  - Common gotcha on a new setup: If the robot model doesn't appear at first, you
    may want to change the "Fixed frame" from e.g. 'map' to 'odom'.

Not Recommended/Supported: Upgrading from 14.04 to 18.04 (via 16.04)
--------------------------------------------------------------------
Fetch Robotics does not recommend this approach and *cannot* provide support for this.
However, if you desire to try to upgrade, the following may be helpful:

- Back up files as described above, or even the full disk if you like.
- You cannot upgrade Ubuntu directly from 14.04 to 18.04. You must first
  upgrade to 16.04 first. This can take a long time.
- You should review the postinstall script for ``fetch-melodic-config``. It is not
  targeted at upgrading a system, so additional tweaks may be required after
  installing it.


Appendices
----------

Disk filling issue
++++++++++++++++++
Some robots may encounter an issue where Gnome3 fills the disk by spamming /var/log/syslog.
This issue has a fix that is not available via `apt` yet, but can be manually done:
https://bugs.launchpad.net/ubuntu/+source/gnome-shell/+bug/1772677/comments/63

Ensuring robot's ethernet ports are configured correctly
++++++++++++++++++++++++++++++++++++++++++++++++++++++++

The robot has two ethernet ports on its computer. You can find more information on this
at `Computer Overview and Configuration <computer.rst>`_.

The most likely problem you may encounter after getting 18.04 installed is if these two
ports are "swapped".  This will cause the robot computer to be unable to talk to the
rest of its hardware. You can fix this in software or in hardware:

- Software: Edit ``/etc/udev/rules.d/70-persistent-net.rules`` and swap ``eth0``
  and ``eth1``. Restart the robot for the change to take effect.
- OR: Hardware: swap the two ethernet cables where they plug into the computer.
  This shouldn't be needed, but in case you do, you should expect to find
  a gray cable (internal communications) and a blue cable (external).
  Typically, the blue goes to the top ethernet port, and the grey goes to the bottom.

Another issue you may encounter with 18.04 is if you are using the ethernet on the
side access panel with a DHCP setup. In some setups, the ethernet port may fail to
be assigned an IP automatically. We recommend consulting IT for help with this, if
needed.

Accessing Boot Menu on Fetch Robots
+++++++++++++++++++++++++++++++++++
You may need to access the boot menu in order to boot from a USB flash
drive and install Ubuntu 18.04.  Due to different computer motherboards used in the
past, Fetch research robots may be using one of two BIOS flavors.  Older robots
use an MSI branded BIOS.  Newer robots use American Megatrends Inc. (AMI).

These different BIOS types activate the boot media selection menu with different keys:

- If your robot shows the MSI splash screen at boot, press F11 to access the boot menu.
- If your robot shows the black AMI splash screen at boot (this lasts for about 1 second),
  press F7 to access the boot menu.

If you fail to get into the boot menu, you can restart the computer and try again.
