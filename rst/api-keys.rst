.. _api-keys:

API Keys
========

Authorization
-------------
We require that a JSON Web Token `JWT <https://jwt.io/>`_ be sent along with requests via the `Authorization` header. There's no need to create JWTs manually since they will be created for you when you register for the API - Register at |dev_portal_url|

JWTs are passed as bearer tokens in the `Authorization` header, and look like the following::

  Authorization: Bearer <api-key>



Security Considerations
-----------------------
Remember when developing a website/web application that your API key should never be stored client side. Calls to the API should only be made from a secure server side application.



Titles
------
The `TitleID` for a request is determined by the API Key and sent in the `Authorization` header automatically. Some objects may have a `titleID` field specifying the game title associated with the data returned.
