Client Error Reporting
======================

Introduction
------------
Brainztorm's error reporting component helps you detect and debug bugs, errors, and crashes in your game through different
development steps. Providing a unified place to track errors and a friendly way to interact with the user when these occur.

<error intro>

How to use
----------
The error reporting component is one of brainztorm core components, which means it will be always enabled. It will create reports automatically for: application crashes (iOS only), server errors and detected brainztorm sdk malfunction. 

There's 2 kinds of errors: server-side errors and client-errors, both of them are handled similarly. When brainztorm detects a client-side error, a popup with related info is created; this popup includes a unique error id that customers can use to contact support and inform them of the situation.

<error popup>

For example, if the player was buying a product from the store and an internal server error happens, transaction data could have not been handled appropriately by the server, leading to missing currency or services. With the corresponding error id, support can verify, reproduce and identify what caused the error.

Whenever an error is detected in the server, a report will be created in the error server and the registered error handler will be invoked. To register error handlers for a given error, you need to create an implementation of the *IErrorHandler* interface. This should be registered to *ITransactionErrors* in order to be triggered.

.. code-block:: c#

  public class MyErrorHandler: IErrorHandler, IInitializable
  {
    [Inject]
    private ITransactionErrors transactionErrors;
  
    public void Initialize ()
    {
      transactionErrors.Add("my-error-type", this);
    }
    
    public void OnFailed(IErrorData error)
    {
      //DO SOMETHING
    }
  }

There's a default error handler, which uses the same error popup and restarts the game when the player dismisses it. To change what is shown to the player in this popup, you can change the *Communication Error Text Settings* either through the configuration view or the settings asset directly.

<error text settings>

Your error handlers can use the error popup as well, through the *IGenericTransactionErrorPopupMaker* interface you create a popup which will invoke an action you define when dismissed.

.. code-block:: c#

  public class MyPopupErrorHandler: IErrorHandler, IInitializable
  {
    [Inject]
    private ITransactionErrors transactionErrors;
    
    [Inject]
    private IGenericTransactionErrorPopupMaker popupMaker;
  
    public void Initialize ()
    {
      transactionErrors.Add("my-error-type", this);
    }
    
    public void OnFailed(IErrorData error)
    {
      popupMaker.Show (error, OnDismissed);
    }
    
    private void OnDismissed()
    {
      //DO SOMETHING
    }
  }

How it works
------------
All error reports are sent to the error server through an independent web service. These error reports include the following information:

- *Error Id* (string): A unique error identifier.
- *Error Code* (string): The error type or categorization.
- *Message* (string): A message sent by server describing what happened.
- *Custom Attributes* (hashtable): Any custom attribute sent by the server when the error was detected.

