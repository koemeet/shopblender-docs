Channels API
==========

Shopblender channels API endpoint is `/api/channels`.

Index of all channels
-------------------

You can retrieve the full list by making the following request:

.. code-block:: text

    GET /api/channels

Response
~~~~~~~~
.. code-block:: text

    STATUS: 200 OK

.. code-block:: json

    {
        "jsonapi": {
            "version": "1.0"
        },
        "data": [
            {
                "type": "channels",
                "id": 1,
                "attributes": {
                    "code": "WEB-UK",
                    "name": "UK Webstore",
                    "description": null,
                    "url": "localhost",
                    "color": "Pink",
                    "enabled": true,
                    "created-at": "2015-12-14T15:53:20+0000",
                    "updated-at": "2015-12-14T15:53:20+0000"
                },
                "relationships": {
                    "workspace": {
                        "data": {
                            "type": "workspaces",
                            "id": 1
                        }
                    },
                    "locales": {
                        "links": {
                            "related": "/api/channels/1/locales"
                        }
                    },
                    "currencies": {
                        "links": {
                            "related": "/api/channels/1/currencies"
                        }
                    },
                    "products": {
                        "links": {
                            "related": "/api/channels/1/products"
                        }
                    },
                    "tags": {
                        "data": [
                            {
                                "type": "tags",
                                "id": 1
                            }
                        ]
                    },
                    "taxonomies": {
                        "links": {
                            "related": "/api/channels/1/taxonomies"
                        }
                    },
                    "payment-methods": {
                        "links": {
                            "related": "/api/channels/1/payment-methods"
                        }
                    },
                    "shipping-methods": {
                        "links": {
                            "related": "/api/channels/1/shipping-methods"
                        }
                    },
                    "default-currency": {
                        "data": null
                    },
                    "default-locale": {
                        "data": null
                    }
                },
                "links": {
                    "self": "/api/channels/1"
                }
            }
        ],
        "included": [
            {
                "type": "workspaces",
                "id": 1,
                "attributes": {
                    "name": "First Workspace"
                },
                "links": {
                    "self": "/api/workspaces/1"
                }
            },
            {
                "type": "tags",
                "id": 1,
                "attributes": {
                    "name": "Tuinposter"
                },
                "links": {
                    "self": "/api/tags/1"
                }
            }
        ]
    }


Create a channel
---------------

To create a new channel, you need to execute the following request:

.. code-block:: text

    POST /api/channels

Parameters
~~~~~~~~~~

+-------------------+-----------+----------+--------------------------------------------------------------------------------+
| Field             | Required? | Type     | Description                                                                    |
+===================+===========+==========+================================================================================+
| workspace         | yes       | int      | The ID of the workspace the channel belongs to                                 |
+-------------------+-----------+----------+--------------------------------------------------------------------------------+
| code              | yes       | string   | Unique code                                                                    |
+-------------------+-----------+----------+--------------------------------------------------------------------------------+
| name              | yes       | string   | Human readable name                                                            |
+-------------------+-----------+----------+--------------------------------------------------------------------------------+
| description       | no        | string   | Description of the channel                                                     |
+-------------------+-----------+----------+--------------------------------------------------------------------------------+
| enabled           | no        | bool     | Can this channel be visited?                                                   |
+-------------------+-----------+----------+--------------------------------------------------------------------------------+
| color             | no        | string   | Color used in the back-end                                                     |
+-------------------+-----------+----------+--------------------------------------------------------------------------------+
| locales           | no        | int[]    | Array of locale id's                                                           |
+-------------------+-----------+----------+--------------------------------------------------------------------------------+
| defaultLocale     | no        | int      | Locale id that is used by default                                              |
+-------------------+-----------+----------+--------------------------------------------------------------------------------+
| currencies        | no        | int[]    | Array of curreny id's                                                          |
+-------------------+-----------+----------+--------------------------------------------------------------------------------+
| defaultCurrency   | no        | int      | Currency id that is used by default                                            |
+-------------------+-----------+----------+--------------------------------------------------------------------------------+
| shippingMethods   | no        | int[]    | Array of shipping method id's                                                  |
+-------------------+-----------+----------+--------------------------------------------------------------------------------+
| paymentMethods    | no        | int[]    | Array of payment method id's                                                   |
+-------------------+-----------+----------+--------------------------------------------------------------------------------+

Request body
~~~~~~~~

.. code-block:: json

    {
        "workspace": 1,
        "code": "C6",
        "name": "Channel A",
        "description": "First channel, selling some goods",
        "tags": ["A tag"],
        "enabled": true,
        "url": "http://channel-a.shopblender.com",
        "color": "red",
        "locales": [1, 2],
        "defaultLocale": 1,
        "currencies": [1, 3],
        "defaultCurrency": 1,
        "shippingMethods": [1, 2, 4],
        "paymentMethods": [1, 2]
    }
