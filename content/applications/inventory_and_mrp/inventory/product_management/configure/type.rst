============
Product type
============

In Odoo, goods and services are both set up as *products*. When setting up a new product, there are
several fields that should be carefully chosen, as they will determine how to invoice and track a
business' goods or services.

To configure an existing product, go to :menuselection:`Inventory app --> Products --> Products`,
select the desired product from the list. Alternatively, from the :guilabel:`Products` menu, click
:guilabel:`New` to create a new product.

.. seealso::
  - `Odoo Tutorials: Product Type <https://www.youtube.com/watch?v=l6j0ZkP5mLM>`_

.. _inventory/product_management/for-sale-or-purchase:

For sale vs. purchase
=====================

Products and services can be designated as those that can be bought, sold, or both. On the product
form, tick the :guilabel:`Sales` checkbox if a product can be *sold* to a customer (e.g. finished
goods). Tick :guilabel:`Purchase` if the product can be *purchased* (e.g. raw materials).

.. example::
  If a resale clothing shop buys discounted denim jackets and sells them at a higher cost to the
  end consumer, the `Jacket` product form might have *both* the :guilabel:`Sales` and
  :guilabel:`Purchase` box ticked.

  On the other hand, let's say the store occasionally sews new jackets using denim and thread as raw
  materials. In the `Denim` and `Thread` product forms, only :guilabel:`Purchase` should be ticked,
  whereas the `Handmade Jacket` product form would only tick :guilabel:`Sales`.

Goods vs. services
==================

:guilabel:`Product Type` needs to be selected on the :guilabel:`General Information` tab. Each
product type impacts different operations in other Odoo applications, such as *Sales* and
*Purchasing*, and should be chosen carefully.

- :guilabel:`Goods`: A tangible, material object (e.g. anything from a hamburger to a house).

- :guilabel:`Service`: An intangible, immaterial offering (e.g. a repair, a haircut, call center
  assistance, etc.

- :guilabel:`Combo`: Any mix of goods or services (e.g. a new car (*good*) with an oil change
  included (*service*)).

.. note::
  Due to their immaterial nature, services are not trackable in Odoo's *Inventory* application.

.. _inventory/product_management/manufacture:

Configuring goods
=================

Selecting :guilabel:`Goods` as the product type automatically triggers the appearance of a few
fields in Odoo:

- :guilabel:`Inventory` tab: From here,
  :doc:`purchasing and manufacturing routes <../../shipping_receiving/daily_operations/use_routes>`
  and product logistics (such as product weight and customer lead time) can be specified.
- :ref:`Invoicing Policy <inventory/product_management/invoicing-policy>` field.
- :ref:`Track Inventory <inventory/product_management/tracking-inventory>` field.
- Smart buttons: Some smart buttons are triggered right away when :guilabel:`Goods` is selected;
  others show upon additionally selecting a :guilabel:`Track Inventory` method. For example,
  :guilabel:`On Hand` and :guilabel:`Forecasted` will display when :guilabel:`Track Inventory` is
  ticked.

.. image:: type/product-form.png
  :alt: Designate a product as a good or service.

.. _inventory/product_management/invoicing-policy:

Invoicing policy
----------------

This field only shows on the product form if a product is for sale (in other words, if
:guilabel:`Sales` is ticked).

When configuring a product for sale, it is necessary to choose an
:doc:`invoicing policy <../../../../sales/sales/invoicing/invoicing_policy>`. When an invoicing
policy of :guilabel:`Ordered quantities` is selected, customers are invoiced once the sales order
is confirmed. When :guilabel:`Delivered quantities` is ticked, customers are invoiced once the
delivery is completed.

.. _inventory/product_management/tracking-inventory:

Track inventory by product type
-------------------------------

The :guilabel:`Track Inventory` field on the product form determines a lot of Odoo's *Inventory*
operations. When :guilabel:`Track Inventory` is ticked, it indicates that the product is
**storable**, whereas when :guilabel:`Track Inventory` is left blank, it indicates a **consumable**
product.

- **Storable** products are those for which stock and inventory are maintained. Examples include
  finished goods and the raw materials or components needed to make them. Once ticked, a dropdown
  menu appears, offering for inventory to be tracked one of three ways:
  :guilabel:`By Unique Serial Number`, :guilabel:`By Lots`, and :guilabel:`By Quantity`.

  .. image:: type/storable.png
    :alt: Configure a storable good.

- **Consumable** products will be consumed in a short period of time, meaning that
  stock / inventory do *not* need to be maintained. Consumables are replaceable and essential, but
  exact counts are unnecessary. Examples include office supplies, packaging
  materials, or items used in production that do not need to be individually tracked.

.. tip::
  Choose :guilabel:`Storable Product` if it is necessary to track a product's stock at various
  locations, for inventory valuation, with lots and/or serial numbers, or when using
  reordering rules.

.. seealso::
  - :doc:`Tracking storable products using lot and serial numbers <../product_tracking>`

.. _inventory/product_management/inventory-ops-by-product-type:

Inventory operations by product type
------------------------------------

:ref:`Whether a good is storable or consumable <inventory/product_management/tracking-inventory>`
affects common *Inventory* operations, like transfers and reordering rules.

The table below summarizes which operations (and smart buttons) are enabled for storable vs.
consumable goods. Click highlighted chart items to navigate to detailed sections and related
documents.

.. list-table::
   :header-rows: 1
   :stub-columns: 1

   * - Inventory operation
     - Storable
     - Consumable
   * - :ref:`Show on-hand quantity <inventory/product_management/on-hand>`
     - Yes
     - No
   * - :ref:`Show forecasted quantity <inventory/product_management/on-hand>`
     - Yes
     - No
   * - :ref:`Use reordering rules <inventory/product_management/replenishment>`
     - Yes
     - No
   * - :ref:`Can be included in a purchase order <inventory/product_management/po>`
     - Yes
     - Yes
   * - :ref:`Use putaway rules <inventory/product_management/putaway>`
     - Yes
     - No
   * - :ref:`Can be manufactured, subcontracted, or used in another good's BoM
       <inventory/product_management/manufacturing>`
     - Yes
     - Yes
   * - :doc:`Use inventory adjustments <../../warehouses_storage/inventory_management/count_products>`
     - Yes
     - No
   * - :doc:`Use inventory valuation <../inventory_valuation/using_inventory_valuation>`
     - Yes
     - No
   * - :ref:`Create transfer <inventory/product_management/transfer-store>`
     - Yes
     - Yes
   * - :doc:`Use lot/serial number tracking <../product_tracking>`
     - Yes
     - No
   * - :doc:`Can be placed in a kit <../../../manufacturing/advanced_configuration/kit_shipping>`
     - Yes
     - Yes
   * - :ref:`Can be placed in a package <inventory/product_management/package>`
     - Yes
     - Yes
   * - :ref:`Appears on inventory reports <inventory/product_management/report>`
     - Yes
     - No

Inventory
~~~~~~~~~

.. _inventory/product_management/on-hand:

On-hand & forecasted quantities
*******************************

A storable product's on-hand and forecasted quantities, based on incoming and outgoing orders, are
reflected on the product form with two smart buttons:

- :icon:`fa-cubes` :guilabel:`On-Hand Quantity`: Number of units currently available in inventory.
  Click the button to view or add stock levels for a storable product.

- :icon:`fa-chart` :guilabel:`Forecasted`: Number of units *expected* to be available in inventory
  after all orders are taken into account. In other words,
  `forecasted = on hand quantity + incoming shipments - outgoing shipments`. Click the button
  to view the :guilabel:`Forecasted Report`.

On the other hand, consumable products are regarded as *always* available. Consequently,
:guilabel:`On-Hand Quantity` is not tracked, and there is no `Forecasted` quantity available.

.. _inventory/product_management/putaway:

Putaway rules & storage
***********************

Both storable and consumable goods can optimize storage using:

- :icon:`fa-random` :doc:`Putaway Rules <../../shipping_receiving/daily_operations/putaway>`:
  Putaway rules that apply to a good, such as where to store it when a new shipment arrives.

- :icon:`fa-cubes`
  :doc:`Storage Capacities <../../shipping_receiving/daily_operations/storage_category>`: Any
  storage capacity limitations specified for this good. For example, a warehouse may require that
  only 10 (or less) sofas be stored there at any given time, due to their large size.

.. _inventory/product_management/replenishment:

Replenishment
*************

Reordering rules
^^^^^^^^^^^^^^^^

Only storable products can trigger
:doc:`reordering rules <../../warehouses_storage/replenishment/reordering_rules>` to generate
purchase orders. Consumables *cannot* be managed using reordering rules.

Reordering rules can be configured directly on the product form via the :icon:`fa-refresh` icon.

    **Note:** If reordering rules already exist on a product, Odoo will relabel
    this button to :guilabel:`Min / Max`, to show the minimum and maximum number of units that must
    be in stock.

.. _inventory/product_management/po:

Creating purchase orders
^^^^^^^^^^^^^^^^^^^^^^^^

Both storable and consumable products can be included in a request for quotation in the *Purchase*
app. However, when receiving consumable products, their on-hand quantity does not change upon
validating the receipt (`WH/IN`).

Replenish smart button
^^^^^^^^^^^^^^^^^^^^^^

The :guilabel:`Replenish` button allows all goods to be restocked directly from the product form,
according to the :guilabel:`Preferred Route`.

.. seealso::
  :doc:`Replenishment <../../warehouses_storage/replenishment>`
  `Odoo Tutorials: Replenishment Methods for Manufacturing
  <https://www.youtube.com/watch?v=vtjeMGcG8aM>`

.. _inventory/product_management/manufacturing:

Manufacturing
~~~~~~~~~~~~~

Both storable and consumable products can be manufactured,
:doc:`subcontracted <../../../manufacturing/subcontracting>`, or included in another product's
:doc:`bill of materials (BoM) <../../../manufacturing/basic_setup/bill_configuration>`.

.. _inventory/product_management/BoM:

On the product form for a storable or consumable good, there are several smart buttons that may
appear for manufacturing operations:

- :icon:`fa-flask` :guilabel:`Bill of Materials`: The BoMs used to make this product.

- :icon:`fa-level-up` :guilabel:`Used In`: Other goods that include this product in their BoM.

.. _inventory/product_management/transfer-store:

Transferring goods
~~~~~~~~~~~~~~~~~~

*Transfers* are warehouse operations that involve the movement of goods. Examples of transfers
include
:doc:`deliveries and receipts <../../shipping_receiving/daily_operations/receipts_delivery_one_step>`
as well as :doc:`internal transfers <../../warehouses_storage/replenishment/resupply_warehouses>`
between warehouses.

When creating a transfer for storable products in the *Inventory* app, transfers modify the on-hand
quantity at each location. For example, transferring five units from the internal location
`WH/Stock` to `WH/Packing Zone` decreases the recorded quantity at `WH/Stock` and increases it at
`WH/Packing Zone`.

For consumable products, transfers can be created, but exact quantities at each storage location are
not tracked.

.. _inventory/product_management/package:

Packages
~~~~~~~~

Both storable and consumable products can be placed in :doc:`packages <package>`.

However, for consumable products, the quantity is not tracked, and the product is not listed in the
package's :guilabel:`Contents` (which can be accessed by going to
:menuselection:`Inventory app --> Products --> Packages`, and selecting the desired package).

.. figure:: type/package-content.png
   :align: center
   :alt: Show Packages page, containing the package contents list.

   A consumable product was placed in the package, but the **Content** section does not list it.

Additionally, if the :guilabel:`Move Entire Packages` feature is enabled
(:menuselection:`Inventory --> Configuration --> Operations Types`, and select any operation),
moving a package updates the location of the contained storable products but not the contained
consumable products.

.. _inventory/product_management/report:

Inventory reports
~~~~~~~~~~~~~~~~~

**Only** storable products appear on the following reports. Note, these reports are only available
to users with :doc:`administrator access <../../../../general/users/access_rights>`.

- :doc:`Stock report <../../warehouses_storage/reporting/stock>`: A comprehensive list of all
  on-hand, unreserved, incoming, and outgoing storable products. To access the report, go to
  :menuselection:`Inventory app --> Reporting --> Stock`.

- :doc:`Location report  <../../warehouses_storage/reporting/locations>`: A breakdown of which
  storable products are held at each location (internal, external, or virtual). The report is only
  available with the *Storage Location* feature activated (:menuselection:`Inventory app -->
  Configuration --> Settings`). To access the report, go to :menuselection:`Inventory app -->
  Reporting --> Locations`.

- :doc:`Moves History report <../../warehouses_storage/reporting/moves_history>`: An overview of
  where and when this good has moved in/out of stock. To access the report, go to
  :menuselection:`Inventory app --> Reporting --> Moves History`. Alternatively, click the
  :icon:`fa-exchange` :guilabel:`In / Out` smart button on a product form to filter the report
  on that product's moves history.

- :guilabel:`Moves Analysis`: A pivot table view of inventory transfers by operation type.

- :ref:`Stock Valuation report <inventory/management/reporting/valuation-report>`: A detailed record
  of the monetary value of all storable products.

