BeakLib
========

BeakLib is the "official" team library of The Beak Squad.

.. _features:

Features
---------

* Vendor-agnostic motor controllers (same API for Talons and Spark MAXes)
* Base drivetrain classes to make configuring drivetrains easier than ever (includes swerve)
* Built-in path following support
* Unit classes to reduce conversion confusion and express parameters as their unit

.. _usage:

Using BeakLib
--------------

BeakLib's features can significantly increase the expressiveness of your code, reduce confusion, and make code changes significantly easier. Let's demonstrate with this example flywheel subsystem with velocity ccontrol:

.. code-block:: java

	public class Flywheel extends SubsystemBase {
		private WPI_TalonSRX m_motor;

		/** Creates a new Flywheel. */
		public Flywheel() {
			m_motor = new WPI_TalonSRX(16);

			m_motor.configFactoryDefault();

			m_motor.config_kF(0, 0.02);
			m_motor.config_kP(0, 0.5);
			m_motor.config_kD(0, 5.);
		}

		public void setVelocity(double rpm) {
			m_motor.set(ControlMode.Velocity, rpm * 4096. / 600.);
		}

		public void setPercent(double percent) {
			m_motor.set(ControlMode.PercentOutput, percent);
		}
	}

Although this code does make some sense, there are several inefficiencies. For example, why can't we configure all PIDF values at once? Let's fix several of these problems with BeakLib. By using BeakLib, we can improve our subsystem code:

.. code-block:: java

	public class Flywheel extends SubsystemBase {
		private BeakTalonSRX m_motor;

		/** Creates a new Flywheel. */
		public Flywheel() {
			m_motor = new BeakTalonSRX(16);

			m_motor.restoreFactoryDefault();

			m_motor.setPIDF(0.5, 0, 5., 0.02, 0);
		}

		public void setVelocity(AngularVelocity velocity) {
			m_motor.setVelocityRPM(velocity.getAsRotationsPerMinute(), 0);
		}

		public void setPercent(double percent) {
			m_motor.set(percent);
		}
	}

Let's break down the changes.

``WPI_TalonSRX`` has been replaced by ``BeakTalonSRX``. This allows us to use the new BeakLib features on the motor.

The lines:

``m_motor.config_kF(0, 0.02);``
``m_motor.config_kP(0, 0.5);``
``m_motor.config_kD(0, 5.);``

Have all been replaced by the line ``m_motor.setPIDF(0.5, 0, 5., 0.02, 0);``. This configures ALL PID values at once!

The parameter for ``setVelocity`` has been changed to an ``AngularVelocity``. Rather than expecting users to pass in a value as an RPM value, users can instead pass in an ``AngularVelocity`` than can be constructed from any variety of units; for example, you can call ``flywheel.setVelocity(AngularVelocity.fromRotationsPerSecond(100));`` if you have a rotations-per-second value.

Rather than manually converting the passed-in value for RPM, motor controllers with BeakLib have built-in methods to use sensible units like rotations and velocity, along with native units. Before, we had to call ``m_motor.set(ControlMode.Velocity, rpm * 4096. / 600.);``. But with BeakLib, we can instead simply call ``m_motor.setVelocityRPM(velocity.getAsRotationsPerMinute(), 0);``. The ``setVelocityRPM`` value natively takes in an RPM value, and doesn't require to pass in a "control mode"; rather, velocity, position, percent output, voltage, and "smart" motion all have discrete methods!

We've now simplified our code, but what if we want to switch the motor controller type?

.. _vendors:

Vendor-Agnostic Motor Controllers
----------------------------------

Say we end up changing our flywheel subsystem to a NEO. With normal CTRE code, we'd have to completely change to REV's different API; but with BeakLib, *all* we have to do is change ``BeakTalonSRX`` to ``BeakSparkMAX``:

.. code-block:: java

	public class Flywheel extends SubsystemBase {
		private BeakSparkMAX m_motor;

		/** Creates a new Flywheel. */
		public Flywheel() {
			m_motor = new BeakSparkMAX(16);

			m_motor.restoreFactoryDefault();

			m_motor.setPIDF(0.5, 0, 5., 0.02, 0);
		}

		public void setVelocity(AngularVelocity velocity) {
			m_motor.setVelocityRPM(velocity.getAsRotationsPerMinute(), 0);
		}

		public void setPercent(double percent) {
			m_motor.set(percent);
		}
	}

That's it!

.. _installing:

Installing BeakLib
-------------------

Our current base code already has BeakLib installed.

todo
