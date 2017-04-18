##################
RateGame Unity SDK
##################

`API Reference`_

**********
How to use
**********
For using this module, first you need activate it in `Brainztorm Settings Menu`_. 
After, in your code you can access the static members through the provided class 
:code:`Brainztorm.RateGame`.

.. note::

    For debugging purposes, it's recommended you activate the Rate Game Log in the core 
    module Logging, through the `Brainztorm Settings Menu`_.


When the user selects an option from the Rate popup, the :code:`NotifyRateAnswer` request 
is enqueued to be sended in the next transaction to the server. This request carries the 
answer the user selects from the Rate popup:

- Rated = 1
- RemindMeLater = 2
- NoThanks = 3

If you activated the Rate Game Logging, you can see the logs in Unity Console showing the 
request and response containing the :code:`NotifyRateAnswer` type as follow:

.. code-block:: javascript

    //Request
    {
        "UUID": "<UUID>",
        "start": false,
        "transactions": [
            {
                "pos": 0,
                "data": {
                    "answer": 1,
                    "type": "NotifyRateAnswer"
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
                "type": "NotifyRateAnswer",
                "pos": 0,
                "data": []
            }
        ]
    }


Using RateGame API
==================
:code:`Brainztorm.RateGame` provide the following members to interact with the module:

Read-only properties: :code:`Logger`.

Methods:

- :code:`TryAskRate`: shows a dialog asking the user to rate the game.

.. code-block:: c#

    using UnityEngine;

    public class ExampleClass : MonoBehaviour 
    {

    }

.. _API Reference: #
.. _Brainztorm Settings Menu: #