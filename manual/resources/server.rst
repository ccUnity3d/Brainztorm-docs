Server Resources
============

Introduction
------------

Provides an interface to manage resources. This module is integrated with the following components:

 - Initial Resources
 - User Resources

Initial Resources
^^^^^^^^^^^^^^^^^^
Provides an interface to manage resources that will be used in the game.

.. image:: images/resources.png

The available fields are:

- *Code*: Unique Identifier of the resource.
- *Name*: Name of the resource.
- *Start Amount*: Amount of the resource to start the game.
- *Maximum Amount*: Maximum Amount of the resource in the game.
- *Free Transfer*: Allow to transfer this resource to other player.
- *Tags*: List of tags to customize the resource.
- *Icon*: Assets that represent the resource.
- *Mesh*: Assets that represent the resource in 3D.

Add a new Resource
------------------

.. image:: images/resources.png

We can "Add" a a new resource in the game. When you do it a new empty record is added in the last position of the list. 

.. image:: images/new.png

When you finish adding the information, press "Publish" to save the new resource.

.. image:: images/success.png

Edit a Resource
------------------

.. image:: images/resources.png

When you select a resource and edit the information, you need to "Publish" in order to save the changes.

.. image:: images/success.png

Delete a Resource
------------------

.. image:: images/delete.png

In order to delete a resource, you can expand it's info display and click the red "x" button. Then save changes pressing "Publish".

User Resources
^^^^^^^^^^^^^^^

Provides an interface to manage user resources in the game. Please see the `Users <../users/server.rst>`__ .

.. image:: ../users/images/resources.png

The available fields are:

- *Code*: Code to represent the resource.
- *Tags*: Tags to group the resources.
- *Amount*: Amount of the resource.
- *Maximum Amount*: Maximum amount of the resource.
