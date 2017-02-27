############
Localization
############

************
Introduction
************
The Localization module is part of `Brainztorm Core Modules`_. It facilitates the 
internationalization of your game by providing dictionaries for translating its content.
Basically, the dictionaries are JSON files for each language you want to support. These 
JSON files are composed by key-value pairs where *key* is the attribute to be referenced into 
your scripts, and the *value* represents the translation in the corresponding language. 
A common dictionary looks like:

.. code-block:: javascript

    //EmbeddedLocalizationDictionary.json
    {
        "BRAINZTORM_DAILY_MISSIONS_COMPLETED_TEXT": "Completed {0}/{1}",
        "BRAINZTORM_ERROR_ASSET_LOADING": "There was a problem downloading a game file ''{0}''.",
        "BRAINZTORM_ERROR_COMMUNICATION_INVALID_RESPONSE": "Error connecting to the server (Invalid response).",
        "BRAINZTORM_ERROR_COMMUNICATION_NO_INTERNET": "We couldn't reach our server, please check your internet connection",
        ...
    }

As you can see in the above snippet, it is possible to make use of parameter specifiers  
in the *value part* of the dictionary for change the text dynamically.

Localization can be described in this diagram:

.. image:: images/localization_diagram.png

*******
Content
*******
.. toctree::
    :maxdepth: 3

    client.rst
    server.rst

.. _Brainztorm Core Modules: #