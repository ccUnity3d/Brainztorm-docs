###############
Users Unity SDK
###############

`API Reference`_

**********
How to use
**********
It's a core module so it doesn't need to be activated, its functionality is provided 
by default. A :code:`Brainztorm.Users` class is provided for accessing the static members.

.. note::

    For debugging purposes, it's recommended to activate the Users Logs in the core 
    module Logging, through the `Brainztorm Settings Menu`_.

Once the session starts, a transaction request called :code:`GetUserData` is sent together 
with the :code:`TransactionStarter`. The transaction starter contains the device's UUID and 
social network ids if any is available; as well as the last user id used in this device. 
The server searches for users linked with network ids, if none is found it tries to find 
one that is linked to the current UUID. If the server fails to find a matching user, 
creates one and links it to the UUID.

.. image:: images/linking.png

If you activated the Users Logging, you can see the entire logs in Unity Console showing the 
initial request and response containing the :code:`GetUserData` type as follow:

.. code-block:: javascript

	//Request
	{
		"UUID": "<UUID>",
		"start": true,
		"transactions": [
			{
				"pos": 2,
				"data": {
					"type": "GetUserData"
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
				"type": "GetUserData",
				"pos": 2,
				"data": {
					"sessionId": "bzfbe34ae84163f916d2cb",
					"publicId": "19fb8bf8e9185170f844c2c0774983e8",
					"userName": "",
					"hashProfile": ""
				}
			}
		]
	}

If for any reason, the server finds an user conflict, a resolution screen is shown to 
the player and the dismissed user is errased.

.. image:: images/conflict.png

Using Users API
===============
:code:`Brainztorm.Users` provide the following members to interact with the module:

Read-only properties: :code:`SessionId`, :code:`PublicId`, :code:`Name`, 
:code:`HasChanged`, :code:`IsRegistered` and :code:`Logger`.

Methods:

- :code:`UpdateName`: allows to change the user name.
- :code:`RegisterUser`: call to backend to register the current user.
- :code:`RemoveUser`: call to backend to remove the current user.

Events:

- :code:`OnSetup`: triggered when *GetUserData* request is complete and successful.
- :code:`OnChangedName`: occurs after :code:`UpdateName` execution is successful.

Getting the User IDs
--------------------
You can get the current user IDs using the :code:`SessionId` and :code:`PublicId` properties:

.. code-block:: c#

    using UnityEngine;
    using System.Collections;
    using BzUsers = Brainztorm.Users;

    public class ExampleClass : MonoBehaviour 
    {
        void Start()
        {
            Debug.Log("The User SessionId is: " + BzUsers.SessionId);
            Debug.Log("The User PublicId is: " + BzUsers.PublicId);
        }
    }

The server knows the user id after the session is stablished, and neither transactions 
nor variables module need this id on your data files to keep track of them.

Username
--------
You can prompt users to change their username at any time, you can do so through the 
*IUserNameChanger* interface. If the player has a previously created username, 
this will be set as default value. Otherwise, the last linked social network id will 
be used as default.

.. code-block:: c#

  [Inject]
  private IUserNameChanger usernameChanger;

  private void PromptForUserName()
  {
    usernameChanger.Show(ContinueTutorial, SetGenericName);
  }

  private void ContinueTutorial()
  {
    //...
  }

  private void SetGenericName()
  {
    //...
  }

The username popup checks different criteria such as duplicated names or profanity filters 
to validate the current name, this happens after the user stops typing for a small amount 
of time or once the submit button is pressed.

.. image:: images/sdk-profanity-true.png

.. image:: images/sdk-profanity-false.png

The appropriate callback will be invoked once the username popup is dismissed.

Profanity Filter
^^^^^^^^^^^^^^^^
Usernames, as well as other features, is constrained by a profanity filter. This filter defines a set of forbidden expressions which can't be used in game.
You can find this useful for brands or offensive words that could get the game rejected from application stores.

Social Networks
^^^^^^^^^^^^^^^
You can link social networks to user's game profile, doing so allows them to keep their progress on different
scenarios:

- Uninstalling and re-installing game again.
- One user using many devices.
- One device used by many users.

Also, you can access this information through the **ISocialManager** interface.

.. code-block:: c#

  [Inject]
  private ISocialManager social;

  private void LogNetworkData()
  {
      // Logs username on the selected social network
      Debug.Log(social.UserInfo.UserName);

      // Logs the unique networkId on the selected social network
      Debug.Log(social.UserInfo.NetworkId);

      Texture2D avatar = social.UserInfo.Avatar;
      // Show avatar
  }
