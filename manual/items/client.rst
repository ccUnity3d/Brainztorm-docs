###############
Items Unity SDK
###############

**********
How to use
**********
For using this module, first you need activate it in `Brainztorm Settings Menu`_. 
After, in your code you can access the static members through the provided class 
:code:`Brainztorm.Items`.

.. note::

    For debugging purposes, it's recommended you activate the Items Log in the core 
    module Logging, through the `Brainztorm Settings Menu`_.

Items module fetches from the server the items information for current user.
If you activated the Items Logging, you can see the entire logs in Unity Console showing the 
initial request and response containing the :code:`GetItems` type as follow:

.. code-block:: javascript

    //Request
    {
        "UUID": "<UUID>",
        "start": true,
        "transactions": [
            {
                "pos": 2,
                "data": {
                    "type": "GetItems"
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
                "type": "GetItems",
                "pos": 2,
                "data": [
                    {
                        "type": "resources",
                        "amount": 20000,
                        "_id": {
                            "$id": "58bdbf6297caff78724f9c63"
                        },
                        "code": {
                            "$id": "548b1b359f30d8ad37e2ca04"
                        },
                        "name": "Gold",
                        "icon": "resource/gold/icon"
                    },
                    {
                        "type": "resources",
                        "amount": 2,
                        "_id": {
                            "$id": "58bdbf6297caff78724f9c64"
                        },
                        "code": {
                            "$id": "560abe2391bb6f1076df8581"
                        },
                        "name": "Rations",
                        "icon": "resource/ration/icon"
                    },
                    {
                        "type": "resources",
                        "amount": 2,
                        "_id": {
                            "$id": "58bdbf6297caff78724f9c65"
                        },
                        "code": {
                            "$id": "560abe2391bb6f1076df8582"
                        },
                        "name": "Thunder",
                        "icon": "resource/thunder/icon"
                    },
                    {
                        "type": "resources",
                        "amount": 0,
                        "_id": {
                            "$id": "58bdbf6297caff78724f9c66"
                        },
                        "code": {
                            "$id": "548b1b359f30d8ad37e2ca05"
                        },
                        "name": "Void Stones",
                        "icon": "resource/void_stone/icon"
                    }
                ]
            }
        ]
    }