############
Leaderboards
############

************
Introduction
************
Leaderboards is a module to show the top rank of the current user in the world, country and friends of social networks.

This module use the messaging pattern `Publish–subscribe`_ allowing to use a realtime messaging with great scalability.

Using the localization information of all users and know the country by the IP of the devices, Brainztorm group all the 
users by country and show in real time the ranking position.

*******
Content
*******
.. toctree::
    :maxdepth: 3

    server.rst
    client.rst
    
.. _Publish–subscribe: https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern
