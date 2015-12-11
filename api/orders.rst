Orders API
==========

Shopblender orders API endpoint is `/api/orders`.

Index of all orders
-------------------

You can retrieve the full list order by making the following request:

.. code-block:: text

    GET /api/orders

The response will contain the newly created order information.

.. code-block:: text

    STATUS: 200 OK

.. code-block:: json

    {
        "jsonapi": {
            "version": "1.0"
        },
        "meta": {
            "page": 1,
            "limit": 10,
            "pages": 1,
            "total": 9
        },
        "links": {
            "first": "http://shopblender.dev/app_dev.php/api/orders?page=1",
            "last": "http://shopblender.dev/app_dev.php/api/orders?page=1",
            "next": null,
            "previous": null
        },
        "data": [
            {
                "type": "orders",
                "id": 1,
                "attributes": {
                    "number": "000000001",
                    "items-total": 8130,
                    "adjustments-total": 4370,
                    "total": 12500,
                    "created-at": "2015-12-10T23:34:15+0000",
                    "updated-at": "2015-12-10T23:35:16+0000",
                    "deleted-at": null,
                    "expires-at": "2015-12-11T02:34:15+0000",
                    "currency": "EUR",
                    "exchange-rate": 1,
                    "checkout-state": "cart",
                    "payment-state": "completed",
                    "shipping-state": "ready"
                },
                "relationships": {
                    "customer": {
                        "data": {
                            "type": "customers",
                            "id": 1
                        }
                    },
                    "channel": {
                        "data": {
                            "type": "channels",
                            "id": 1
                        }
                    },
                    "shipping-address": {
                        "data": {
                            "type": "addresses",
                            "id": 1
                        }
                    },
                    "billing-address": {
                        "data": {
                            "type": "addresses",
                            "id": 2
                        }
                    },
                    "payments": {
                        "links": {
                            "related": "/api/orders/1/payments"
                        }
                    },
                    "shipments": {
                        "links": {
                            "related": "/api/orders/1/shipments"
                        }
                    }
                },
                "links": {
                    "self": "/api/orders/1"
                }
            }
        ]
    }

Edit an order
---------------

To edit an existing order (cart), you need to execute the following request:

.. code-block:: text

    PUT /api/orders/1

Request body
~~~~~~~~

.. code-block:: json

    {
        "channel": 1,
        "state": "shipped",
        "currency": "GBP",
        "items": [
            {
                "quantity": 2,
                "unitPrice": 120.00
            }
        ],
        "shippingAddress": {
            "firstName": "Steffen",
            "lastName": "Brem",
            "phoneNumber": "+31612345678",
            "company": "Shopblender",
            "country": 158,
            "street": "Tanstraat 11",
            "city": "Twello",
            "postcode": "7391 TR"
        },
        "billingAddress": {
            "firstName": "Steffen",
            "lastName": "Brem",
            "phoneNumber": "+31612345678",
            "company": "Shopblender",
            "country": 158,
            "street": "Tanstraat 15",
            "city": "Twello",
            "postcode": "7391 TR"
        }
    }

Response
~~~~~~~~
.. code-block:: text

    STATUS: 200 OK

.. code-block:: json

    {
        "jsonapi": {
            "version": "1.0"
        },
        "data": {
            "id": 1,
            "type": "orders",
            "attributes": {
                "state": "shipped",
                "payment-state": "completed",
                "created-at": "2015-12-10T23:34:15+0000",
                "expires-at": "2015-12-11T02:34:15+0000",
                "deleted-at": null,
                "items-total": 24000,
                "exchange-rate": 1,
                "total": 28370,
                "shipping-state": "ready",
                "updated-at": "2015-12-11T15:17:36+0000",
                "number": "000000001",
                "adjustments-total": 4370,
                "checkout-state": "cart",
                "currency": "GBP"
            },
            "relationships": {
                "shipments": {
                    "links": {
                        "related": "/api/orders/1/shipments"
                    }
                },
                "shipping-address": {
                    "data": {
                        "type": "addresses",
                        "id": 1
                    }
                },
                "channel": {
                    "data": {
                        "type": "channels",
                        "id": 1
                    }
                },
                "customer": {
                    "data": {
                        "type": "customers",
                        "id": 1
                    }
                },
                "billing-address": {
                    "data": {
                        "type": "addresses",
                        "id": 2
                    }
                },
                "payments": {
                    "links": {
                        "related": "/api/orders/1/payments"
                    }
                }
            },
            "links": {
                "self": "/api/orders/1"
            }
        }
    }
