Client Error Reporting
======================

Introduction
------------
Brainztorm's error reporting component helps you detect and debug bugs, errors, and crashes in your game through different
development steps. Providing a unified place to track errors and a friendly way to interact with the user when these occur.

<error intro>

We report errors for many common situations:
- Application crashes (iOS only)
- Unhandled and Managed Server errors
- Managed Client errors

How to use
----------



There's 2 kinds of errors: server-side errors and client-errors, both of them are handled similarly. Whenever an error is detected, a report will be created in the error server and a popup showing the error id will be shown to the user. With this error id, customers can contact support and inform them of the situation.

<error popup>

For example, if the player was buying a product from the store and an internal server error happens, transaction data could have not been handled appropriately by the server, leading to missing currency or services. With the corresponding error id, support can verify, reproduce and identify what caused the error.

