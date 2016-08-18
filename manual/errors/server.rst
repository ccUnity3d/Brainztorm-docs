Show errors in Admin Tools
==========================

Admin tools has a option "Diagnostics" and the sub-option "Errors", in this section you can see all creashes in the game that has reported by the client side ordered by the last insidence to the first.

.. image:: images/errors.png

In the right top you can found a section of filters to group by type of error and show specific error by error.

.. image:: images/errors-filter.png

In the list of errors you can see the following columns:

- *Type*: Son el tipo de error que fue enviado si fue por parte de FrontEnd (Cliente) o Backend (Servidor).
- *First ocurrence*: Show the date of first ocurrence of this error.
- *Las ocurrence*: Show the date of last ocurrence of this error.
- *Ocurrence*: Show the number of ocurrences of this error.
- *Devices afected*: Show a list of devices that report this error.
- *Track error code*: Show the code of this error.
- *Message*: Show a short message of this error.
- *Version*: Show the version of brazintorm that used to report this error.
- *Content*: Button to show content of message reported by the cliend side.
- *Backtrace*: Button that only appear in type "Backend" to show all backtrace of the error.
