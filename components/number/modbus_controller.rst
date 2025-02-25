Modbus Controller Number
========================

.. seo::
    :description: Instructions for setting up a modbus_controller device sensor.

The ``modbus_controller`` platform creates a Number from a modbus_controller.
When the Number is updated a modbus write command is created sent to the device.

Configuration variables:
------------------------

- **id** (*Optional*, :ref:`config-id`): Manually specify the ID used for code generation.
- **name** (**Required**, string): The name of the sensor.
- **address** (**Required**, int): start address of the first register in a range
- **value_type** (**Required**): datatype of the mod_bus register data. The default data type for modbus is a 16 bit integer in big endian format (MSB first)

    - ``U_WORD`` (unsigned 16 bit integer from 1 register = 16bit)
    - ``S_WORD`` (signed 16 bit integer from 1 register = 16bit)
    - ``U_DWORD`` (unsigned 32 bit integer from 2 registers = 32bit)
    - ``S_DWORD`` (signed 32 bit integer from 2 registers = 32bit)
    - ``U_DWORD_R`` (unsigned 32 bit integer from 2 registers low word first)
    - ``S_DWORD_R`` (signed 32 bit integer from 2 registers low word first)
    - ``U_QWORD`` (unsigned 64 bit integer from 4 registers = 64bit)
    - ``S_QWORD`` (unsigned 64 bit integer from 4 registers = 64bit)
    - ``U_QWORD_R`` (unsigned 64 bit integer from 4 registers low word first)
    - ``U_QWORD_R`` signed 64 bit integer from 4 registers low word first)
    - ``FP32`` (32 bit IEEE 754 floating point from 2 registers)
    - ``FP32_R`` (32 bit IEEE 754 floating point - same as FP32 but low word first)

- **skip_updates** (*Optional*, int): By default all sensors of a modbus_controller are updated together. For data points that don't change very frequently updates can be skipped. A value of 5 would only update this sensor range in every 5th update cycle
  Note: The modbus_controller groups component by address ranges to reduce number of transactions. All components with the same address will be updated in one request. skip_updates applies for all components in the same range.
- **response_size** (*Optional*): Size of the response for the register in bytes. Defaults to register_count*2.
- **force_new_range** (*Optional*, boolean): If possible sensors with sequential addresses are grouped together and requested in one range. Setting ``force_new_range: true`` enforces the start of a new range at that address.
- **offset** (*Optional*, int): only required for uncommon response encodings offset from start address in bytes. If more than one register is read a modbus read registers command this value is used to find the start of this datapoint relative to start address. The component calculates the size of the range based on offset and size of the value type
- **min_value** (*Optional*, float): The minimum value this number can be.
- **max_value** (*Optional*, float): The maximum value this number can be.
- **step** (*Optional*, float): The granularity with which the number can be set. Defaults to 1
- **custom_command** (*Optional*, list of bytes): raw bytes for modbus command. This allows using non-standard commands. If ``custom_command`` is used ``address`` and ``register_type`` can't be used.
  custom data must contain all required bytes including the modbus device address. The crc is automatically calculated and appended to the command.
  See :ref:`modbus_custom_command` how to use ``custom_command``
- **lambda** (*Optional*, :ref:`lambda <config-lambda>`):
  Lambda to be evaluated every update interval to get the new value of the sensor.

  Parameters passed into the lambda

  - **x** (float): The parsed float value of the modbus data
  - **data** (std::vector<uint8_t): vector containing the complete raw modbus response bytes for this sensor
    *note:* because the response contains data for all registers in the same range you have to use ``data[item->offset]`` to get the first response byte for your sensor.
  - **item** (const pointer to a SensorItem derived object):  The sensor object itself.

  Possible return values for the lambda:

  - ``return <FLOATING_POINT_NUMBER>;`` the new value for the sensor.
  - ``return NAN;`` if the state should be considered invalid to indicate an error (advanced).


- **write_lambda** (*Optional*, :ref:`lambda <config-lambda>`): Lambda called before send.
  Lambda is evaluated before the modbus write command is created.

  Parameters passed into the lambda

  - **x** (float): The float value to be sent to the modbus device
  - **payload** (``std::vector<uint16_t>&payload``): empty vector for the payload. The lambda can add 16 bit raw modbus register words.
    *note:* because the response contains data for all registers in the same range you have to use ``data[item->offset]`` to get the first response byte for your sensor.
  - **item** (const pointer to a SensorItem derived object):  The sensor object itself.

  Possible return values for the lambda:

  - ``return <FLOATING_POINT_NUMBER>;`` the new value for the sensor.
  - ``return <anything>; and fill payload with data`` if the payload is added from the lambda then these 16 bit words will be sent
  - ``return {};`` if you don't want write the command to the device (or do it from the lambda).

- **multiply** (*Optional*, float): multiply the new value with this factor before sending the requests. Ignored if lambda is defined.
- **use_write_multiple** (*Optional*, boolean): By default the modbus command ``Preset Single Registers`` (function code 6) is used for setting the holding register if only 1 register is set. If your device only supports ``Preset Multiple Registers`` (function code 16) set this option to true.


All other options from :ref:`Number <config-number>`.

**Example**

.. code-block:: yaml

    number:
      - platform: modbus_controller
        modbus_controller_id: epever
        id: battery_capacity_number
        name: "Battery Cap Number"
        address: 0x9001
        value_type: U_WORD
        lambda: "return  x * 1.0; "
        write_lambda: |-
          ESP_LOGD("main","Modbus Number incoming value = %f",x);
          uint16_t b_capacity = x ;
          payload.push_back(b_capacity);
          return x * 1.0 ;
        ## multiply is ignored because lamdba is used
        multiply: 1.0


See Also
--------
- :doc:`/components/modbus_controller`
- :doc:`/components/sensor/modbus_controller`
- :doc:`/components/binary_sensor/modbus_controller`
- :doc:`/components/switch/modbus_controller`
- :doc:`/components/text_sensor/modbus_controller`
- :doc:`/components/output/modbus_controller`
- https://www.modbustools.com/modbus.html
- :ghedit:`Edit`
