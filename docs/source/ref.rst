Quick Reference Guide
======================

This page provides a quick reference for repetitive and menial tasks, naming conventions, etc.

.. _naming:

Naming Conventions
-------------------

In order to keep our code readable and consistent, we use constant, unchanging naming conventions. It's important to follow this to a dime in order to make your code easier to maintain and re-use as a reference for future codebases.

Case Conventions
~~~~~~~~~~~~~~~~~

* Camel case: looks ``likeThisDoes``. The first "word" is uncapitalized, and subsequent "words" have their first letter capitalized.
* Title case: looks ``LikeThisDoes``. All "words" have their first letter capitalized.
* Snake case: looks ``like_this_does``. All "words" are uncapitalized and separated by underscores (``_``).
* Capital snake case: looks ``LIKE_THIS_DOES``. All "words" are fully capitalized and separated by underscores (``_``),

Never Do
~~~~~~~~~

Never do any of these.

* Start variable names with an underscore: ``_variableName``.
   * Not only is this hard to read and make sense of, but many internal variable names used by the Java compiler start with underscores. Therefore, if you start variables with underscores, there's a chance you can mess up the compilation.
* Make class names uncapitalized: ``className`` or ``classname``.
   * Class names are ALWAYS capitalized with title case. This is done to differentiate between variables and their types. For example, if your class name is uncapitalized, then you can end up with declarations like ``private coolCommand m_coolCommand``. To avoid this, use title case!
* Leave no "separation" between "words": ``variablename``.
   * Put simply, this is ugly and unreadable. Separation is necessary to be able to understand fully what a variable is. It's also entirely possible that two variables could have the same letters, and especially in such cases, "separation" between words is necessary.
* Use non-words, abbreviations, or excessive shorthands.
   * Just because it makes sense to you doesn't mean it'll make sense to anyone else. It may be tempting to shorten a variable named ``m_coolNewMotor`` to ``m_cNM``, but nobody except for you will have any clue what it means.
   * Non-words or made up words should never be used, period.
   * However, abbreviation and shorthanding *can* be okay. If a word is relatively long (i.e. ``odometry`` or ``robotDifferentialDrivetrain``), then it's perfectly okay to shorten it (i.e. ``odom`` or ``drivetrain``). Don't be excessive with it though; it must still make some sense to others and yourself.
* Name variables unrelated or nonsensical things.
   * This expands off the previous "don't". If a variable is of a motor, don't name it ``subsystem``. Name it ``turretMotor`` or the like. Generally self explanatory.
   * Also avoid giving variables totally nonsensical things. Never name anything ``bruh`` or ``thing`` or ``idk``. That doesn't even make any sense. The only exception is for quick, one-off debug variables that won't actually make it into the final code. Always check for these debug variables before each push!
* Use names that are too broad or generic.
   * Don't name a motor ``motor``. Be specific. Does it control a turret? Name it ``turretMotor``. Does it control the front left drive motor? Name it ``frontLeftDriveMotor`` (Note that in this case, it's perfectly okay to shorten it to ``FLDriveMotor``, or possibly even ``FLDrive`` or just ``FL`` if it's within a drive subsystem).
   * Don't get too specific, though. You don't need to name the shooter hood adjustment motor something like ``motorOnTheBackOfTheShooterThatAdjustsTheHoodAngle``. Be specific, but be concise.

General Conventions
~~~~~~~~~~~~~~~~~~~~

* Private variables of a subsystem/class: ``m_variableName`` (camel case, with an ``m_`` prefix)
   * Example: ``private double m_targetSpeed;``. This should be done for variables that **only** need to be directly accessed within the subsystem or class. If you need to get/set the variable externally, create getter/setter functions: i.e. ``setTargetSpeed`` and ``getTargetSpeed``.
* Public variables of a subsystem/class: ``VariableName`` (title case, no prefix)
   * Example: ``public double TargetSpeed``. This should generally never be used.
* "Temporary" variables, within a function or algorithm: ``variableName`` (camel case, no prefix)
   * Example: ``double targetSpeed``. This should be used within a function or algorithm to store a variable temporarily. For example, if a function takes in a distance in meters, and you need to change it to centimeters for it to be useful, then you can create a temporary variable; i.e. ``double distanceFeet = Units.metersToFeet(distanceMeters)``. You don't need to specify private or public.
* Constant variables: ``VARIABLE_NAME`` (capital snake case, no prefix)
   * Example: ``private final double DEFAULT_TARGET_SPEED``. Constants are values that should NEVER change during usage of the robot, and only can be changed by redeploying code. This is useful for defaults, PID values, and similar unchanging values. Ensure that it's ``final``, as that will ensure the value can not be reassigned. If the variable is in a subsystem, then make it private; however, if it's within a ``Constants`` file, make sure it's public.

.. _code:

Commonly Used Code
-------------------

A reference for boilerplate, repetitive code we use all the time.

.. _instances:

Instances
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: java

   private static SubsystemName m_instance;

   ...

   public static SubsystemName getInstance() {
      if (m_instance == null) {
         m_instance = new SubsystemName();
      }
      return m_instance;
   }
