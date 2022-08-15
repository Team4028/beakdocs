Section 3: Servos & Solenoids
==============================

.. _what:

What are Servos & Solenoids?
-----------------------------

Servos are a type of very basic motor. They can have a linear or rotational movement pattern, and are designed
to go to a position (to "servo" to a position) and stay there with high amounts of force. These are typically used
for shooter hoods, or for small-scale, low-power rotation of arms or other limbs.

Solenoids control pneumatics systems. Pneumatics are used to control "cylinders", which are linear actuators with two
states: fully extended, or fully retracted. Because they use compressed air to transfer force, they can generally provide
enough force to move an object that a motor can't. They are solely used for two-state systems, i.e. an infeed or a hook.

.. _servocode:

Servos in Code
---------------

Servos are extremely simple to use--using them is identical to running a basic motor. First, create your servo variable
at the top of Robot.java:

.. code-block:: java

    Servo servoMotor;

Now we instantiate our servo. Much like a motor, the servo constructor takes a single argument: the PWM ID. Check the RIO's
PWM ports, and trace the servo you want to control to the PWM port it uses, and plug this in (in robotInit):

.. code-block:: java

    servoMotor = new Servo(0);

Controlling servos is just like a motor as well, although the "percent output" is really the position to set the servo to.
Servos generally have a hard minimum or maximum position. On 4028, the servos we use generally have a range of 0.2-1.0.
Because of this, if you want to go to the "zero" position, you must set the servo to 0.2. In teleopInit:

.. code-block:: java

    servoMotor.set(0.2);

Deploy and enable as described in the last section. The servo should be fully retracted after a while.

Now let's try to fully lengthen it. Replace the 0.2 with 1.0, deploy, and enable. It should go to the fully
lengthened position.

.. _solenoidcode:

Solenoids in Code
------------------

Solenoids are even simpler than solenoids. They are simple binary actuators: they only have a true and false state.
Double solenoids are slightly different, with forward, reverse, and off states. However, they both accomplish the same
thing: to either retract or extend a pneumatic cylinder (see the Pneumatics link in the sidebar).

As always, create your solenoid variable and instantiate it. At the top of the Robot class:

.. code-block:: java

    Solenoid solenoid;

The Solenoid constructor takes two arguments: the pneumatic hub type (this is either `PneumaticsModuleType.CTREPCM`
or `PneumaticsModuleType.REVPH`. Ask a veteran member for help determing which to use), and the channel. For now, we are
only using single solenoids. Trace the solenoid you want to control back to the PCM or PH, and find its port. Use this port
in your constructor (robotInit):

.. code-block:: java

    solenoid = new Solenoid(PneumaticsModuleType.CTREPCM, 0);

Replace 0 with the port you determined.

To set a solenoid, we simply call `solenoid.set()`. This call takes one argument: true or false.
The default state of a solenoid is false; so, to see a difference, you will want to set this to `true`
(teleopInit):

.. code-block:: java

    solenoid.set(true);

Now, deploy and enable. You should hear a small click and the solenoid will light up.
