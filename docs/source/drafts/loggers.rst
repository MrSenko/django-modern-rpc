Loggers
=======

Internally, django-modern-rpc use exceptions and Python logging system to handle errors.
This design choice has 2 goals:

 1. **Return useful error message to clients** Both XML-RPC and JSON-RPC describe how a server must provide
    error response if something in the remote procedure failed. In django-modern-rpc, we try to be as accurate as
    possible when returning an error response.
 2. **Allow for error logging** The server administrators should be informed when a RPC call has failed, and get all
    information needed to decide if a bug should be fixed in procedure's code or if an error can be ignored.
