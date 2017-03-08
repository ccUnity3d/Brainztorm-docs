######################
Localization Unity SDK
######################

`API Reference`_

**********
How to use
**********
It's a core module so it doesn't need to be activated, its functionality is provided 
out-of-the-box. A :code:`Brainztorm.Localization` class is provided for accessing the 
static members.

.. note::

    For debugging purposes, it's recommended to activate the Localization Logs in the core 
    module Logging, through the `Brainztorm Settings Menu`_.

Initial loading
===============
During module initialization, it automatically loads a default "EN" dictionary embedded locally. 
Next, it fetches from the server the localization data based on current language device 
configuration. If you've activated the Localization Logging, you can see the entire logs 
in Unity Console showing the  initial request and response including the 
:code:`GetLocaleOptions` type as follow:

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

The response data means:

- **url**: the URL to the requested language dictionary.
- **urlFallback**: if dictionary cannot be downloaded from *url*, retry download from *urlFallback*.
- **hash**: to compare internally if requested dictionary has changed.
- **defaultUrl**: the URL to the default language dictionary.
- **defaultUrlFallback**: if dictionary cannot be downloaded from *defaultUrl*, retry download from *defaultUrlFallback*.
- **defaultHash**: to compare internally if default dictionary has changed.
- **flush**: it especify if dictionaries must be flushed.

Using Localization API
======================
:code:`Brainztorm.Localization` provide the following members to interact with the module:

Read-only properties:

- :code:`CurrentLanguage` for retrieving the current language.
- :code:`DefaultLanguage` for retrieving the default language.
- :code:`IsReady` returns :code:`true` if module is completely load, :code:`false` otherwise.

Methods:

- :code:`Localize`: translate a key.

Events:

- :code:`OnReady`: executes when module is completely loaded.
.. - :code:`OnGotLanguageData`: fired after language file has been downloaded from server.

We strongly recommend to take advantage of the OnReady event to access the module properties. 
This ensure the response from server is done and the module has properly set its members. 
Take a look at the following example:

.. code-block:: c#

    using UnityEngine;
    using System.Collections;
    using BzLocalization = Brainztorm.Localization;

    public class ExampleClass : MonoBehaviour 
    {
        BzLocalization.OnReady += OnLocalizationReady;

        private void OnLocalizationReady()
        {
            Debug.Log("Current Language is: " + BzLocalization.CurrentLanguage);
            Debug.Log("Default Language is: " + BzLocalization.DefaultLanguage);

            //Translate a Brainztorm built-in key
            Debug.Log("BRAINZTORM_ERROR_GENERIC: " + BzLocalization.Localize("BRAINZTORM_ERROR_GENERIC"));
        }
    }

.. _API Reference: #
.. _Brainztorm Settings Menu: #
