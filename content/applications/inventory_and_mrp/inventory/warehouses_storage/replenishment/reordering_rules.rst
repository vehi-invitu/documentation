================
Reordering rules
================

.. |SOs| replace:: :abbr:`SOs (Sales Orders)`

.. _inventory/management/reordering_rules:

Reordering rules are used to keep forecasted stock levels above a certain threshold without
exceeding a specified upper limit. This is accomplished by specifying a minimum quantity that stock
should not fall below and a maximum quantity that stock should not exceed.

Reordering rules can be configured for each product based on the route used to replenish it. If a
product uses the *Buy* route, then a Request for Quotation (RFQ) is created when the reordering rule
is triggered. If a product uses the *Manufacture* route, then a Manufacturing Order (MO) is created
instead. This is the case regardless of the selected replenishment route.

.. seealso::
   - `Odoo Tutorials: Automatic Reordering Rules <https://www.youtube.com/watch?v=XEJZrCjoXaU>`_
   - `Odoo Tutorials: Manual Reordering Rules <https://www.youtube.com/watch?v=deIREJ1FFj4>`_

Configure products for reordering rules
=======================================

In order to use reordering rules for a product, it must first be correctly configured. Begin by
navigating to :menuselection:`Inventory app --> Products --> Products`, then select an existing
product, or create a new one by clicking :guilabel:`New`.

On the product form, under the :guilabel:`General Information` tab, make sure that the
:guilabel:`Product Type` is set to :guilabel:`Storable Product`. This is necessary because Odoo only
tracks stock quantities for storable products, and this number is used to trigger reordering rules.

.. image:: reordering_rules/product-type.png
   :align: center
   :alt: Set the Product Type as Storable.

Next, click on the :guilabel:`Inventory` tab and select one or more routes from the
:guilabel:`Routes` section. Doing so tells Odoo which route to use to replenish the product.

.. image:: reordering_rules/select-routes.png
   :align: center
   :alt: Select one or more routes on the Inventory tab.

If the product is reordered using the :guilabel:`Buy` route, confirm that the :guilabel:`Can be
Purchased` checkbox is enabled under the product name. This makes the :guilabel:`Purchase` tab
appear. Click on the :guilabel:`Purchase` tab, and specify at least one vendor, and the price that
they sell the product for, so that Odoo knows which company the product should be purchased from.

.. image:: reordering_rules/specify-vendor.png
   :align: center
   :alt: Specify a vendor and price on the Purchase tab.

If the product is replenished using the :guilabel:`Manufacture` route, it needs to have at least one
Bill of Materials (BoM) associated with it. This is necessary because Odoo only creates
manufacturing orders for products with a :abbr:`BoM (Bill of Materials)`.

If a :abbr:`BoM (Bill of Materials)` does not already exist for the product, select the
:guilabel:`Bill of Materials` smart button at the top of the product form, then click
:guilabel:`New` to configure a new :abbr:`BoM (Bill of Materials)`.

.. image:: reordering_rules/bom-smart-button.png
   :align: center
   :alt: The Bill of Materials smart button on a product form.

Create new reordering rules
===========================

To create a new reordering rule, navigate to :menuselection:`Inventory app --> Configuration -->
Reordering Rules`, then click :guilabel:`New`, and fill out the new line as follows:

- :guilabel:`Product`: The product that is replenished by the rule.
- :guilabel:`Location`: The location where the product is stored.
- :guilabel:`Min Quantity`: The minimum quantity that can be forecasted without the rule being
  triggered. When forecasted stock falls below this number, a replenishment order for the product is
  created.
- :guilabel:`Max Quantity`: The maximum quantity that stock is replenished up to.
- :guilabel:`Multiple Quantity`: Specify if the product should be replenished in batches of a
  certain quantity (e.g., a product could be replenished in batches of 20).
- :guilabel:`UoM`: The unit of measure used for reordering the product. This value can simply be
  `Units` or a specific unit of measurement for weight, length, etc.

.. image:: reordering_rules/reordering-rule-form.png
   :align: center
   :alt: The form for creating a new reordering rule.

.. tip::
   Reordering rules can also be created from each product form. To do so, navigate to
   :menuselection:`Inventory app --> Products --> Products`, then select a product. Click on
   :menuselection:`Reordering Rules smart button --> New`, then fill out the new line, as detailed
   above.

For advanced usage of reordering rules, learn about the following reordering rule fields:

- :ref:`Trigger <inventory/product_management/trigger>`
- :ref:`Visibility days <inventory/product_management/visibility-days>`
- :ref:`Preferred route <inventory/product_management/route>`

.. note::
   The fields above are not available by default, and must be enabled by selecting the
   :guilabel:`(slider)` icon in the far-right corner, and selecting the desired column from the
   drop-down menu.

.. _inventory/product_management/trigger:

Trigger
=======

When stock falls below the reordering rule's minimum, set the reordering rule's *trigger* to
*automatic* to automatically create purchase or manufacturing orders to replenish stock.

Alternatively, setting the reordering rule's trigger to *manual* displays the product and forecasted
stock on the *replenishment dashboard*, where the procurement manager can review the stock levels,
lead times, and forecasted dates of arrival.

.. seealso::
   :doc:`../replenishment`

.. tip::
   The :guilabel:`Replenishment` dashboard is accessible by going to :menuselection:`Inventory app
   --> Operations --> Replenishment`.

To enable the :guilabel:`Trigger` field, go to :menuselection:`Inventory app --> Configuration -->
Reordering Rules`. Then, click the :guilabel:`(slider)` icon, located to the far-right of the column
titles, and enable the :guilabel:`Trigger` option from the additional options drop-down menu that
appears.

.. image:: reordering_rules/enable-trigger.png
   :align: center
   :alt: Enable the Trigger field by toggling it in the additional options menu.

In the :guilabel:`Trigger` column, select :guilabel:`Auto` or :guilabel:`Manual`. Refer to the
sections below to learn about the different types of reordering rules.

Auto
----

Automatic reordering rules, enabled by setting the reordering rule's :guilabel:`Trigger` field to
:guilabel:`Auto`, generate purchase or manufacturing orders when:

#. the scheduler runs, and the *On Hand* quantity is below the minimum
#. a sales order is confirmed, and lowers the *Forecasted* quantity of the product below the minimum

.. tip::
   The scheduler is set to run once a day, by default.

   To manually trigger a reordering rule before the scheduler runs, ensure :ref:`developer mode
   <developer-mode>` is enabled, and then select :menuselection:`Inventory app --> Operations -->
   Run Scheduler`. Then, select the green :guilabel:`Run Scheduler` button on the pop-up window that
   appears.

   Be aware that this also triggers *any other* scheduled actions.

.. example::
   The product, `Office Lamp`, has an automatic reordering rule set to trigger when the forecasted
   quantity falls below the :guilabel:`Min Quantity` of `5.00`. Since the current
   :guilabel:`Forecast` is `55.00`, the reordering rule is **not** triggered.

   .. image:: reordering_rules/auto.png
      :align: center
      :alt: Show automatic reordering rule from the Reordering Rule page.

If the :guilabel:`Buy` route is selected, then an :abbr:`RFQ (Request for Quotation)` is generated.
To view and manage :abbr:`RFQs (Requests for Quotation)`, navigate to :menuselection:`Purchase app
--> Orders --> Requests for Quotation`.

If the :guilabel:`Manufacture` route is selected, then an :abbr:`MO (Manufacturing Order)` is
generated. To view and manage :abbr:`MOs (Manufacturing Orders)`, navigate to
:menuselection:`Manufacturing app --> Operations --> Manufacturing Orders`.

When no route is selected, Odoo selects the :guilabel:`Route` specified in the :guilabel:`Inventory`
tab of the product form.

.. _inventory/product_management/manual-rr:

Manual
------

Manual reordering rules, configured by setting the reordering rule's :guilabel:`Trigger` field to
:guilabel:`Manual`, list a product on the replenishment dashboard when the forecasted quantity
falls below a specified minimum. Products on this dashboard are called *needs*, because they are
needed to fulfill upcoming sales orders, for which the forecasted quantity is not enough.

The replenishment dashboard, accessible by navigating to :menuselection:`Inventory app -->
Operations --> Replenishment`, considers sales order deadlines, forecasted stock levels, and vendor
lead times. It displays needs **only** when it is time to reorder items.

.. note::
   If the one-day window for ordering products is too short, skip to the :ref:`visibility days
   <inventory/product_management/visibility-days>` section to make the need appear on the
   replenishment dashboard a specified number of days in advance.

.. image:: reordering_rules/manual.png
   :align: center
   :alt: Click the Order Once button on the replenishment dashboard to replenish stock.

.. _inventory/product_management/visibility-days:

Visibility days
===============

.. important::
   Ensure :doc:`lead times <lead_times>` are understood before proceeding with this section.

*Visibility days*  allow businesses to optimize reordering rules by strategically grouping purchase
orders for upcoming needs. This reduces transport costs and leverages supplier discounts for larger
orders by consolidating quantities required now and in the near future.

For example:

- A company places orders every Monday, with a vendor lead time of seven days. Odoo plans the
  :guilabel:`To Order` quantity for the period from this Monday to next Monday.
- However, a sales order (SO) is due next Tuesday. Without visibility days, this need will only
  appear on the replenishment report tomorrow (Tuesday), **prompting a separate order and additional
  shipping costs**.

Context
-------

To understand how visibility days help with the typical ordering process, it must be understood that
a reordering rule's *Forecast* and *To Order* quantities is dependent on a **set range of dates**.

By default, Odoo's range of dates is between between the current date plus the purchase lead time.
The *Forecast* and *To Order* quantities are calculated based on the number of open |SOs| with the
delivery date within this range.

.. note::
   When the product has multiple vendors, the chosen purchase lead time is based on the selected
   vendor in the :guilabel:`Vendor` column (click the :icon:`oi-settings-adjust`
   :guilabel:`(sliders)` icon to enable) or the selected vendor in the :guilabel:`Lead Times` pop-up
   window found by clicking the :icon:`fa-info-circle` :guilabel:`(i)` icon.

.. example::

   Continuing the example from above, with the vendor lead time of 7 days, with the following |SOs|:
   - SO 1: 1 unit with a delivery deadline in 5 days
   - SO 2: 3 units with a delivery deadline in 9 days

   .. figure:: reordering_rules/default-range.png
      :alt: Default range of dates.

      Demands within 7 days are visible on the replenishment report.

   With the default range, replenishment report will only show demand for up to the next 7 days. In
   that case, the :guilabel:`To Order` quantity is `1`.

   .. image:: reordering_rules/no-visibility.png
      :alt: Show normal demand.

Set visibility days
-------------------

To set a visibility day to incorporate orders in the near future, navigate to
:menuselection:`Inventory app --> Operations --> Replenishment`.

Next, enable the :guilabel:`Visibility Days` field by clicking the :guilabel:`(sliders)` icon to the
far right and choosing the feature from the drop-down menu. Then, enter the desired visibility days.

.. example::

   To continue the above example, after adding `2.00` to visiblity days, the demand for SO 2 in 9
   days is also considered, as the :guilabel:`To Order` quantity has been updated to `4.00`.

   .. figure:: reordering_rules/extended.png
      :alt: Extended range of dates.

      Demands within 7 (+ 2) days are visible on the replenishment report.

   .. image:: reordering_rules/visibility.png
      :alt: Show demand with visibility days included.

.. _inventory/product_management/route:

Preferred route
===============

Odoo allows for multiple routes to be selected under the :guilabel:`Inventory` tab on each product
form. For instance, it is possible to select both :guilabel:`Buy` and :guilabel:`Manufacture`, thus
enabling the functionality of both routes.

Odoo also enables users to set a preferred route for a product's reordering rule. This is the route
that the rule defaults to if multiple are selected. To select a preferred route, begin by navigating
to :menuselection:`Inventory app --> Configuration --> Reordering Rules` or
:menuselection:`Inventory app --> Operations --> Replenishment`.

Click inside of the column on the row of a reordering rule, and a drop-down menu shows all available
routes for that rule. Select one to set it as the preferred route.

.. image:: reordering_rules/select-preferred-route.png
   :align: center
   :alt: Select a preferred route from the drop-down.

.. important::
   If multiple routes are enabled for a product but no preferred route is set for its reordering
   rule, the product is reordered using the selected route that is listed first on the
   :guilabel:`Inventory` tab of the product form.
