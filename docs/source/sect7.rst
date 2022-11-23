Section 7: Subsystems
======================

So far, all of our robot code has been in two files: Robot.java and RobotContainer.java. So far, it's worked well; and it *is* possible to write a functioning robot this way. However, this is a very inefficient and clunky method for creating a robot. Once you have more than one or two motors, it ends up being clunky and wasteful. It's even more clunky and wasteful when you have complicated algorithms, autonomous routines, and dozens of motors, sensors, servos, solenoids, cameras, and everything else!

We solve this fundamental problem with the use of **subsystems**.

What Are Subsystems?
---------------------

A subsystem, in its most literal, etymological form, means "under the system". In this case, the "system" is the robot as a whole. Therefore, a subsystem is a small part of the robot. What a "part" is depends on the robot. Physically, a subsystem is generally a group of related motors, sensors, servos, and solenoids that all work together to control a specific component of the robot. Programming wise, it consists of a group of motor controllers that run these related motors, as well as algorithms that combine the functionality of all of these 

If that made no sense to you, good. If it did make sense, even better. Here are some examples of what a subsystem might look like.

.. note:: 
	TODO: add pictures?

**Drivetrain**: A drivetrain, well, drives a robot! This is *the* universal constant for every competitive FRC robot in existence. It doesn't matter the game or how good the robot is, it has a drivetrain. A drivetrain consists of the following:

* Drive motors: generally 4 or 6, or if using swerve, 8 (4 for driving and 4 for turning individual wheels). Alternatively, `if you're 2481, you use 10 <https://www.chiefdelphi.com/t/roboteers-team-2481-2022-robot-reveal/405919>`_.
* Encoders for the wheels: used for autonomous control and knowing how far the robot has driven.

A drivetrain has rather simple control: driving and turning. In the code, you would implement simple algorithms to run the drive wheels. That's it.

**Shooter**: Used in shooting games to, well, shoot balls. Shooters tend to consist of the following:

* Shooter wheels: generally 1 or 2 sets of wheels. These wheels generally need to be run at a specific speed every time.
* Camera: used to get the distance and angle to the target.
* Hood adjustment: usually a servo or a motor that adjusts the angle of the "hood" of the shooter, allowing for a ball to be shot higher or lower, or farther or closer.

In the code, a shooter subsystem would use the camera to find the correct distance, calculate the speed needed for the shooter motors and the angle needed for the hood, to make a shot, and plug those values into the adjustment motor and shooter motors.
