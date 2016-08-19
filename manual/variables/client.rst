Client Variables
================

Intro
-----
The variables module eases the way to handle data stored on server. Allows you to create custom entities and sync them with backend collections instantly.

<intro>

You might need to create a set of units with different stats, keep track of the players characters and more. You could do so storing the data on a secure server rather than in local storage, which could be easily breached and exploited through many already available tools.

How to use
----------
The variables module is one of brainztorm's core features, so it will be enabled by default. To start using this component  first you need to define entities using the `Entity Manager <https://github.com/BrainzGames/Brainztorm-docs/blob/master/manual/variables/server.rst#create-a-new-structure>`_.

Then you can go to *Brainztorm > Settings > Modules > Variables* and press the sync button, once you do this matching c# classes will be created for the entities you defined in the admin tools.

<sync>

<generated>

To access your data, you use the **IData** interface, which offers methods to get, update and delete records.

.. code-block:: c#

  public interface IData
  {
    void Get<T>(Action<List<T>> listHandler, QueryBuilder query = null, DataOptions options = DataOptions.None) where T : class, new();
    
    void GetOne<T>(Action<T> handler, QueryBuilder query = null, DataOptions options = DataOptions.None) where T : class, new();
    
    IDataCursor<T> CreateCursor<T>(int pageSize, QueryBuilder query = null, DataOptions options = DataOptions.None) where T : class, new();
    
    void GetIn<T>(Action<List<T>> listHandler, IEnumerable<ObjectId> ids, DataOptions options = DataOptions.None) where T : class, new();
    
    void GetAll<T>(Action<List<T>> listHandler, DataOptions options = DataOptions.None) where T : class, new();
    
    void Save<T>(T obj, Action<string> errorHandler = null) where T : class, new();
    
    void Delete<T>(T obj, Action<string> errorHandler = null) where T : class, new();
    
    void Apply();
  }

As you can see, we use generics. So any data class which has an **[Entity ("mappedEntity")]** attribute can be used to handle backend data.

Getting data
^^^^^^^^^^^^
There are 5 ways to get data from backend:
- Get: Fetches all matches for the given criteria on the corresponding entity collection, if no criteria is set it will retrieve all elements in the collection.
- GetOne: Retrieves the first matching ocurrence in the mapped collection.
- GetIn: 
- GetAll:
