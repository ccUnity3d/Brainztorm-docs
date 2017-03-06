###############
Inbox Unity SDK
###############

`API Reference`_

**********
How to use
**********
For using this module, first you need activate it in `Brainztorm Settings Menu`_. 
After, in your code you can access the static members through the provided class 
:code:`Brainztorm.Inbox`.

.. note::

    For debugging purposes, it's recommended to activate the Inbox Logs in the core 
    module Logging, through the `Brainztorm Settings Menu`_.

Get Unread Inbox
================
When the module begins, it automatically fetches the backend for unread messages, 
if you have enabled the Communication Logging, you can find in the transaction Log 
the respective request and response as follows:

.. code-block:: javascript

    //Request
    {
        "UUID": "<UUID>",
        "start": true,
        "transactions": [
            {
                "pos": 8,
                "data": {
                    "type": "GetUnreadInbox"
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
                "type": "GetUnreadInbox",
                "pos": 8,
                "data": {
                    "count": 4
                }
            }
        ]
    }

As you can see in the response fragment above, the *count* data refers to the  
unread messages quantity. In this example, 4 unread messages were found.

Using Inbox Messages API
========================
:code:`Brainztorm.Inbox` provide the following members:

Methods:

- :code:`Ready`: for executing instructions after module is completely ready.

Event types:

- :code:`OnReady`: executes when module is completely loaded.

We strongly recommend to take advantage of the Ready method to access the module properties. 
This ensure the response from server is done and the module has properly set its members. 
Take a look at the following example:

.. code-block:: c#

    using UnityEngine;
    using System.Collections;
    using BzInbox = Brainztorm.Inbox;

    public class ExampleClass : MonoBehaviour 
    {
        BzInbox.Ready(OnInboxReady);

        private void OnInboxReady()
        {
            Debug.Log("You have " + BzInbox.GetUnreadInbox() + " unread messages.");
        }
    }

.. _API Reference: #
.. _Brainztorm Settings Menu: #
