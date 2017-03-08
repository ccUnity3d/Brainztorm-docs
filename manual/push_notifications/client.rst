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

Attributes:
- :code:`NotificationId`, read-only, retrieves an string with an unique ID 
to register the current device in the Push Notifications Server.
- :code:`IsRegistered`, read-only boolean to check the registration status.

.. Methods:
..
- :code:`Ready`: for executing instructions after module is completely ready.
- :code:`Subscribe`: attach listeners to module events.
- :code:`Unsubscribe`: detach listeners previously attached to event manager.

Events:
.. - :code:`OnReady`: executes when module is completely loaded.

- :code:`OnRegistered`: if the request for register the Notification ID is successfully.
- :code:`OnError`: if registration request responses with error.

In the following example, let's get the Notification ID using the :code:`OnRegistered` event:

.. code-block:: c#

    using UnityEngine;
    using System.Collections;
    using BzPushNotifications = Brainztorm.PushNotifications;

    public class ExampleClass : MonoBehaviour 
    {
        BzPushNotifications.OnRegistered += LogSuccess;
        BzPushNotifications.OnError += LogError;

        private void LogSuccess(string id)
        {
            Debug.Log("Notification ID is: " + id);
        }

        private void LogError(string id)
        {
            Debug.LogError("Notification ID registration error.");
        }
    }

.. _API Reference: #
.. _Brainztorm Settings Menu: #
