Show errors in Admin Tools
==========================

Admin tools has an option "Diagnostics" and the sub-option "Errors", in this section you can see all the crashes in the game that has been reported by the client ordered by the lastest insidence to the first.

At the right top of the screen, you can find a section of filters to group by type of errors and show a specific error by its code.

.. image:: images/errors-filter.png


In the list of errors you can see the following columns:

.. image:: images/errors.png

- **Type**: Shows the type of error that has been sent: Frontend (Client) or Backend (Server).
- **First ocurrence**: Shows the date of first ocurrence of this error.
- **Last ocurrence**: Shows the date of last ocurrence of this error.
- **Ocurrence**: Shows the number of ocurrences of this error.
- **Devices afected**: Shows a list of devices that have reported this error.
- **Track error code**: Shows the code of this error.
- **Message**: Shows a short message or description of this error.
- **Version**: Shows the Brainztorm version that have been used to report this error.
- **Content**: Button to display the content of message reported by the client side.
- **Backtrace**: Button that only appears when the error is of type "Backend" to show the backtrace of the error.
