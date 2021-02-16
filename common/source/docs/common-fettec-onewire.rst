FETtec OneWire
==============

This is a half duplex serial protocol with a 2Mbit/s Baudrate created by Felix Niessen (former Flyduino KISS developer) from `FETtec <https://fettec.net/>`.
For example, you can connect a 4in1 ESC with only 1 signal wire and 1 GND wire to your flight controller.
The OneWire protocol is limited to 24 ESCs per OneWire bus.
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

Configuring
===========

To configure it you need to set the SERIALx_PROTOCOL parameter to FETtec_OneWire (37) and SERIALx_OPTIONS parameter to HalfDuplex (4), where x is the number of the serial port you are using.

For example:
SERIAL2_PROTOCOL = 37
SERIAL2_OPTIONS = 4

Then you need to reboot the autopilot. After that you must set the channels you want to use in the SERVO_FTW_MASK parameter
, and again restart your autopilot.

For example, a quadcopter using the first four motors would need
SERVO_FTW_MASK = 15

Buying
======

Multiple ESCs are available at <https://fettec.net>
