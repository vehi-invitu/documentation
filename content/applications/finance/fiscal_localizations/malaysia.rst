========
Malaysia
========

.. _malaysia/configuration:

Configuration
=============

.. _malaysia/configuration/modules:

Modules installation
--------------------

:ref:`Install <general/install>` the following modules to get the latest features of the Malaysian
localization:

.. list-table::
   :header-rows: 1

   * - Name
     - Technical name
     - Description
   * - :guilabel:`Malaysia - Accounting`
     - `l10n_my`
     - This module includes the default
       :ref:`fiscal localization package <fiscal_localizations/packages>`.
   * - :guilabel:`Malaysia - Accounting Reports`
     - `l10n_my_reports`
     - This module includes the accounting reports for Malaysia.
   * - :guilabel:`Malaysia - UBL PINT`
     - `l10n_my_ubl_pint`
     - This module includes the features required to export invoices in PINT format.
   * - :guilabel:`Malaysia - E-invoicing`
     - `l10n_my_edi`
     - This module includes the features required for integration with MyInvois under IRBM.

.. note::
   When **Malaysia** is selected for a company's :guilabel:`Fiscal Localization`, Odoo automatically
   installs specific modules.

.. _malaysia/configuration/company:

Configure your company
----------------------

To configure the company information, go to the :guilabel:`Contacts` app and search for the company
name.

#. Select the :guilabel:`Company` and configure the following fields:

   - :guilabel:`Name`.
   - :guilabel:`Address`: Add :guilabel:`City`, :guilabel:`State`, :guilabel:`Zip Code`, and
     :guilabel:`Country`.

     - In the :guilabel:`Street` field, enter the street name, number, and any additional address
       information.
     - In the :guilabel:`Street 2` field, enter the neighborhood.

   - :guilabel:`Tax ID`: Tax identification number.
   - :guilabel:`SST`: Malaysian Sales and Service Tax Number - add if applicable.
   - :guilabel:`TTx`: Malaysian Tourism Tax Number - add if applicable.
   - :guilabel:`Phone`.

#. To upload a company logo to the :guilabel:`Your logo` field, click the :icon:`fa-pencil`
   :guilabel:`(pencil)` icon, select an image, and click :guilabel:`Select`.

#. :guilabel:`Save` the contact.

.. _malaysia/myinvois:

E-invoicing integration with MyInvois
=====================================

The MyInvois Portal is a platform provided by the :abbr:`IRBM (Inland Revenue Board of Malaysia)`
that facilitates the implementation of e-invoices for Malaysian taxpayers.
Odoo supports integration with MyInvois to submit the invoices generated on Odoo.

.. important::
   - :guilabel:`Malaysia - E-invoicing module` must be installed to submit invoices to MyInvois.

.. _malaysia/myinvois/setup:

Set-up
------

.. _malaysia/myinvois/setup/registration:

MyInvois registration
~~~~~~~~~~~~~~~~~~~~~

Before use, the company must register and log in to the MyInvois portal to grant Odoo the
**right to invoice** as an intermediary.

.. _MyTax: https://mytax.hasil.gov.my

#. To access the MyInvois portal, log in to MyTax_ . Choose the :guilabel:`ID Type` and the
   corresponding :guilabel:`identification number` that was used to register for the digital
   certificate.

   .. note::
      If there was no previous login, please refer to the :guilabel:`User Manual` in MyTax Portal.
      Both the **Pre-production** (:dfn:`testing environment to try the functions before using the
      actual (production) environment`) and **Production** (:dfn:`actual environment to submit
      e-invoices with accurate information`) environments are supported.

#. From the :guilabel:`dashboard`, click the :icon:`fa-angle-down` :guilabel:`(angle-down)` in the
   top-right corner and select :guilabel:`View Taxpayer Profile`.

#. In the :guilabel:`Representatives` section, click :guilabel:`Add Intermediary` in the top-right
   corner.

   .. image:: malaysia/myinvois-add-intermediary.png
      :alt: MyInvois add intermediary

#. Add `ODOO S.A.` as an intermediary using the following information.

   - :guilabel:`TIN`: `C57800417080`
   - :guilabel:`BRN`: `BE0477472701`
   - :guilabel:`Name`: `ODOO S.A.`

#. To make sure the below necessary permissions are granted, click the :icon:`fa-toggle-on`
   :guilabel:`(toggle-on)`:

   - :guilabel:`Representation From`: **On**
   - :guilabel:`Representation To`: Off
   - :guilabel:`Document - Submit`: **On**
   - :guilabel:`Document - Cancel`: **On**
   - :guilabel:`Document - Request Rejection`: **On**
   - :guilabel:`Notifications - View`: Off

   .. note::
      Access can be revoked in the future if needed.
      Odoo, as an intermediary, does not store invoices sent on behalf of the client on the proxy
      server.

#. Click :guilabel:`Save`. `ODOO S.A.` status is then :guilabel:`Active`.

   .. image:: malaysia/myinvois-intermediary-active.png
      :alt: MyInvois status active

.. _malaysia/myinvois/setup/odoo:

Configuration in Odoo
~~~~~~~~~~~~~~~~~~~~~

.. _malaysia/myinvois/setup/odoo/einvoicing:

Electronic Invoicing
********************

Go to :menuselection:`Accounting --> Configuration --> Settings`. In the
:guilabel:`Malaysian Electronic Invoicing` section, choose the relevant :guilabel:`MyInvois mode`
related to the :guilabel:`production` or :guilabel:`pre-production` environment registered for
MyInvois access.
Make sure to allow Odoo to process the e-invoices by checking the box, then click
:guilabel:`Register`.

.. note::
   To change the TIN reference, click :guilabel:`Unregister` and :guilabel:`Register` again after
   changing the company contact. Make sure the number registered on MyInvois matches.

.. _malaysia/myinvois/setup/odoo/company:

Company & Contacts Information
******************************

Open the :guilabel:`Settings` app. In the :guilabel:`Companies` section, click
:guilabel:`Update Info`. In the :guilabel:`E-invoicing` section, complete the following fields:

   - :guilabel:`Identification`: The :guilabel:`ID Type` and associated
     :guilabel:`Identification number` used to register for the digital certificate.
   - :guilabel:`Ind. Classification`: The 5-digit numeric code that represents the nature and
     activity of the business.

In the :guilabel:`Contacts` app, for the contacts who receive the invoices, fill in the following
fields:

   - :guilabel:`Country`
   - :guilabel:`State`
   - :guilabel:`Phone`
   - :guilabel:`Tax ID`
   - :guilabel:`Identification`: the :guilabel:`ID Type` and the corresponding
     :guilabel:`Identification number` of the contact registered under MyTax.

.. _malaysia/myinvois/setup/odoo/product:

Products
********

All the products to be included in e-invoicing require a :guilabel:`Malaysian classification code`.
To do so, access the :guilabel:`Product` form. In the :guilabel:`General Information` tab,
complete the :guilabel:`Malaysian classification code`.

.. _malaysia/myinvois/workflow:

Workflow
--------

.. _malaysia/myinvois/workflow/sending:

Send invoices to MyInvois
~~~~~~~~~~~~~~~~~~~~~~~~~

Invoices can be sent to MyInvois once they have been confirmed. To do so, follow the
:ref:`invoice sending <accounting/invoice/sending>` steps, and in the :guilabel:`Send` window,
enable the :guilabel:`Send to MyInvois` option and click :guilabel:`Send & Print`.

.. _malaysia/myinvois/workflow/sending/status:

MyInvois status
***************

In the :guilabel:`MyInvois` tab of the invoice, the :guilabel:`MyInvois State` is updated to
:guilabel:`Valid` when the submission to MyInvois is successful. The :guilabel:`Submission UID`,
:guilabel:`MyInvois` and :guilabel:`Validation Time` have also been updated.
The same information is available on MyInvois.

.. note::
   If no information is received from the MyInvois portal, the :guilabel:`MyInvois State` is
   :guilabel:`In Progress`. In this case, Odoo will automatically check and update the status.

.. _malaysia/myinvois/workflow/cancellation:

Invoice cancellation
~~~~~~~~~~~~~~~~~~~~

Sent invoices can be canceled within 72 hours from :guilabel:`Validation time`. In this case, open
the invoice and click :guilabel:`Request Cancel`. In the :guilabel:`Cancel document` window, include
the cancellation :guilabel:`Reason`, then click :guilabel:`Update Invoice`. The
:guilabel:`MyInvois State` is updated to :guilabel:`cancelled`.
