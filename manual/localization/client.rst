######################
Localization Unity SDK
######################

`API Reference`_

**********
How to use
**********
This is a core module, so you don't need activate it before using, it is out the box. 
A :code:`Brainztorm.Localization` class is provided for accessing the static members.

.. note::

    For debugging purposes, it's recommended you activate the Localization Log in the core 
    module Logging, through the `Brainztorm Settings Menu`_.

Initial loading
===============
During module initialization, it automatically loads a default "EN" dictionary embebed locally.
Next, it fetch from the server the localization data based on current device language configuration.
If you activated the Localization Logging, you can see the entire logs in Unity Console showing the 
initial request and response containing the :code:`GetLocaleOptions` type as follow:

.. code-block:: javascript

    //Request
    {
        "UUID": "<UUID>",
        "start": true,
        "transactions": [
            {
            "pos": 5,
            "data": {
                "language": "EN",
                "type": "GetLocaleOptions"
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
                "type": "GetLocaleOptions",
                "pos": 5,
                "data": {
                    "url": "https://brainztorm-l10n.s3.amazonaws.com/EN/default-584b2013a9040.json",
                    "urlFallback": "https://brainztorm-l10n.s3.amazonaws.com/EN/default-584b2013a9040.json",
                    "hash": "cfd9026257f0c51c",
                    "defaultUrl": "https://brainztorm-l10n.s3.amazonaws.com/EN/default-584b2013a9040.json",
                    "defaultUrlFallback": "https://brainztorm-l10n.s3.amazonaws.com/EN/default-584b2013a9040.json",
                    "defaultHash": "cfd9026257f0c51c",
                    "flush": false
                }
            }
        ]
    }

The respsonse data means:

- **url**: 
- **urlFallback**: 
- **hash**: 
- **defaultUrl**: 
- **defaultUrlFallback**: 
- **defaultHash**: 
- **flush**: 

Using Localization API
======================
:code:`Brainztorm.Localization` provide the following members to interact with the module:

Read-only property :code:`CurrentLocale` for retrieving the current locale.

Methods:

- :code:`TranslateKey`: traslate a key.
- :code:`Ready`: for executing instructions after module is completely ready.
- :code:`Subscribe`: attach listeners to module events.
- :code:`Unsubscribe`: detach listeners previously attached to event manager.

Event types:

- :code:`OnReady`: executes when module is completely loaded.
- :code:`OnGotLanguageData`: fired after language file has been downloaded from server.

We strongly recommend take advantage of Ready method for accessing the module properties. 
This ensure the response from server is done and the module has set the current quality 
and resolution. Look the following example:

.. code-block:: c#

    using UnityEngine;
    using System.Collections;
    using BzLocalization = Brainztorm.Localization;

    public class ExampleClass : MonoBehaviour 
    {
        BzLocalization.Ready(OnLocalizationReady);

        private void OnLocalizationReady()
        {
            Debug.Log("Current Locale is: " + BzLocalization.CurrentLocale);
            Debug.Log("KEY: " + BzLocalization.TranslateKey("KEY"));
        }
    }

.. _API Reference: #
.. _Brainztorm Settings Menu: #