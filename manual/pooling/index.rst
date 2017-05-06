#######
Pooling
#######

************
Introduction
************
A good game isn't only pretty art and engaging gameplay. You have to accomplish the 
best performance and generally you want to ensure a high efficiency in the 
major number of devices availables in the market. Each decision in design and technical 
approach have their respective impact in the game performance, therefore, it's 
important to choose those ones having the minimal impact in hardware computation.

One of the aspects that you have to be more careful in Unity is Creating and 
instantiating GameObjects. The following table taken from the Unity's Unite 2016 
conference: `Let's Talk (Content) Optimization`_, shows the times to perform some 
common tasks like Create, Load and Clone assets in iOS:

=======  ==========  =================  ==============  ===========  =========
Task     Total Time  Spawn GameObjects  Add Components  Reparenting  Remainder
=======  ==========  =================  ==============  ===========  =========
Create   583ms       135ms              403ms           30ms         15ms
Load     1366ms      134ms              0ms             0ms          1232ms
Clone    188ms       175 / 112ms        0 / 63ms        0 / 2ms      13ms
=======  ==========  =================  ==============  ===========  =========

From previous table, we can conclude that Creating and Loading GameObjects is 
expensive, the situation is turning worst because this is a common repetitive task. 
A common technic to deal with this is known as `Object Pooling`_. Brainztorm 
implements a Pooling mechanism that you can use to improve performance in your games.

*******
Content
*******
.. toctree::
    :maxdepth: 3

    client.rst

.. _`Let's Talk (Content) Optimization`: https://www.youtube.com/watch?v=n-oZa4Fb12U
.. _Object Pooling: https://unity3d.com/es/learn/tutorials/topics/scripting/object-pooling