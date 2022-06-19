Section 3: Servos, Solenoids, & Controllers
============================================

.. _what:

What are Servos & Solenoids?
-----------------------------

Servos are a type of very basic motor. They can have a linear or rotational movement pattern, and are designed
to go to a position (to "servo" to a position) and stay there with high amounts of force. These are typically used
for shooter hoods, or for small-scale, low-power rotation of arms or other limbs.

Solenoids control pneumatics systems. Pneumatics are used to control "cylinders", which are linear actuators with two
states: fully extended, or fully retracted. Because they use compressed air to transfer force, they can generally provide
enough force to move an object that a motor can't. They are solely used for two-state systems, i.e. an infeed or a hook.

.. _code:

Servos & Solenoids in Code
---------------------------

.. note:: 
    Servo servo = new Servo(0);

    m_operatorController.a.whenPressed(() -> servo.set(0.5));
