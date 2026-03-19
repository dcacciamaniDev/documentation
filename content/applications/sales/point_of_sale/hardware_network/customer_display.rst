================
Customer display
================

The customer display feature provides real-time updates on a secondary screen for customers
during the checkout process. It shows the following information:

- :ref:`Items in the cart <pos/use/sell>`
- Unit :doc:`prices <../../point_of_sale/extra/pricing>`
- Subtotals and total amount
- :ref:`Taxes <pos/pricing/taxes>`
- :ref:`Discounts and promotions <pos/pricing/loyalty>`
- Added :ref:`notes <pos/use/notes>`
- Selected :doc:`payment method <../payment_methods>`
- Change to be returned

.. example::
   On the customer display, the customer can review their order and all amounts, including discounts
   and taxes:

   - 2 pizzas at `19.36€` each
   - An `Extra spicy` burger at `18.76€`
   - A 10% discount applied to the order
   - `8.98€` in taxes

   Finally, the customer pays `60.00€` and receives `8.27€` in change.

   .. image:: customer_display/customer-display-example.png
      :scale: 70%
      :alt: Customer display view.

.. _pos/hardware_network/display-configuration:

Configuration
=============

The customer display can be shown on either a secondary screen connected via USB-C or HDMI, or on a
screen connected through an :ref:`IoT box <pos/hardware_network/display-configuration-iot>`.

The customer display feature is built in, but the background image can be customized. To do so, go
to the :ref:`POS settings <pos/use/settings>` and scroll down to the :guilabel:`Connected Devices`
section. Under :guilabel:`Customer Display`, click :guilabel:`Upload your file` to set a
background image.

.. note::
   Both the customer and POS displays must have a minimum diagonal size of 6 inches. For optimal
   readability, larger screens are recommended.

.. _pos/hardware_network/display-configuration-iot:

Using an IoT box
----------------

To connect a display via an :doc:`IoT system </applications/general/iot>`:

#. Navigate to the :ref:`POS settings <pos/use/settings>`.
#. Scroll down to the :guilabel:`Connected Devices` section.
#. Enable the :guilabel:`IoT Box` option.
#. Click :guilabel:`Save` to install the IoT app in Odoo (if not already installed).
#. :doc:`Connect and configure an IoT system </applications/general/iot/connect>` for the
   :doc:`screen </applications/general/iot/devices/screen>`.
#. Return to the :guilabel:`Connected Devices` section and select an IoT-connected screen in the
   :guilabel:`Customer Display` field for the :guilabel:`IoT Box`.

.. tip::
   This configuration is especially useful for connecting tablets.

.. _pos/hardware_network/open-display:

Opening the customer display
============================

To open the customer display, follow these steps:

#. :ref:`Access the POS register <pos/use/open-register>`.
#. Click the :icon:`fa-bars` (:guilabel:`hamburger menu`) icon in the upper-right corner.
#. Click the :icon:`fa-desktop` (:guilabel:`Customer Display`) icon.
#. On the :guilabel:`Open Customer Display` pop-up, choose the device to use for the customer
   display:

   - :guilabel:`This device`: Use this option if a secondary screen is connected via USB-C or
     HDMI, then drag the customer display window to that screen.
   - :guilabel:`Display QR`: Scan the QR code to open the customer display on any internet-connected
     device.

.. note::
   For IoT-connected screens, the customer display opens automatically on the connected device. Make
   sure both devices are connected to the same :doc:`local network <pos_lna>`.

.. tip::
   For POS terminals running the
   `Odoo Android app <https://play.google.com/store/apps/details?id=com.odoo.mobile>`_ with
   dual screens, :doc:`activate the Point of Sale Mobile module <../../../general/apps_modules>`.
   To use the customer display, :ref:`open it <pos/hardware_network/open-display>`, and
   :guilabel:`Select a display`.

.. seealso::
   - :doc:`pos_iot`
   - :doc:`../../../general/iot`
