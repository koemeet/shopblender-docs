Database Guide
==============

When making changes to the PostgreSQL database (our main data store) you have to properly make
migrations to ensure a safe way to update the schema. We use the ``DoctrineMigrationsBundle``,
so we have an easy and standardized way to solve this.

.. danger::

    **IMPORTANT!** Never remove columns nor tables, but only add onto the existing schema in the
    first migration. This way we can guarantee that the application still works with the new schema.
    This is very important, since the database schema is migrated first and after that the application
    servers will be updated. In this guide we will provide you with a best practise on how to remove
    old columns on the next migration.


Adding a new migration file
---------------------------

So you have build your new cool feature and you had to make some changes to the schema (that is
changing the Doctrine mappings).

We start by running the following command:

.. code-block:: bash

    $ php app/console doctrine:migrations:diff

This will create a new migration version file at ``app/migrations/Version*.php``. Right now you
will have to check for anything that can break the application when running on an older version.

Some rules:
 - When you encounter a ``DROP COLUMN`` statement, comment it out.
 - When you encounter a ``RENAME COLUMN`` statement, you need to change it to ``ADD COLUMN`` and also make a ``DROP COLUMN`` from the old one and comment it out.

The reason that you have to comment some statements out is so that we can include those in the
next migration. We can do that because the application would no longer depend on those fields
and we can safely remove them.

So let's do that right now! Let's check if the previous migration file has some commented statements.
If so, we will include those too in our new migration file. Make it is easy to understand which
statements are from the previous migration and which ones are recent.

.. note::
    Some datatype changes to columns can also break the migration, so keep that in mind!

When you've altered the migration so that it can run on the previous application version and on
the new version, you are **done**!


Testing your migration file
---------------------------

Since we are using PostgreSQL we can run our migrations inside a transaction and if something fails,
for example some unique constraint, then it will properly rollback to pre-transaction. So with
that in mind, we try our new migration with an existing data set by running:

.. code-block:: bash

    $ php app/console doctrine:migrations:migrate


If you encounter an error that looks something like the image below, don't freak out! The schema
will be rolled back properly automatically and you can start over. In the case below there was
some duplicate data and the new schema change wanted to add a unique constraint on that data. To
fix that we can for example make a script in our migration to suffix all duplicate data with 1, 2, 3
etc.

.. image:: http://puu.sh/odBBT/164d3ea13b.png

.. note::
    In order to fix the issue described above we have to implement ``ContainerAwareInterface`` in
    our migration file.

    For more information about this topic, go to:
    https://symfony.com/doc/current/bundles/DoctrineMigrationsBundle/index.html#container-aware-migrations
