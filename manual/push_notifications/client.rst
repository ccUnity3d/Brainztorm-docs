############################
Push Notifications Unity SDK
############################

`API Reference`_

**********
How to use
**********
For using this module, first you need activate it in `Brainztorm Settings Menu`_. 
After, in your code you can access the static members through the provided class 
:code:`Brainztorm.PushNotifications`.

.. note::

    For debugging purposes, it's recommended to activate the PushNotifications Logs in the core 
    module Logging, through the `Brainztorm Settings Menu`_.

Notification ID
===============
The module automatically generates a unique notification ID for current device and sends to 
backend for register in the Push Notifications provider. Below you can see the transaction: 

.. code-block:: javascript

    //Request
    {
        "UUID": "<UUID>",
        "start": true,
        "transactions": [
            {
                "pos": 8,
                "data": {
                    "notificationId": "<NOTIFICATION_ID>",
                    "type": "RegisterNotificationId"
                },
                "elapsedTime": 0
            }
        ]
    }

    //Response
    {
        "code": "NoError",
        "data": [
            {
                "type": "RegisterNotificationId",
                "pos": 8,
                "data": []
            }
        ]
    }

The response no returns data.

Using Push Notifications API
============================
:code:`Brainztorm.PushNotifications` provide the following members to interact 
with the module:

Read-only property :code:`NotificationID`, retrieves the unique ID for the game 
in the current device.

Methods:

- :code:`Ready`: for executing instructions after module is completely ready.
- :code:`Subscribe`: attach listeners to module events.
- :code:`Unsubscribe`: detach listeners previously attached to event manager.

Event types:

- :code:`OnReady`: executes when module is completely loaded.
- :code:`OnRegistered`: if the request for register the Notification ID is successfully.
- :code:`OnError`: if registration request responses with error.

We strongly recommend to take advantage of the Ready method to access the module properties. 
This ensure the response from server is done and the module has properly set its members. 
Take a look at the following example:

.. code-block:: c#

    using UnityEngine;
    using System.Collections;
    using BzPushNotifications = Brainztorm.PushNotifications;

    public class ExampleClass : MonoBehaviour 
    {
        BzPushNotifications.Ready(OnPushNotificationsReady);

        private void OnPushNotificationsReady()
        {
            Debug.Log("Notification ID is: " + BzPushNotifications.NotificationID);
        }
    }

.. _API Reference: #
.. _Brainztorm Settings Menu: #
