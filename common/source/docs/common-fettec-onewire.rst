==============
FETtec OneWire
==============

This is a half duplex serial protocol with a 2Mbit/s Baudrate created by Felix Niessen (former Flyduino KISS developer) from `FETtec <https://fettec.net/>`_.
You can change many more settings of the ESC over OneWire than over DShot.
It also has a better cyclic redundancy check (CRC) than Dshot offers.
CRC checks if there are any signal errors that occur in the communication between autopilot and ESC; and between ESC and autopilot.
It supports ESC telemetry, so information from the ESC status can be sent back to the autopilot:

- Motor rotations per minute (RPM)
- Input voltage (V)
- Current draw (A)
- Power consumption (W)
- Temperature (°C)

This information allows the autopilot to:

- dynamicaly change the center frequency of the notch filters used to reduce frame vibration noise in the gyros
- log the status of each ESC to the SDCard or internal Flash, for post flight analysis
- send the status of each ESC to the Ground Station or companion computer for real-time monitoring

Connecting
==========

The protocol supports up-to 25 ESCs, but the ArduPilot implementation of it limits this to 12.
You can connect all ESCs to a single serial port using only a single signal wire from the autopilot's UART TX pin to the ESC's TLM pin and one GND wire.
If you are using 4in1 ESCs you can connect up-to 3 of them in this fashion.

TODO: add a figure here.

Configuring
===========

To configure it you need to set the :ref:`SERIALx_PROTOCOL <common-serial-options#serialx-protocol>` parameter to `FETtec_OneWire` (38) and :ref:`SERIALx_OPTIONS <common-serial-options#serialx-options-parameter>` parameter to `HalfDuplex` (4), where x is the number of the serial port you are using.

For example, a serial 2 connection would need:

```
SERIAL2_PROTOCOL = 38
SERIAL2_OPTIONS = 4
```

Then you need to reboot the autopilot.
After that you must set the channels you want to use in the SERVO_FTW_MASK parameter, and again restart your autopilot.

For example, a quadcopter using the first four motors would need:

```
SERVO_FTW_MASK = 15


To get RPM from the telemetry you need to set the motor pole count e.g.:
SERVO_FTW_POLES = 14



```

Buying
======

Multiple ESCs are available at `FETtec <https://fettec.net>`_
