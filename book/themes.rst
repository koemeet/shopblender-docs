.. index::
   single: Themes

Themes
======================

Shopblender has a hierachycal way of working with themes. You can link themes with each other to create template inheritance.

A **Theme** represents the whole design of a webshop. It has the following basic properties:

+------------+-----------------------------------------------------------------------------------------------------+
| Property   | Description                                                                                         |
+============+=====================================================================================================+
| name       | The human readable name of the theme                                                                |
+------------+-----------------------------------------------------------------------------------------------------+
| templates  | Holds a collection of **Template** models for the theme                                             |
+------------+-----------------------------------------------------------------------------------------------------+
| channel    | The ``Channel`` that this theme belongs to. If it's ``null`` it can be sold in the **Theme Store**  |
+------------+-----------------------------------------------------------------------------------------------------+
| parent     | The parent theme, so the theme can inherit templates etc.                                           |
+------------+-----------------------------------------------------------------------------------------------------+

A **Template** that a **Theme** can hold is very basic and consists of the following properties:

+------------+----------------------------------------------------------------------------------------------+
| Property   | Description                                                                                  |
+============+==============================================================================================+
| theme      | The **Theme** that owns the template                                                         |
+------------+----------------------------------------------------------------------------------------------+
| path       | The path of the template, it is seperated by a double colon (e.x. ``Product:show.html.twig``)|
+------------+----------------------------------------------------------------------------------------------+
| source     | The actual contents of the template in ``twig`` notation                                     |
+------------+----------------------------------------------------------------------------------------------+

