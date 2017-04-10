############
AssetBundles
############

************
Introduction
************
Usually, the assets amount increases considerely when you improve your game over the time, 
making the game size becomes higher. This could have a negative consecuence in users 
motivation to dowload your game due to storage capacitity restrictions across devices. 

The Brainztorm Asset Bundles module is designed to help you with this issue leveraging 
`Unity AssetBundles`_ functionality.

The proposed workflow to work with Asset Bundles is as follows:

1. Build your Asset Bundles as usual like described in `Building AssetBundles`_ guide.
2. Upload your Asset Bundles to a Git repository provider like GitHub, Bitbucket or GitLab.
3. Configure a Webhook in your Git repository to point to a Brainztorm backend.

*******
Content
*******
.. toctree::
    :maxdepth: 3

    server.rst
    client.rst

.. _Unity AssetBundles: https://docs.unity3d.com/Manual/AssetBundlesIntro.html
.. _Building AssetBundles: https://docs.unity3d.com/Manual/BuildingAssetBundles.html