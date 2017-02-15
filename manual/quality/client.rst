#################
Quality Unity SDK
#################

`API Reference`_

**********
How to use
**********
For using this module, first you need activate it in `Brainztorm Settings Menu`_. 
After, in your code you can access the methods through the provided static class 
:code:`Brainztorm.Quality`.

Get recommended quality
=======================
You can establish recommended quality setting based on per-device characteristics. 
The :code:`GetQuality` method retrieves (from Backend) the quality recommended for gamer's device.

.. code-block:: c#

    using UnityEngine;
    using System.Collections;

    public class ExampleClass : MonoBehaviour {
        Brainztorm.Quality.GetQuality(callback);

        private void callback(int qualityLevel)
        {
            QualitySettings.SetQualityLevel(qualityLevel);
        }
    }

When you use :code:`GetQuality` method, you get a response as follow:

.. code-block:: javascript

    {
        "code": "NoError",
        "data": [
            {
                "type": "GetQuality",
                "pos": 0,
                "data": {
                    "quality": 4,
                    "optimal": 2,
                    "resolution": 0.25,
                    "criticalFpsThreshold": 10
                }
            }
        ]
    }

- **quality**: is the gamer's custom choosen quality.
- **optimal**: is the recommended quality by Brainztorm.
- **resolution**: is the recommended resolution by Brainztorm.
- **criticalFpsThreshold**: 

Set preferred quality
=====================
Gamers can set the quality level overwriting the recommended by Brainztorm. If you choose 
provide your players with this feature, use the :code:`SetQuality` method.

.. code-block:: c#

    //Establish FAST quality
    Brainztorm.Quality.SetQuality(1);

The default behaviour of :code:`SetQuality` method don't send this change to the Server. 
For persisting the chosen quality level in Backend, pass true as 2nd parameter.

.. code-block:: c#

    //Establish FAST quality and persist in backend
    Brainztorm.Quality.SetQuality(1, true);

The quality level is sent to Backend through the Communications module. The typical JSON 
payload looks like: 

.. code-block:: javascript

    Host: demo.brainztorm.com/v1/user/execute/<sessionId>

    {
        "UUID": "<UUID>",
        "start": false,
        "transactions": [
            {
            "pos": 0,
            "data": {
                "quality": 2,
                "type": "SetQuality"
            },
            "elapsedTime": 0
            }
        ]
    }

Quality Profiling
=================
An important feature in Quality module is profiling. By this feature you can get vital 
information about how your game behave across different devices. Profiling consist in 
periodically send data to Backend for you can analize and take actions to improve your game. 
This data include information of frames, scene, criticals, screen resolution and quality level.

You can set the interval in seconds for sending data to Backend through 
*Brainztorm Settings Menu -> Modules -> Quality*. The following image shows a 120 seconds interval.

.. image:: images/settings.png

Each time the interval reaches, it send data to the Server as follow:

.. code-block:: javascript

    Host: demo.brainztorm.com/v1/user/execute/<sessionId>

    {
        "UUID": "<UUID>",
        "start": false,
        "transactions": [
            {
                "pos": 0,
                "data": {
                    "frames": 4073,
                    "time": 120,
                    "type": "SendQuality",
                    "scene": "Demo Quality",
                    "criticals": 0,
                    "resolution": 0.25,
                    "qualityLevel": 2
                },
                "elapsedTime": 0
            }
        ]
    }

.. _API Reference: #
.. _Brainztorm Settings Menu: #