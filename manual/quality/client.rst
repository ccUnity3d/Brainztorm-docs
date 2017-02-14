Client Quality
=====================

Introduction
------------
The Quality module laverage Unity `Quality Settings`_ for easily monitors game performance 
and change settings on the fly based on a per-device profiling. Quality sets the 
game's visual performance, avoiding the complexity from managing many screen sizes, 
resolutions, graphics cards, memory and other particular characteristics from each brand 
of consoles or mobile devices. This module offers you a straightforward manner to establish 
default quality parameters, let players to choose their preferred visual quality and 
even more important, improve your game, taking decisions based on device profiles.

How to use
----------
For using this module, first you need activate it in `Brainztorm Settings Menu`_. 
After, in your code you can access the methods through the provided static class 
:code:`Brainztorm.Quality`.

Get recomended quality
~~~~~~~~~~~~~~~~~~~~~~
You can establish recommended quality setting based on per-device characteristics. 
The :code:`GetQuality` method retrieves (from Backend) the quality recommended for gamer's device.

.. code-block:: c#

    using UnityEngine;
    using System.Collections;

    public class ExampleClass : MonoBehaviour {
        Brainztorm.Quality.GetQuality();

        private void callback(int qualityLevel)
        {
            QualitySettings.SetQualityLevel(qualityLevel);
        }
    }

Set preferred quality
~~~~~~~~~~~~~~~~~~~~~
Gamers can set the quality overwriting the recommended by Brainztorm. If you choose provide 
your players with this feature, use the :code:`SetQuality` method.

.. code-block:: c#

    //Establish FAST quality
    Brainztorm.Quality.SetQuality(1);

    //For persisting this change in Backend, pass true as 2nd parameter
    Brainztorm.Quality.SetQuality(1, true);

Quality Profiling
~~~~~~~~~~~~~~~~~
An important feature in Quality module is profiling. By this feature you can get vital 
information about how your game behave across different devices. Profiling consist in 
periodically send data to Backend for you can analize and take actions to improve your game. 
This data include information of frames, scene, criticals, screen resolution and quality level.

You can set the interval in seconds for sending data to Backend through 
*Brainztorm Settings Menu -> Modules -> Quality*. The following image shows a 120 seconds interval.

.. image:: images/settings.png

.. _Quality Settings: https://docs.unity3d.com/Manual/class-QualitySettings.html
.. _Brainztorm Settings Menu: #