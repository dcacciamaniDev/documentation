========
Invoices
========

.. _pos_invoices/invoices:

Point of Sale allows you to issue and print invoices for :ref:`registered customers
<pos/use/customers>` upon payment and retrieve all past invoiced orders.

.. note::
   An invoice created in a POS creates an entry into the corresponding :ref:`accounting journal
   <cheat_sheet/journals>` :ref:`configured in the POS settings
   <pos_invoices/invoice_configuration>`.

.. _pos_invoices/invoice_configuration:

Configuration
=============

To define the default journals for a specific POS, go to :menuselection:`Point of Sale -->
Configuration --> Settings`, scroll down to the :guilabel:`Accounting` section, and select the
appropriate journals for :guilabel:`Orders` and :guilabel:`Invoices` under :guilabel:`Default
Journals`.

.. image:: pos_invoices/invoice-config.png
   :alt: accounting section in the POS settings
   :scale: 70 %

.. note::
   Specific journals can also be defined for each :doc:`payment method <../payment_methods>`.

Customer invoicing
==================

To invoice a customer from the :ref:`Payment screen <pos/use/sell>`, follow these steps:

#. Enable :icon:`fa-file-text-o` :guilabel:`Invoice`.
#. Click :icon:`fa-user` :guilabel:`Customer`.
#. Choose or :ref:`create a customer <pos/use/customers>`.

Continue the :ref:`payment process <pos/use/sell>`. The invoice is automatically issued and ready
for download and/or printing.

To create a single global invoice for all orders linked to the same customer or invoicing address,
follow these steps:

#. Go to :menuselection:`Point of Sale --> Orders --> Orders`.
#. Click the search bar and filter by :guilabel:`Customer`.
#. Click the :icon:`fa-caret-right` (:guilabel:`caret`) icon next to a customer to display their
   orders.
#. Tick the :guilabel:`Order Ref` checkbox, click :guilabel:`Create Invoices`, then
   :guilabel:`Create`.

.. note::
   To issue a global invoice, the orders' :guilabel:`Invoice Status` must be set to :guilabel:`To
   Invoice`.

Invoice retrieval
=================

To retrieve the invoice of a POS order, follow these steps:

#. Go to :menuselection:`Point of Sale --> Orders --> Orders`.
#. Click the relevant invoiced order in the list.
#. On the order form, click the :guilabel:`Invoice` smart button.

.. tip::
   To filter the list of orders to display only invoiced orders, click the search bar and select
   the :guilabel:`Invoiced` filter.

Invoice generation via QR codes
===============================

To allow customers to request an invoice by scanning a QR code printed on their :ref:`receipt
<pos/configuration/receipts>`, follow these steps:

#. Go to :menuselection:`Point of Sale --> Configuration --> Settings`.
#. Select the POS in the :guilabel:`Point of Sale` field, and scroll down to the :guilabel:`Bills &
   Receipts` section.
#. Enable :guilabel:`Use QR code on ticket`.

Upon scanning, customers must fill in a form with their billing information and click :guilabel:`Get
my invoice`. The invoice is then generated and available for download, and the order status is
updated to :guilabel:`Fully Invoiced`.
