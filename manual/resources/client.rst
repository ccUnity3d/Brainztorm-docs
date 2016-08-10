Client Resources
================

Introduction
------------
Games often use currency to purchase in-game goods, unlocking levels or other services. These resources can be collected either through the game itself or purchased with real money.
We offer a way to handle resources transactions for any kind of game, keeping a secure record of every transaction on a player's account and providing integration with other modules.

<introduction graphic>

Configuration
-------------
To use the resources module, you need to enable the installer in the module settings.

<enabled resources module>

Then you need to create your Resources using the admin and once you've done that sync the data structures with the local Resources definition; to do so you can go to the wizard and select the Resources Module.

<wizard button>

Once you've syced the Resources definition, an enumeration containing all your values should be created in your project. It will look something like this:

.. code-block:: c#
  
  public enum Resources
  {
    Gold,
    Thunder,
    Rations
  }

How to use
----------
To interact with the resources component, you can use the *IResourcesInventory* interface.

.. code-block:: c#
  
  public interface IResourcesInventory : IResourcesInventoryBase
  {
    event Action<ResourceType, int> OnChangeAmount;
    
    event Action<ResourceType, int> OnChangeMaximumAmount;
    
    void GetResource(ResourceType resourceType, Action<IResource> callback);
    
    IResource GetResourceNow(ResourceType resourceType);
    
    void Increase(ResourceType resourceType, int increaseAmount);
    
    void Decrease(ResourceType resourceType, int decreaseAmount);
    
    void SetMaximum(ResourceType resourceType, int newMaxAmount);
  }
	
To increase or decrease the amount of a given resource, you need to use the *Increase* or *Decrease* methods, specifying which resource amount to change and how much.

.. code-block:: c#
  
  public class Rewarder ()
  {
    [Inject]
    private IResourcesInventory resources;
    
    public void GiveReward ()
    {
      resources.Increase(ResourceType.Gold, 1000);  
    }
  }

In case you need to validate that a resource never reaches 0, you can user the *IResourcesHelper* to check
if after the transaction the value will still be over 0.

.. code-block:: c#

  public class RationConsumer()
  {
    [Inject]
    private IResourcesInventory resources;
    
    [Inject]
    private IResourcesHelper helper;
    
    public void UseRations (int amount)
    {
      helper.ValidateResourcesForPurchase (ResourceType.Rations, amount, (valid, finalAmount) =>
      {
        if (valid)
          resources.Decrease (ResourceType.Rations, amount);
      });
    }
  }
  
Indicators
^^^^^^^^^^
We provide resource indicators as well, so the player can keep track of the amount of resources available at any time.
You can find the prefab on the *Plugins/Brainztorm/Prefabs/Resources* folder. You can use a resource bar, or a single resource indicator.

<resources bar>

<resource indicator>

Once you've got it on your scene you can configure which resources to show.

<configuration>

How it works
------------
Resources are synced with brainztorm's servers; any change either locally or on the backend will be inmediately reflected on the other end. The backend server validates all transactions.

Once the Resources component is initialized, it maps the utility ResourceCode info to the id of the corresponding player resource. All changes are made through the Variables component, which stores the data on a secure database.

Even if a hacker manages to cheat the game locally, since our backend has the data regarding every transaction, we can detect intrussions and handle them appropriately.
