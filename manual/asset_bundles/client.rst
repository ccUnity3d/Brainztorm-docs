######################
AssetBundles Unity SDK
######################

`API Reference`_

**********
How to use
**********
For using this module, first you need activate it in `Brainztorm Settings Menu`_. 
After, in your code you can access the static members through the provided class 
:code:`Brainztorm.AssetBundles`.

.. note::

    For debugging purposes, it's recommended you activate the AssetBundles Log in the core 
    module Logging, through the `Brainztorm Settings Menu`_.

During the initialization phase, the module automatically fetch from the server 
the configuration to work with AssetBundles. If you activated the AssetBundles Logging, 
you can see the entire logs in Unity Console showing the initial request and response 
containing the :code:`GetAssetsOptions` type as follow:

.. code-block:: javascript

    //Request
    {
        "UUID": "<UUID>",
        "start": true,
        "transactions": [
            {
                "pos": 6,
                "data": {
                    "type": "GetAssetsOptions"
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
                "type": "GetAssetsOptions",
                "pos": 6,
                "data": {
                    "clean": false,
                    "url": "<URL>/<platform>/",
                    "parallelDownloadsCarrierData": 5,
                    "parallelDownloadsLocalArea": 6
                }
            }
        ]
    }

The respsonse data means:

- **clean**: if AssetBundle cache must be cleaned.
- **url**: address from server hosting the bundles. It has the form *<URL>/<platform>/* where <URL> is the address configured in Admin Tools, and <platform> is the detected current execution platform, e.g., iOS, Android, PC, OSX, Web or Unity<XX>, this last one means you are working on Unity in dev mode, where <XX> is the Unity version you are using.
- **parallelDownloadsCarrierData**: pending.
- **parallelDownloadsLocalArea**: pending.

Using AssetBundles API
======================
:code:`Brainztorm.AssetBundles` provide the following members to interact with the module:

Read-only properties: 

- :code:`Logger`: returns the own logger object for this module.

Methods:

- :code:`ClearCache`: clears asset bundles cache.
- :code:`UnloadAll`: unloads from memory all previously loaded bundles.
- :code:`UnloadBundle`: unload from memory the specified bundle.
- :code:`GetAllAssetBundlesNames`: returns an array with current loaded bundles.