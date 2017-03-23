###############
Items Unity SDK
###############

`API Reference`_

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
                    }
                ]
            }
        ]
    }

The respsonse data means:

- **type**: the item type.
- **amount**: item quantity shown in the game.
- **_id**: user-item relation's identifier in backend database.
- **code**: item code in backend database.
- **name**: item name shown in the game.
- **icon**: path to item icon to show in the game.

Using Items API
===============
:code:`Brainztorm.Items` provide the following members to interact with the module:

Methods:

- :code:`GetItems`, fetches items from server for current user. 
- :code:`SetItem`, increase or decrease the amount of the given item.

.. code-block:: c#

    using UnityEngine;
    using System.Collections.Generic;
    using Brainztorm.ItemsModule.Models;

    public class ExampleClass : MonoBehaviour 
    {
        void Start()
        {
            Brainztorm.Items.GetItems(OnResponseGetItems, false);
        }

        private void OnResponseGetItems(List<ItemData> data)
        {
            Debug.Log("Items count: " + data.Count.ToString());
            //Statements to process data
        }

        private void AddItemAmount(ItemData item, int amountAdded)
        {
            //If amountAdded is negative, it will decrease the item quantity
            Brainztorm.Items.SetItem(
                item.type,
                item.code,
                amountAdded,
                () => {
                    Debug.Log(string.Format("New item amount: {0}", item.amount + amountAdded));
                },
                true
            );
        }
    }

.. _API Reference: #
.. _Brainztorm Settings Menu: #