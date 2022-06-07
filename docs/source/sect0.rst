Section 0: WPILib & Vendor installation
=====

.. _WPILib:

WPILib
------------

To install WPILib, you can either use a USB flash drive (ask from an experienced Controls member for help),
or install from the `WPILib GitHub <https://github.com/wpilibsuite/allwpilib/releases/latest/>`_.

Finish this part

.. code-block:: java

   public void coolFunction() {
       System.out.println("Hi");
   }

.. _CTRE:

CTRE
-----

Phoenix tuner & framework

Creating recipes
----------------

To retrieve a list of random ingredients,
you can use the ``lumache.get_random_ingredients()`` function:

.. autofunction:: lumache.get_random_ingredients

The ``kind`` parameter should be either ``"meat"``, ``"fish"``,
or ``"veggies"``. Otherwise, :py:func:`lumache.get_random_ingredients`
will raise an exception.

.. autoexception:: lumache.InvalidKindError

For example:

>>> import lumache
>>> lumache.get_random_ingredients()
['shells', 'gorgonzola', 'parsley']
