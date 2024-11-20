==============
United Kingdom
==============

.. _localization/united-kingdom/modules:

Configuration
=============

:ref:`Install <general/install>` the :guilabel:`UK - Accounting` and the :guilabel:`UK - Accounting
Reports` modules to get all the features of the UK localization.

.. list-table::
   :header-rows: 1

   * - Name
     - Technical name
     - Description
   * - :guilabel:`UK - Accounting`
     - `l10n_uk`
     -  - CT600-ready chart of accounts
        - VAT100-ready tax structure
        - Infologic UK counties listing
   * - :guilabel:`UK - Accounting Reports`
     - `l10n_uk_reports`
     -  - Accounting reports for the UK
        - Allows sending the tax report via the MTD-VAT API to HMRC.
   * - :guilabel:`UK BACS Payment Files`
     - `l10n_uk_bacs`
     - Allows generating :ref:`localization/united-kingdom/BACS-files` for bill and invoice payments

.. note::
   - Only UK-based companies can submit reports to HMRC.
   - Installing the module :guilabel:`UK - Accounting Reports` installs all two modules at once.
   - In the UK construction industry, deductions under the :ref:`Construction Industry Scheme (CIS)
     <localization/united-kingdom/cis-deduction>` are required.

.. seealso::
   - `HM Revenue & Customs <https://www.gov.uk/government/organisations/hm-revenue-customs/>`_
   - `Overview of Making Tax Digital
     <https://www.gov.uk/government/publications/making-tax-digital/overview-of-making-tax-digital/>`_

.. _localization/united-kingdom/chart-of-account:

Chart of accounts
=================

The UK chart of accounts is included in the :guilabel:`UK - Accounting` module. Go to
:menuselection:`Accounting --> Configuration --> Accounting: Chart of Accounts` to access it.

Setup your :abbr:`CoA (chart of accounts)` by going to :menuselection:`Accounting --> Configuration
--> Settings --> Accounting Import section` and choose to :guilabel:`Review Manually` or
:guilabel:`Import (recommended)` your initial balances.

.. _localization/united-kingdom/taxes:

Taxes
=====

As part of the localization module, UK taxes are created automatically with their related financial
accounts and configuration.

Go to :menuselection:`Accounting --> Configuration --> Settings --> Taxes` to update the
:guilabel:`Default Taxes`, the :guilabel:`Tax Return Periodicity` or to :guilabel:`Configure your
tax accounts`.

To edit existing taxes or to :guilabel:`Create` a new tax, go to :menuselection:`Accounting -->
Configuration --> Accounting: Taxes`.

.. seealso::
   - :doc:`taxes <../accounting/taxes>`
   - Tutorial: `Tax report and return
     <https://www.odoo.com/slides/slide/tax-report-and-return-1719?fullscreen=1>`_.

.. _localization/united-kingdom/digital-tax:

Making Tax Digital (MTD)
------------------------

In the UK, all VAT-registered businesses have to follow the MTD rules by using software to submit
their VAT returns.

The **UK - Accounting Reports** module enables you to comply with the `HM Revenue & Customs
<https://www.gov.uk/government/organisations/hm-revenue-customs/>`_ requirements regarding
`Making Tax Digital
<https://www.gov.uk/government/publications/making-tax-digital/overview-of-making-tax-digital/>`_.

.. important::
   If your periodic submission is more than three months late, it is no longer possible to submit
   it through Odoo, as Odoo only retrieves open bonds from the last three months. Your submission
   has to be done manually by contacting HMRC.

.. _localization/united-kingdom/hmrc-registration:

Register your company to HMRC before the first submission
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Go to :menuselection:`Accounting --> Reporting --> Tax report` and click on
:guilabel:`Connect to HMRC`. Enter your company information on the HMRC platform. You only need to
do it once.

.. _localization/united-kingdom/periodic-hmrc-submission:

Periodic submission to HMRC
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Import your obligations HMRC, filter on the period you want to submit, and send your tax report by
clicking :guilabel:`Send to HMRC`.

.. tip::
   You can use dummy credentials to demo the HMRC flow. To do so, activate the
   :ref:`developer mode <developer-mode>` and go to :menuselection:`General Settings -->
   Technical --> System Parameters`. From here, search for `l10n_uk_reports.hmrc_mode` and change
   the value line to `demo`. You can get such credentials from the `HMRC Developer Hub
   <https://developer.service.hmrc.gov.uk/api-test-user>`_.

.. _localization/united-kingdom/periodic-hmrc-submission-multi:

Periodic submission to HMRC for multi-company
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Only one company and one user can connect to HMRC simultaneously. If several UK-based companies are
on the same database, the user who submits the HMRC report must follow these instructions before
each submission:

#. Log into the company for which the submission has to be done.
#. Go to :guilabel:`General Settings`, and in the :guilabel:`Users` section, click
   :guilabel:`Manage Users`. Select the user who is connected to HMRC.
#. Go to the :guilabel:`UK HMRC Integration` tab and click :guilabel:`Reset Authentication
   Credentials` or :guilabel:`Remove Authentication Credentials` button.
#. You can now :ref:`register your company to HMRC <localization/united-kingdom/hmrc-registration>`
   and submit the tax report for this company.
#. Repeat the steps for other companies' HMRC submissions.

.. note::
   During this process, the :guilabel:`Connect to HMRC` button no longer appears for other UK-based
   companies.

.. _localization/united-kingdom/BACS-files:

Bacs files
==========

:abbr:`Bacs (Bankers' Automated Clearing Services)` files are electronic files used in the UK to
process payments and transfers between bank accounts.

To enable the use of Bacs files, make sure the
:ref:`UK BACS Payment Files <localization/united-kingdom/modules>` module is installed, then:

#. Configure your Bacs Service User Number:

   #. Go to :menuselection:`Accounting --> Configuration --> Settings` and scroll down to the
      :guilabel:`Customer Payments` section.
   #. Enter your :guilabel:`Service User Number` under :guilabel:`BACS` and manually save.

#. Configure your **bank** journal:

   #. Go to :menuselection:`Accounting --> Configuration --> Journals` and select your **bank**
      journal.
   #. In the :guilabel:`Journal Entries` tab, configure the :guilabel:`Account Number` and
      :guilabel:`Bank` fields.
   #. In the :guilabel:`Incoming Payments` and :guilabel:`Outgoing Payments` tabs, make sure the
      :guilabel:`BACS Direct Debit` payment method is enabled.

#. Configure the contacts for whom you wish to use Bacs files: Access the contact form and, in
   the :guilabel:`Accounting` tab, click :guilabel:`Add a line` and fill in the
   :guilabel:`Account Number` and :guilabel:`Bank` fields.

.. _localization/united-kingdom/bill-payments:

Bill payments
-------------

To generate Bacs files for bill payments, set the :guilabel:`Payment Method` to
:guilabel:`BACS Direct Debit` when :ref:`registering vendor payments <batch-payments/register-payments>`.

Then, create a vendor batch payment:

#. Go to :menuselection:`Accounting --> Vendors --> Batch Payments`, and click :guilabel:`New`.
#. Select the bank journal in the :guilabel:`Bank` field, set the :guilabel:`Payment Method` to
   :guilabel:`BACS Direct Credit`, and select a :guilabel:`BACS Processing Date`.
#. Optionally, you can also:

   - select a :guilabel:`BACS Expiry Date`;
   - enable :guilabel:`BACS Multi Mode` to process the payments on their individual date.

#. Click :guilabel:`Add a line`, select the payments you want to include, click :guilabel:`Select`,
   then :guilabel:`Validate`.

Once validated, the Bacs file is available in the chatter. You can also :guilabel:`Re-generate
Export File` if you need a new Bacs file for that batch payment.

.. image:: united_kingdom/bacs-files.png
   :alt: Vendor Batch Payment view with generated BACS file.

.. _localization/united-kingdom/invoice-payments:

Invoice payments
----------------

Before generating Bacs files for invoice payments, you must first create a **BACS Direct Debit
Instruction**: Go to :menuselection:`Accounting --> Customers --> BACS Direct Debit Instructions`
and click :guilabel:`New`. Select a :guilabel:`Customer`, their :guilabel:`IBAN`, and the
:guilabel:`Journal` you wish to use.

To generate Bacs files for invoice payments, set the :guilabel:`Payment Method` to
:guilabel:`BACS Direct Debit` when :ref:`registering invoice payments <batch-payments/register-payments>`.

.. tip::
   If you register the payment for an invoice linked to a subscription or via
   :menuselection:`Accounting --> Customers --> Payments`, you can select the :guilabel:`BACS
   Payment Type`:

   - :guilabel:`Direct debit-first collection of a series`;
   - :guilabel:`Direct debit single collection`;
   - :guilabel:`Direct debit repeating collection in a series`;
   - :guilabel:`Direct debit-final collection of a series`.

Then, create a customer batch payment:

#. Go to :menuselection:`Accounting --> Customers --> Batch Payments`, and click :guilabel:`New`.
#. Select the bank journal in the :guilabel:`Bank` field, set the :guilabel:`Payment Method` to
   :guilabel:`BACS Direct Credit`, and select a :guilabel:`BACS Processing Date`.
#. Optionally, you can also:

   - select a :guilabel:`BACS Expiry Date`;
   - enable :guilabel:`BACS Multi Mode` to process the payments on their individual date.

#. Click :guilabel:`Add a line`, select the payments you want to include, click :guilabel:`Select`,
   then :guilabel:`Validate`.

Once validated, the Bacs file is available in the chatter. You can also :guilabel:`Re-generate
Export File` if you need a new Bacs file for that batch payment.

.. _localization/united-kingdom/employment-hero:

Employment Hero payroll
=======================

If your business is already up and running with :doc:`Employment Hero <employment_hero>`, you can
use our connector as an alternative payroll solution.

.. important::
   To :ref:`configure the Employment Hero API <employment_hero/configuration>` for **United
   Kingdom**, use the following value as :guilabel:`Payroll URL`: `https://api.yourpayroll.co.uk/`.

.. _localization/united-kingdom/cis-deduction:

.. |HMRC| replace:: :abbr:`HMRC (HM Revenue and Customs)`
.. |CIS| replace:: :abbr:`CIS (Construction Industry Scheme)`

CIS deduction
=============

The Construction Industry Scheme deduction (CIS deduction) is a tax deduction system used in the UK
construction industry. Contractors deduct a percentage from a subcontractor’s payments and pass it
to HM Revenue and Customs (HMRC). These deductions apply only to the labour portion of the payments
and count as advance payments for the subcontractor’s tax and National Insurance. Contractors are
required to register for the scheme, but subcontractors are not. However, subcontractors who are not
registered face higher payment deductions. Under the |CIS|, contractors must deduct 20% from
payments to registered subcontractors, while the deduction increases to 30% for the unregistered
ones.

.. seealso::

   - `Construction Industry Scheme (CIS) <https://www.gov.uk/what-is-the-construction-industry-scheme>`_
   - `What you must do as a Construction Industry Scheme (CIS) contractor
     <https://www.gov.uk/what-you-must-do-as-a-cis-contractor>`_
   - `What you must do as a Construction Industry Scheme (CIS) subcontractor
     <https://www.gov.uk/what-you-must-do-as-a-cis-subcontractor>`_
   - `Construction Industry Scheme: a guide for contractors and subcontractors (CIS 340)
     <https://www.gov.uk/government/publications/construction-industry-scheme-cis-340/construction-industry-scheme-a-guide-for-contractors-and-subcontractors-cis-340>`_

.. _localization/united-kingdom/cis-contractors:

Contractors
-----------

Contractors are required to register for the |CIS| before hiring subcontractors and must verify that
each subcontractor is registered under the |CIS|. They are also responsible for maintaining records
of all payments and deductions. Additionally, contractors must submit monthly returns to HMRC,
including the following details:

- Information about the subcontractors.
- Records of payments made and any deductions applied.
- A declaration confirming that the employment status of all subcontractors has been reviewed.
- A declaration confirming that all subcontractors requiring verification have been verified.

.. note::
   If no payments were made to subcontractors in the previous tax month, contractors must notify
   |HMRC| by the 19th of the month to avoid a penalty.

.. _localization/united-kingdom/cis-configuration:

Configuration
-------------

:ref:`Install <general/install>` the :guilabel:`UK - Construction Industry Scheme` module.

.. list-table::
   :header-rows: 1

   * - Name
     - Technical name
     - Description
   * - :guilabel:`UK - Construction Industry Scheme`
     - `l10n_uk_reports_cis`
     -  - Allows sending the Monthly return to |HMRC|
        - CIS Deduction (GB) report for UK construction industry
   * - :guilabel:`UK - HMRC API`
     - `l10n_uk_hmrc`
     -  - Includes the basics of |HMRC|.

.. note::
   Installing the :guilabel:`UK - Construction Industry Scheme` module installs the other module
   simultaneously.

To enable the :guilabel:`Test` mode and use test credentials, activate
:ref:`developer mode <developer-mode>` and go to :menuselection:`Settings --> Technical -->
System Parameters`. Then search for `l10n_uk_hmrc.api_mode`. Select it and switch the value from
`production` to `test`.

.. _localization/united-kingdom/cis-monthly-returns:

Monthly returns
---------------

Monthly returns only work for vendor bills and vendor refunds. To submit a complete return to
|HMRC|, several steps must be followed to report all payments made to subcontractors under the
scheme during the previous tax month:

- :ref:`localization/united-kingdom/cis-contractor-setup`
- :ref:`localization/united-kingdom/cis-subcontractor-setup`
- :ref:`localization/united-kingdom/cis-vendorbills`
- :ref:`localization/united-kingdom/cis-monthly-return-sending`

.. _localization/united-kingdom/cis-contractor-setup:

Contractor setup
~~~~~~~~~~~~~~~~

To configure the company |HMRC| information, go to the :guilabel:`Settings` app. In the
:guilabel:`Companies` section, click :guilabel:`Manage Companies` and select the company. Open the
:guilabel:`HMRC` tab and configure the information in the :guilabel:`HMRC Credentials` and the
:guilabel:`Contractor details` sections. All the fields are mandatory.

.. _localization/united-kingdom/cis-subcontractor-setup:

Subcontractor setup
~~~~~~~~~~~~~~~~~~~

In the :guilabel:`Contacts` app, open the subcontractor's contact form and select the
:guilabel:`Accounting` tab. In the :guilabel:`HMRC Details` section, enable the
:guilabel:`Construction Industry Scheme` option to unlock the additional fields.

By default, the :guilabel:`Deduction rate` is set to 30%. To modify it, a
:guilabel:`Verification Number` is required. The verification number is provided by |HMRC| when
verifying the contact. Make sure to check the status of the subcontractor and update the
:guilabel:`Deduction Rate` accordingly.

The :guilabel:`Forename` and :guilabel:`Surname` fields are mandatory if the contact is set to
:guilabel:`Individual`.

.. _localization/united-kingdom/cis-vendorbills:

Vendor bills
~~~~~~~~~~~~

Additional |CIS| tax must be applied to labour line items on vendor bills. Material line items
on vendor bills do not apply. The tax rate corresponds to the subcontractor's
:guilabel:`deduction rate`: :guilabel:`O% CIS`, :guilabel:`20% CIS` or :guilabel:`30% CIS`. To apply
this, in the :guilabel:`Invoice Lines` section of the vendor bill, select the appropriate |CIS| tax
rate in the :guilabel:`Taxes` column of the labour line items.

.. note::
   - When creating a vendor bill, if the :guilabel:`Construction Industry Scheme` option hasn't been
     enabled in the :ref:`subcontractor <localization/united-kingdom/cis-subcontractor-setup>`'s
     :guilabel:`Contact` form, a yellow warning banner appears at the top of the page.
   - If the |CIS| tax used in the vendor bill does not match the expected |CIS| deduction rate for a
     :ref:`subcontractor <localization/united-kingdom/cis-subcontractor-setup>`, a yellow warning
     banner appears at the top of the page.

.. _localization/united-kingdom/cis-monthly-return-sending:

Monthly returns sending
~~~~~~~~~~~~~~~~~~~~~~~

On the 6th of each month, Odoo sends a reminder email to submit a monthly return to |HMRC|. The
recipient email address is the one entered in the company :guilabel:`Email` field. To send monthly
returns to |HMRC|, go to :menuselection:`Accounting --> Reporting --> Tax Return` and follow these
steps:

#. Click :icon:`fa-book` :guilabel:`Report:` and select :guilabel:`CIS Deduction (GB)`.
#. In the :icon:`fa-calendar` :guilabel:`(calendar)` date selector, the :guilabel:`Tax Period` is
   automatically adjusted to match the |CIS| deduction period.
#. Click on :guilabel:`Send to HMRC` in the top-left corner.
#. In the :guilabel:`CIS monthly return` window, select the required options in the
   :guilabel:`Declaration` section.

   - :guilabel:`Employment Status`: To declare that the employment status of all subcontractors has
     been reviewed.
   - :guilabel:`Subcontractor Verification`: To declare that all submitted subcontractors requiring
     verification have been verified.
   - :guilabel:`Inactivity Indicator`: To declare temporary inactivity.

#. In the :guilabel:`Information correct declaration` section, confirm that the information is true
   and complete by checking the box. Then, enter the :guilabel:`Password` used in the
   :guilabel:`HMRC Credentials` section during
   :ref:`contractor setup <localization/united-kingdom/cis-contractor-setup>`.
#. Click :guilabel:`Send` to prompt Odoo to request |HMRC| to initiate the transaction.

When the transaction results in a response from |HMRC|, Odoo automatically emails the user who
submitted the transaction, informing them that the response from |HMRC| is available in the chatter
section of the company page. If an error has been detected in the submission, a new submission will
be required to ensure compliance with |HMRC| requirements.

The transaction response from |HMRC| appears in the company chatter with an attached
:guilabel:`XML` document. The message specifies the relevant period. To download the
:guilabel:`XML` document, click on the :icon:`fa-download` :guilabel:`(download)` icon. Both the
electronic and paper versions of the |HMRC| receipt should be retained.

.. note::
   - Transactions are updated daily. To manually update the |HMRC| request, click the :icon:`fa-cog`
     :guilabel:`(cog)` icon and select :guilabel:`Refresh HMRC request`.
   - |CIS| invoices are included in the :guilabel:`CIS Deduction (GB)` report but are not sent to
     |HMRC|.
