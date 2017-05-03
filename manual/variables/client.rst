################
Client Variables
################

**********
How to use
**********
The variables module is one of brainztorm's core features, so it will be enabled by 
default. To start using this component  first you need to define entities using the 
`Entity Manager <https://github.com/BrainzGames/Brainztorm-docs/blob/master/manual/variables/server.rst#create-a-new-structure>`_.

Then you can go to *Brainztorm > Settings > Modules > Variables* and press the sync 
button, once you do this matching c# classes will be created for the entities you 
defined in the admin tools.

To access your data, you use the **IData** interface, which offers methods to get, 
update and delete records.

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

As you can see, we use generics. So any data class which has an 
**[Entity ("mappedEntity")]** attribute can be used to handle backend data.

Handling data
=============
There are 5 ways to get data from backend:
- Get: Fetches all matches for the given criteria on the corresponding entity collection, if no criteria is set it will retrieve all elements in the collection.
- GetOne: Retrieves the first matching ocurrence in the mapped collection.
- GetIn: Retrieves a set of elements in the given collection that match the ids requested.
- GetAll: Gets all elements in the collection.

The callback will be invoked with the results once the response from the backend 
server is sent.

- To sync an element with the database you pass it as the argument of the *Save* method.

- The delete function errases the element from the database and any local copy of it.

- When you call the apply function, it updates every element modified locally to the database.

************
How it works
************
The database has a collection with all the created elements, whenever the client 
requests data these are sent in a JSON format like this:

.. code-block:: javascript
  
  {
    id: {
      $id: "6F43ADE2"
    },
    name: "Martin",
    health: 100,
    cost: 30,
    tier: "Gold"
  }
  
When the response is being handled by the client it is de-serialized to a c# data 
structure that matches it:

.. code-block:: c#

  [Entity ("Character")]
  public class Character
  {
    public ObjectId id;
    public string name;
    public int health;
    public int cost;
    public Tier tier; // this is an enum
  }
  
Then a local reference of the objects returned is kept to track all changes and 
enable syncing, updating and deleting.

Cache
=====
The results of data fetches, are stored locally in binary files as caches. These 
cache files have expiration time and a hash of the requested data so whenever you 
request exactly the same, it will be retrieved from cache rather than making a 
request to the server. This behaviour makes everything way faster.

Two types of cache are used: individual and query. The individual cache is used 
when you fetch using the GetIn or GetOne method, the query cache checks if the 
request is exactly the same and hashes it, so if you make similar querys often 
these will be cached.