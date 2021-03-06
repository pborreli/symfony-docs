Luhn
======

This constraint is used to ensure that a credit card number passes the `Luhn algorithm`_.
It is useful as a first step to validating a credit card: before communicating with a
payment gateway.

+----------------+-----------------------------------------------------------------------+
| Applies to     | :ref:`property or method<validation-property-target>`                 |
+----------------+-----------------------------------------------------------------------+
| Options        | - `message`_                                                          |
+----------------+-----------------------------------------------------------------------+
| Class          | :class:`Symfony\\Component\\Validator\\Constraints\\Luhn`             |
+----------------+-----------------------------------------------------------------------+
| Validator      | :class:`Symfony\\Component\\Validator\\Constraints\\LuhnValidator`    |
+----------------+-----------------------------------------------------------------------+

Basic Usage
-----------

To use the Luhn validator, simply apply it to a property on an object that
will contain a credit card number.

.. configuration-block::

    .. code-block:: yaml

        # src/Acme/SubscriptionBundle/Resources/config/validation.yml
        Acme\SubscriptionBundle\Entity\Transaction:
            properties:
                cardNumber:
                    - Luhn:
                        message: Please check your credit card number.

    .. code-block:: xml

        <!-- src/Acme/SubscriptionBundle/Resources/config/validation.xml -->
        <class name="Acme\SubscriptionBundle\Entity\Transaction">
            <property name="cardNumber">
                <constraint name="Luhn">
                    <option name="message">Please check your credit card number.</option>
                </constraint>
            </property>
        </class>

    .. code-block:: php-annotations

        // src/Acme/SubscriptionBundle/Entity/Transaction.php
        use Symfony\Component\Validator\Constraints as Assert;

        class Transaction
        {
            /**
             * @Assert\Luhn(message = "Please check your credit card number.")
             */
            protected $cardNumber;
        }

    .. code-block:: php

        // src/Acme/SubscriptionBundle/Entity/Transaction.php
        use Symfony\Component\Validator\Mapping\ClassMetadata;
        use Symfony\Component\Validator\Constraints\Luhn;

        class Transaction
        {
            protected $cardNumber;

            public static function loadValidatorMetadata(ClassMetadata $metadata)
            {
                $metadata->addPropertyConstraint('luhn', new Luhn(array(
                    'message' => 'Please check your credit card number',
                )));
            }
        }

Available Options
-----------------

message
~~~~~~~

**type**: ``string`` **default**: ``Invalid card number``

The default message supplied when the value does not pass the Luhn check.

.. _`Luhn algorithm`: http://en.wikipedia.org/wiki/Luhn_algorithm