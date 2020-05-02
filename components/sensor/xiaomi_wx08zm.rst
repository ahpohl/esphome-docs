Xiaomi WX08ZM BLE Sensor
========================

.. seo::
    :description: Instructions for setting up Xiaomi Mi Jia Mosquito Repellent Smart Version (Model WX08ZM) in ESPHome.
    :image: xiaomi_wx08zm.jpg
    :keywords: Xiaomi, Mi Jia, BLE, Bluetooth, WX08ZM, mosquito

The ``xiaomi_wx08zm`` sensor platform lets you track the output of the Xiaomi WX08ZM Bluetooth Low Energy device using the :doc:`/components/esp32_ble_tracker`. This component will track the tablet consumption, the sensor state (on/off) and optionally the battery level of the device every time the sensor sends out a BLE broadcast. Note that contrary to other implementations, ESPHome can track as many WX08ZM devices at once as you want.

.. figure:: images/xiaomi_wx08zm-full.jpg
    :align: center
    :width: 60.0%

    Xiaomi Mosquito Repellent over BLE.

.. code-block:: yaml

    # Example configuration entry
    esp32_ble_tracker:

    sensor:
    - platform: xiaomi_wx08zm
      mac_address: "74:a3:4a:b5:07:34"
      tablet:
        name: "WX08ZM Tablet"
      state:
        name: "WX08ZM State"
      battery_level:
        name: "WX08ZM Battery Level"

Configuration variables:
------------------------

- **mac_address** (**Required**, MAC Address): The MAC address of the Xiaomi WX08ZM device.
- **tablet** (*Optional*): The information for the sensor tablet consumption.

  - **name** (**Required**, string): The name for the tablet sensor.
  - **id** (*Optional*, :ref:`config-id`): Set the ID of this sensor for use in lambdas.
  - All other options from :ref:`Sensor <config-sensor>`.

- **state** (*Optional*): The information for the sensor on/off state

  - **name** (**Required**, string): The name for the state sensor.
  - **id** (*Optional*, :ref:`config-id`): Set the ID of this sensor for use in lambdas.
  - All other options from :ref:`Sensor <config-sensor>`.

- **battery_level** (*Optional*): The information for the battery level sensor

  - **name** (**Required**, string): The name for the battery level sensor.
  - **id** (*Optional*, :ref:`config-id`): Set the ID of this sensor for use in lambdas.
  - All other options from :ref:`Sensor <config-sensor>`.


Setting Up Devices
------------------

To set up Xiaomi WX08ZM devices you first need to find their MAC Address so that ESPHome can
identify them. So first, create a simple configuration without any ``xiaomi_lywsdcgq`` entries like so:

.. code-block:: yaml

    esp32_ble_tracker:

After uploading the ESP32 will immediately try to scan for BLE devices such as the Xiaomi LYWSDCGQ. When
it detects these sensors, it will automatically parse the BLE message print a message like this one:

.. code::

    Found device 74:a3:4a:b5:07:34 RSSI=-86
      Address Type: PUBLIC
      Name: 'MJ_MR_V1'
      TX Power: 2

Note that it can sometimes take some time for the first BLE broadcast to be received. You can speed up
the process by pressing the grey bluetooth button on the back of the device.

Then just copy the address (``74:a3:4a:b5:07:34``) into a new ``sensor.xiaomi_xm08zm`` platform entry like
in the configuration example at the top.

.. note::

    The ESPHome Xiaomi integration listens passively to packets the xiaomi device sends by itself.
    ESPHome therefore has no impact on the battery life of the device.

See Also
--------

- :doc:`/components/esp32_ble_tracker`
- :doc:`/components/sensor/xiaomi_hhccjcy01`
- :doc:`/components/sensor/index`
- :apiref:`xiaomi_lywsdcgq/xiaomi_wx08zm.h`
- `Xiaomi Mijia BLE protocol <https://github.com/mspider65/Xiaomi-Mijia-Bluetooth-Temperature-and-Humidity-Sensor>`__
  by `@mspider65 <https://github.com/mspider65>`__
- `OpenMQTTGateway <https://github.com/1technophile/OpenMQTTGateway>`__ by `@1technophile <https://github.com/1technophile>`__
- :ghedit:`Edit`
