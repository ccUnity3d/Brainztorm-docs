#################
Store Admin Tools
#################

**********
How to use
**********
Adding new products to your Store is easy. First, you need to create the corresponding
categories to group the products that will be sold.

Creating Categories
===================

.. image:: images/at_store_categories.png

Categories attributes are: Identifier, Name, Icon and Order. Identifier and Name can be 
any string value you prefer. Icon is a path that will be managed by `Asset Bundles`_ component. 
The Order property determines the order of appareance for the category in the Store view. 

After the Categories had been created, it's time to create Products.

Creating Products
=================

.. image:: images/at_store_products.png

As shown in the image above, the following attributes are availables:

- **Store Categories**: a category previously created.
- **Icon**: an asset bundle path.
- **Code**, **Name** and **Description**: any string you want for identify and describe your product.

If the product is an **IAP** (In App Purchase) you must fill the corresponding fields with 
the provided identifiers from iOS (App Store) and Android (Google Play). Otherwise, 
you must fill the fields under the section **IAS** (In App Source) as follows:

- Item type: the type of resource used to purchase this product.
- Resource: the resource used to pay for this product.
- Amount: resource quantity the player will have to pay for this product.

If the product has requirements it should fulfill you can specify them in 
**Requirements** section.

The **Rewards** section is for setting the given resource by purchasing this product. 
Choose the Item type and Item code from their correspondant dropdowns and insert an 
Item amount the player receive when he/she purchase this product.

The **View Template** attribute you have to fill the name of the Item Type you 
created in Unity, this is used in Unity to know where to show the product.

Finally, the **Order** attribute sets the precedence level for each product within its 
respective category.

.. _Asset Bundle: #