Introduction
============

It provides an interface for managing users and their devices to record useful
information for managing a game, recording data such as:

- Information about the device log on to the game.
- Unification of devices for social networking.
- Location by device user.
- Life time a user and their history logins.
- Registration logs of a device in the game.
- Management of banned users.
- Resource management game to a user.
- State of other modules such as:
 - Achievements
 - Resources
 - Store
 - Issues
 - Inbox

Devices
-------
When you log into the game devices are sending all the information of the mobile
device hardware server Brainztorm linking it to a user.

.. image:: images/devices.png

The information stored in the device are:

- *UUID*: The Universal Unique Identifier of the mobile device.
- *Platform*: Is dispotiivos mobile operating system, such as iOS, Android and default is Editor.
- *Device Model*: The model registered device, such as iPhone 6.
- *OS Version*: The version of the mobile operating system.
- *Locale*: The language you have set up the operating sitema having the mobile device.
- *Build*: The build number that has regsitrado the game, with this information you can look that version of the game has every mobile device.
- *Notification ID*: The unique code to send push notifications to mobile device.
- *Quality*: The quality of images that have the game on the mobile device.

.. image:: images/devices2.png

Social Networks
---------------
Devices that belong to a user and are connected to a social network such as
Google Play, Grame Center or Facebook, send information from your social network
and connects the user accounts that through your social network can a user have
multiple devices and not lose your progress in the game.

Validators
----------
If the execution environment is not production, input and output data is validated in every transaction.
The validation is performed using a JSON Schema. All listeners should specify a validator class in an
annotation @Validation (class=<validator class>) at the class level. That validator class should implement
the TransactionValidator interface, which defines methods getInputSchema for validating input values and
getOutputSchema for validating output values, they expect as return an array with the expected JSON schema fields,
their types and whether they are required among other possibilities.

The following is an example of a listener alongside its validators:

.. code-block:: php

  <?php

  namespace MyGame\Listeners;

  use Brainztorm\Transactions\TransactionListener;
  use Brainztorm\Transactions\TransactionValidator;

  /**
   * StorePlayerStatusListener
   *
   * Allows to update a player status
   *
   * @Validation(class=this)
   */
  class StorePlayerStatusListener extends TransactionListener implements TransactionValidator
  {
     /**
      * Returns a JSON-schema structure to validate the input of this transaction
      */
     public function getInputSchema()
     {
         return [
             'type' => 'object',
             "properties" => [
                 "playerId"    => ["type" => "string"],
                 "progress"  => ["type" => "integer"]
             ],
             "required" => ["player", "progress"]
         ];
     }

     /**
      * Returns a JSON-schema structure to validate the output of this transaction
      */
     public function getOutputSchema()
     {
         return [];
     }

     /**
      * Listener implementation
      *
      */
     public function execute($event, $executor, $data)
     {
         // ...
     }
  }
