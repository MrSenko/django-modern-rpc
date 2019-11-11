=================
Quick-start guide
=================

Configuring django-modern-rpc is quick and simple. Follow that steps to be up and running in few minutes!

Installation and configuration
==============================

Install ``django-modern-rpc`` in your environment, using pip or any equivalent tool:

.. code:: bash

    pip install django-modern-rpc

Add ``modernrpc`` app to your ``settings.INSTALLED_APPS``:

.. code::

    INSTALLED_APPS = [
        ...
        'modernrpc',
    ]

Declare a RPC EntryPoint
========================

The entrypoint is a special Django view which handle RPC calls. Like any other view, it has to
be declared in URLConf or any app specific ``urls.py``:

.. code::

    from django.conf.urls import url
    from modernrpc.views import RPCEntryPoint

    urlpatterns = [
        # ... other url patterns
        url(r'^rpc/', RPCEntryPoint.as_view()),
    ]

Entry points behavior can be customized to your needs. Read :ref:`Entrypoint configuration` for full documentation.

Write a remote procedure
========================

Remotes procedures are simple Python functions decorated with ``@rpc_method``.

.. code:: python

    # In myproject/rpc_app/rpc_methods.py
    from modernrpc.core import rpc_method

    @rpc_method
    def add(a, b):
        return a + b

``@rpc_method`` behavior can be customized to your needs. Read :ref:`Configure the registration <rpc_method_options>`
for full list of options.

Declare your RPC methods modules
================================

Django-modern-rpc will automatically register functions decorated with ``@rpc_method``, but needs a hint to locate them.
Declare ``settings.MODERNRPC_METHODS_MODULES`` to indicate all python modules where remote procedures are defined.

.. code:: python

    MODERNRPC_METHODS_MODULES = [
        'rpc_app.rpc_methods'
    ]

That's all !
============

Your application is ready to receive XML-RPC or JSON-RPC calls. The entry point URL is ``http://yourwebsite.com/rpc/``
but you can customize it to fit your needs.
