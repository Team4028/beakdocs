Section 4: Controllers
=======================

.. _setup:

Controllers do as their namesake: they control things. Ever played video games? You've used a controller.
Ever used a keyboard and mouse? You've used a controller. In FRC, the controllers we use are similar
if not identical to those found on consoles like Xbox.

picture of a controller

But how do we use them?

For simplicity's sake, we will be using the BeakXboxController class as our wrapper around
controllers. The BeakXboxController class itself wraps around the built-in WPILib class, XboxController,
which provides functionality to use Xbox and Xbox-like controllers for robots. Buttons are mapped properly
for an Xbox controller, and generally, this is how we give commands to the robot.

To start, get the BeakXboxController class. Go to `here <https://raw.githubusercontent.com/Team4028/2023-Drive/master/src/main/java/frc/robot/utilities/BeakXBoxController.java>`_.
In the file that opens, select all and copy. Now, in your `robot` folder, create a new folder and call it `utilities`.
From here, right-click on the utilities folder, and click "New File". Name the file `BeakXBoxController.java`
(watch your capitalization!), and press enter. Now, delete whatever may be in the new file, and then
press `Ctrl+V` to paste the BeakXBoxController class. You have successfully created your controller!
