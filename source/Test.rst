.. |br| raw:: html

     <br/>

BFQ4004

Dual-band Wi-Fi Module

AT Command Reference

July 2020

Overview
========

BFQ4004 AT Firmware, officially launched by BeeFi Technologies
(hereafter “BeeFi”), is available for download and can be used directly.
Users may also find AT Project where BeeFi created example demo code for
users to customize their AT firmware.

.. code-block:: python

    def some_function():
        interesting = False
                      print 'This line is highlighted.'
                      print 'This one is not...'
                      print '...but this one is.'

.. important::
    -  *Please make sure that correct binary file (.bin) has been installed     in BFQ4004 module before using the AT commands in this document.* |br|
    -  *AT firmware uses priority levels* *and 1 of system_os_task, so only     one task of priority 2 is allowed to be set up by user application.* |br|

This document provides detailed information about the BF4004Q WiFi
module AT commands. It also introduces how to download firmware images
onto the flash on the module as well as some customization examples.

.. note::
     -  *Please make sure that correct binary file (.bin) has been installed     in BFQ4004 module before using the AT commands in this document.* |br|
     -  *AT firmware uses priority levels* *and 1 of system_os_task, so only     one task of priority 2 is allowed to be set up by user application.* |br|

.. attention::
     *Please make sure that correct binary file (.bin) has been installed     in BFQ4004 module before using the AT commands in this document.* |br|
   
     
 


Command Types and Formats
=========================

Each command set contains four types of AT commands.

.. table::
    :widths: 30,35,35

+-----------------+--------------------+-----------------------------+
| **Type**        | **Command Format** | **Description**             |
+=================+====================+=============================+
| Test Command    | AT+<X>=?           | Queries the Set Commands’   |
|                 |                    | internal parameters and     |
|                 |                    | their range of values.      |
+-----------------+--------------------+-----------------------------+
| Query Command   | AT+<X>?            | Returns the current value   |
|                 |                    | of parameters.              |
+-----------------+--------------------+-----------------------------+
| Set Command     | AT+<X>=<…>         | Sets the value of           |
|                 |                    | user-defined parameters in  |
|                 |                    | commands, and runs these    |
|                 |                    | commands.                   |
+-----------------+--------------------+-----------------------------+
| Execute Command | AT+<X>             | Runs commands with no       |
|                 |                    | user-defined parameter.     |
+-----------------+--------------------+-----------------------------+

.. note::
     -  *Not all AT commands support all four varioations mentioned above.* |br|
     -  *Square brackets “[]” designate the default value. It is not always     required or may not appear.* |br|
     -  *String values need to be included in double quotation markets, for     example:     AT+CWSAP_CUR=”BFQ4004A”,”123456789”,1,4* |br|
     -  *The default baud rate is 1152.* |br|
     -  *AT commands have to be capitalized and must end with a new line (CR     LF).* |br|


Basic AT Commands
=================

.. _overview-1:

Overview
--------

============ =====================================================
**Commands** **Description**
============ =====================================================
AT           Tests AT startup.
ATE          Configures echoing of AT commands.
AT+RST       Restarts the module.
AT+GMR       Checks AT commands version information.
AT+RESTORE   Restores the factory settings.
AT+UART_CUR  The current UART configuration.
AT+UART_DEF  The default UART configuration, saved in flash.
AT+SYSRAM    Checks the available RAM space.
AT+SLEEP     Configures the operating modes for power optimization
AT+GSLP      Enters suspend (deep-sleep) mode.
AT+RFPOWER   Sets the maximum RF TX power.
============ =====================================================

Command Descriptions
--------------------

AT – Tests AT Startup
~~~~~~~~~~~~~~~~~~~~~

.. table::
    :widths: 50,50
    
=================== ==
**Execute Command** AT
**Response**        OK
**Parameters**      \-
=================== ==

AT+ATE – Configures Echoing of AT Commands
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+---------------------+-----------------------------------------------+
| **Execute Command** | ATE                                           |
+---------------------+-----------------------------------------------+
| **Response**        | OK                                            |
+---------------------+-----------------------------------------------+
| **Parameters**      | -  ATE=: switches echo off.                   |
|                     |                                               |
|                     | -  ATE=1: switches echo on.                   |
+---------------------+-----------------------------------------------+
| **Notes**           | This command is used to configure command     |
|                     | echoing. It means that entered commands are   |
|                     | echoed back to the sender when ATE is set to  |
|                     | 1. Two settings are possible. The command     |
|                     | returns OK in normal case and ERROR when a    |
|                     | parameter other than or 1 was specified.      |
+---------------------+-----------------------------------------------+

AT+RST – Restarts the Module
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

=================== ======
**Execute Command** AT+RST
**Response**        OK
**Parameters**      \-
=================== ======

AT+GMR – Checks AT Commands Version Information
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

=================== ==================
**Execute Command** AT+GMR
**Response**        <AT version info>
                    
                    <SDK version info>
                    
                    <compile time>
                    
                    OK
**Parameters**      \-
=================== ==================

AT+RESTORE – Restores Factory Settings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+---------------------+-----------------------------------------------+
| **Execute Command** | AT+RESTORE                                    |
+---------------------+-----------------------------------------------+
| **Response**        | OK                                            |
+---------------------+-----------------------------------------------+
| **Notes**           | The execution of this command resets all      |
|                     | parameters saved in flash, and restores the   |
|                     | factory default settings of the module. The   |
|                     | chip will be restarted when this command is   |
|                     | executed.                                     |
+---------------------+-----------------------------------------------+

AT+UART_CUR – Current UART Configuration in RAM
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-------------------------+
| **Command**    | Query:                  | Set:                    |
|                | AT+UART_CUR?            | AT+UART_CUR=<baudrate>, |
|                |                         | <databit                |
|                |                         | s>,<stopbits>,<parity>, |
|                |                         | <flow control>          |
+----------------+-------------------------+-------------------------+
| **Response**   | | +UART_CUR:<baudrate>, | OK                      |
|                | | <databit              |                         |
|                | s>,<stopbits>,<parity>, |                         |
|                | | <flow control>        |                         |
|                |                         |                         |
|                | OK                      |                         |
+----------------+-------------------------+-------------------------+
| **Notes**      | Command AT+UART_CUR?    | \-                      |
|                | will return the actual  |                         |
|                | value of UART           |                         |
|                | configuration           |                         |
|                | parameters, which may   |                         |
|                | have allowable errors   |                         |
|                | compared with the set   |                         |
|                | value because of the    |                         |
|                | clock division.         |                         |
|                |                         |                         |
|                | For example, if the     |                         |
|                | UART baud rate is set   |                         |
|                | as 1152, the baud rate  |                         |
|                | returned by using       |                         |
|                | command AT+UART_CUR?    |                         |
|                | could be 115273.        |                         |
+----------------+-------------------------+-------------------------+
| **Parameters** | -  <baudrate>: UART                               |
|                |    baud rate                                      |
|                |                                                   |
|                | -  <databits>: data                               |
|                |    bits                                           |
|                |                                                   |
|                |    -  5: 5-bit data                               |
|                |                                                   |
|                |    -  6: 6-bit data                               |
|                |                                                   |
|                |    -  7: 7-bit data                               |
|                |                                                   |
|                |    -  8: 8-bit data                               |
|                |                                                   |
|                | -  <stopbits>: stop                               |
|                |    bits                                           |
|                |                                                   |
|                |    -  1: 1-bit stop bit                           |
|                |                                                   |
|                |    -  2: 1.5-bit stop                             |
|                |       bit                                         |
|                |                                                   |
|                |    -  3: 2-bit stop bit                           |
|                |                                                   |
|                | -  <parity>: parity bit                           |
|                |                                                   |
|                |    -  : None                                      |
|                |                                                   |
|                |    -  1: Odd                                      |
|                |                                                   |
|                |    -  2: Even                                     |
|                |                                                   |
|                | -  <flow control>: flow                           |
|                |    control                                        |
|                |                                                   |
|                |    -  : flow control is                           |
|                |       not enabled                                 |
|                |                                                   |
|                |    -  1: enable RTS                               |
|                |                                                   |
|                |    -  2: enable CTS                               |
|                |                                                   |
|                |    -  3: enable both                              |
|                |       RTS and CTS                                 |
+----------------+-------------------------+-------------------------+
| **Notes**      | 1. The configuration                              |
|                |    changes will NOT be                            |
|                |    saved in the flash.                            |
|                |                                                   |
|                | 2. The use of flow                                |
|                |    control requires the                           |
|                |    support of hardware:                           |
|                |                                                   |
|                |    -  GPIO9 is UART CTS                           |
|                |                                                   |
|                |    -  GPIO8 is UART RTS                           |
|                |                                                   |
|                |    -  There are 2 UART                            |
|                |       ports, only UART                            |
|                |       has flow control                            |
|                |       (4-wire)                                    |
|                |                                                   |
|                | 3. The range of baud                              |
|                |    rates supported:                               |
|                |    110~115200*4.                                  |
+----------------+-------------------------+-------------------------+
| **Examples**   | AT+UART_CUR=1152,8,1,,3                           |
+----------------+-------------------------+-------------------------+

AT+UART_DEF – Default UART Configuration from Flash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-------------------------+
| **Command**    | Query:                  | Set:                    |
|                | AT+UART_DEF?            | AT+UART_DEF=<baudrate>, |
|                |                         | <databit                |
|                |                         | s>,<stopbits>,<parity>, |
|                |                         | <flow control>          |
+----------------+-------------------------+-------------------------+
| **Response**   | | +UART_DEF:<baudrate>, | OK                      |
|                | | <databit              |                         |
|                | s>,<stopbits>,<parity>, |                         |
|                | | <flow control>        |                         |
|                |                         |                         |
|                | OK                      |                         |
+----------------+-------------------------+-------------------------+
| **Parameters** | -  <baudrate>: UART                               |
|                |    baud rate                                      |
|                |                                                   |
|                | -  <databits>: data                               |
|                |    bits                                           |
|                |                                                   |
|                |    -  5: 5-bit data                               |
|                |                                                   |
|                |    -  6: 6-bit data                               |
|                |                                                   |
|                |    -  7: 7-bit data                               |
|                |                                                   |
|                |    -  8: 8-bit data                               |
|                |                                                   |
|                | -  <stopbits>: stop                               |
|                |    bits                                           |
|                |                                                   |
|                |    -  1: 1-bit stop bit                           |
|                |                                                   |
|                |    -  2: 1.5-bit stop                             |
|                |       bit                                         |
|                |                                                   |
|                |    -  3: 2-bit stop bit                           |
|                |                                                   |
|                | -  <parity>: parity bit                           |
|                |                                                   |
|                |    -  : None                                      |
|                |                                                   |
|                |    -  1: Odd                                      |
|                |                                                   |
|                |    -  2: Even                                     |
|                |                                                   |
|                | -  <flow control>: flow                           |
|                |    control                                        |
|                |                                                   |
|                |    -  : flow control is                           |
|                |       not enabled                                 |
|                |                                                   |
|                |    -  1: enable RTS                               |
|                |                                                   |
|                |    -  2: enable CTS                               |
|                |                                                   |
|                |    -  3: enable both                              |
|                |       RTS and CTS                                 |
+----------------+-------------------------+-------------------------+
| **Notes**      | 1. The configuration                              |
|                |    changes will be                                |
|                |    saved in the user                              |
|                |    parameter area in                              |
|                |    the flash and will                             |
|                |    still be valid when                            |
|                |    the chip is powered                            |
|                |    on again after                                 |
|                |    shutdown.                                      |
|                |                                                   |
|                | 2. The use of flow                                |
|                |    control requires the                           |
|                |    support of hardware:                           |
|                |                                                   |
|                |    -  GPIO9 is UART CTS                           |
|                |                                                   |
|                |    -  GPIO8 is UART RTS                           |
|                |                                                   |
|                |    -  There are 2 UART                            |
|                |       ports, only UART                            |
|                |       has flow control                            |
|                |       (4-wire)                                    |
|                |                                                   |
|                | 3. The range of baud                              |
|                |    rates supported:                               |
|                |    110~115200*4.                                  |
+----------------+-------------------------+-------------------------+
| **Examples**   | AT+UART_DEF=1152,8,1,                             |
|                | ,3                                                |
+----------------+-------------------------+-------------------------+

AT+SYSRAM – Checks the Remaining Space on RAM
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-------------------+---------------------------------------------------------+
| **Query Command** | AT+SYSRAM?                                              |
+-------------------+---------------------------------------------------------+
| **Response**      | +SYSRAM:<remaining RAM size>                            |
|                   |                                                         |
|                   | OK                                                      |
+-------------------+---------------------------------------------------------+
| **Notes**         | <remaining RAM size>: remaining space of RAM, in bytes. |
+-------------------+---------------------------------------------------------+

AT+SLEEP – Configures the Operating Modes for Power Optimization
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-----------------------+
| **Command**    | Query:                  | Set:                  |
|                | AT+SLEEP?               | AT+SLEEP=<sleep mode> |
+----------------+-------------------------+-----------------------+
| **Response**   | +SLEEP:<sleep mode>     | OK                    |
|                |                         |                       |
|                | OK                      |                       |
+----------------+-------------------------+-----------------------+
| **Parameters** | -  <sleep mode>:                                |
|                |                                                 |
|                |    -  : Disable sleep                           |
|                |          mode                                   |
|                |                                                 |
|                |       (high-performance                         |
|                |          mode)                                  |
|                |                                                 |
|                |    -  1: Sleep mode                             |
|                |                                                 |
|                |    -  2: Associated                             |
|                |          mode                                   |
+----------------+-------------------------+-----------------------+
| **Notes**      | This command can only                           |
|                | be used in Station                              |
|                | mode. Associated mode                           |
|                | is the default mode.                            |
|                |                                                 |
|                | 1. “Disable sleep”                              |
|                |    means chip host CPU                          |
|                |    and everything else                          |
|                |    are all powered on.                          |
|                |    This is the highest                          |
|                |    power-consumption                            |
|                |    mode and also the                            |
|                |    highest performance                          |
|                |    mode.                                        |
|                |                                                 |
|                | 2. “Sleep” means WLAN                           |
|                |    blocks are powered                           |
|                |    down and clocks are                          |
|                |    suspended, and                               |
|                |    BFQ4004 is                                   |
|                |    disconnected from                            |
|                |    access point.                                |
|                |                                                 |
|                | 3. “Associated” means                           |
|                |    BFQ4004 is duty                              |
|                |    cycling between                              |
|                |    sleep state and                              |
|                |    active WLAN TX, RX.                          |
|                |    It is used to allow                          |
|                |    BFQ4004 to                                   |
|                |    periodically wake up                         |
|                |    and listen for                               |
|                |    beacon signals from                          |
|                |    access point (AP) to                         |
|                |    maintain the                                 |
|                |    connection with the                          |
|                |    AP.                                          |
+----------------+-------------------------+-----------------------+
| **Examples**   | AT+SLEEP=0                                      |
+----------------+-------------------------+-----------------------+

AT+GSLP – Enters Suspend (Deep-sleep) Mode
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-----------------+---------------------------------------------------+
| **Set Command** | AT+GSLP=<time>                                    |
+-----------------+---------------------------------------------------+
| **Response**    | <time>                                            |
|                 |                                                   |
|                 | OK                                                |
+-----------------+---------------------------------------------------+
| **Parameters**  | <time>: the milliseconds (ms) BFQ4004 stays in    |
|                 | suspend mode.                                     |
+-----------------+---------------------------------------------------+
| **Notes**       | In suspend mode only the wakeup manager and PMU   |
|                 | are powered with everything else powered down. It |
|                 | is the lowest power consumption mode at the       |
|                 | expense of a longer wakeup latency.               |
|                 |                                                   |
|                 | BFQ4004 can exit suspend mode in 2 ways:          |
|                 |                                                   |
|                 | 1. The synchronous internal timer expired after   |
|                 |    <time> milliseconds; or                        |
|                 |                                                   |
|                 | 2. An asynchronous event is detected on the       |
|                 |    WAKEUP pin.                                    |
+-----------------+---------------------------------------------------+

AT+RFPOWER – Sets Maximum of RF TX Power
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-----------------+---------------------------------------------------+
| **Set Command** | AT+RFPOWER=<TX power>                             |
+-----------------+---------------------------------------------------+
| **Response**    | OK                                                |
+-----------------+---------------------------------------------------+
| **Parameters**  | <TX power>: the maximum value of RF TX power,     |
|                 | range: [0, 82] in 0.25dBm unit                    |
+-----------------+---------------------------------------------------+
| **Notes**       | This command sets the maximum value of BFQ4004 RF |
|                 | TX power. It is not precise. The actual value     |
|                 | could be smaller than the set value.              |
+-----------------+---------------------------------------------------+
| **Examples**    | AT+RFPOWER=50                                     |
+-----------------+---------------------------------------------------+

Hardware-Related AT Commands
============================

.. _overview-2:

Overview
--------

=============== =====================================================
**Commands**    **Description**
=============== =====================================================
AT+SYSIOSETCFG  Configures IO working mode.
AT+SYSIOGETCFG  Checks the working mode of IO pin.
AT+SYSGPIODIR   Configures the direction of GPIO.
AT+SYSGPIOWRITE Configures the GPIO output level.
AT+SYSGPIOREAD  Configures the GPIO input level.
AT+WAKEUPGPIO   Configures a GPIO to wake BFQ4004 up from sleep mode.
=============== =====================================================

.. _command-descriptions-1:

Command Descriptions
--------------------

AT+SYSIOSETCFG – Configures IO Working Mode
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-----------------+---------------------------------------------------+
| **Set Command** | AT+SYSIOSETCFG=<pin>,<mode>,<pull-up>             |
+-----------------+---------------------------------------------------+
| **Response**    | OK                                                |
+-----------------+---------------------------------------------------+
| **Parameters**  | -  <pin>: number of an IO pin                     |
|                 |                                                   |
|                 | -  <mode>: the working mode of the IO pin         |
|                 |                                                   |
|                 | -  <pull-up>                                      |
|                 |                                                   |
|                 |    -  : disable the pull-up                       |
|                 |                                                   |
|                 |    -  1: enable the pull-up of the IO pin         |
+-----------------+---------------------------------------------------+
| **Notes**       | Please refer to BFQ4004 Pin List for uses of      |
|                 | AT+SYSGPIO-related commands.                      |
+-----------------+---------------------------------------------------+
| **Examples**    | AT+SYSIOSETCFG=12,3,1 //Set GPIO12 to work as a   |
|                 | GPIO                                              |
+-----------------+---------------------------------------------------+

AT+SYSIOGETCFG – Get IO Working Mode
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-----------------+---------------------------------------------------+
| **Set Command** | AT+SYSIOGETCFG=<pin>                              |
+-----------------+---------------------------------------------------+
| **Response**    | +SYSIOGETCFG:<pin>,<mode>,<pull-up>               |
|                 |                                                   |
|                 | OK                                                |
+-----------------+---------------------------------------------------+
| **Parameters**  | -  <pin>: number of an IO pin                     |
|                 |                                                   |
|                 | -  <mode>: the working mode of the IO pin         |
|                 |                                                   |
|                 | -  <pull-up>                                      |
|                 |                                                   |
|                 |    -  : disable the pull-up                       |
|                 |                                                   |
|                 |    -  1: enable the pull-up of the IO pin         |
+-----------------+---------------------------------------------------+
| **Notes**       | Please refer to BFQ4004 Pin List for uses of      |
|                 | AT+SYSGPIO-related commands.                      |
+-----------------+---------------------------------------------------+

AT+SYSGPIODIR – Configures the Direction of GPIO
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-----------------+---------------------------------------------------+
| **Set Command** | AT+SYSGPIODIR=<pin>,<dir>                         |
+-----------------+---------------------------------------------------+
| **Response**    | -  | If the configuration is successful, the      |
|                 |      command will return:                         |
|                 |    | OK                                           |
|                 |                                                   |
|                 | -  | If the IO pin is not in GPIO mode, the       |
|                 |      command will return:                         |
|                 |    | NOT GPIO MODE!                               |
|                 |    | ERROR                                        |
+-----------------+---------------------------------------------------+
| **Parameters**  | -  <pin>: GPIO pin number                         |
|                 |                                                   |
|                 | -  <dir>:                                         |
|                 |                                                   |
|                 |    -  : sets the GPIO as an input                 |
|                 |                                                   |
|                 |    -  1: sets the GPIO as an output               |
+-----------------+---------------------------------------------------+
| **Notes**       | Please refer to BFQ4004 Pin List for uses of      |
|                 | AT+SYSGPIO-related commands.                      |
+-----------------+---------------------------------------------------+
| **Examples**    | AT+SYSIOSETCFG=12,3,1 //Set GPIO12 to work as a   |
|                 | GPIO                                              |
|                 |                                                   |
|                 | AT+SYSGPIODIR=12,0 //Set GPIO12 to work as an     |
|                 | input                                             |
+-----------------+---------------------------------------------------+

AT+SYSGPIOWRITE – Configures the Output Level of a GPIO
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-----------------+---------------------------------------------------+
| **Set Command** | AT+SYSGPIOWRITE=<pin>,<level>                     |
+-----------------+---------------------------------------------------+
| **Response**    | -  | If the configuration is successful, the      |
|                 |      command will return:                         |
|                 |    | OK                                           |
|                 |                                                   |
|                 | -  | If the IO pin is not in output mode, the     |
|                 |      command will return:                         |
|                 |    | NOT OUTPUT!                                  |
|                 |    | ERROR                                        |
+-----------------+---------------------------------------------------+
| **Parameters**  | -  <pin>: GPIO pin number                         |
|                 |                                                   |
|                 | -  <level>:                                       |
|                 |                                                   |
|                 |    -  : low level                                 |
|                 |                                                   |
|                 |    -  1: high level                               |
+-----------------+---------------------------------------------------+
| **Notes**       | Please refer to BFQ4004 Pin List for uses of      |
|                 | AT+SYSGPIO-related commands.                      |
+-----------------+---------------------------------------------------+
| **Examples**    | AT+SYSIOSETCFG=12,3,1 //Set GPIO12 to work as a   |
|                 | GPIO                                              |
|                 |                                                   |
|                 | AT+SYSGPIODIR=12,1 //Set GPIO12 to work as an     |
|                 | output                                            |
|                 |                                                   |
|                 | AT+SYSGPIOWRITE=12,1 //Set GPIO12 to output high  |
|                 | level                                             |
+-----------------+---------------------------------------------------+

AT+SYSGPIOREAD – Reads the GPIO Level
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-----------------+---------------------------------------------------+
| **Set Command** | AT+SYSGPIOREAD=<pin>                              |
+-----------------+---------------------------------------------------+
| **Response**    | -  | If the configuration is successful, the      |
|                 |      command will return:                         |
|                 |    | +SYSGPIOREAD:<pin>,<dir>,<level>             |
|                 |    | OK                                           |
|                 |                                                   |
|                 | -  | If the IO pin is not in GPIO mode, the       |
|                 |      command will return:                         |
|                 |    | NOT GPIO MODE!                               |
|                 |    | ERROR                                        |
+-----------------+---------------------------------------------------+
| **Parameters**  | -  <pin>: GPIO pin number                         |
|                 |                                                   |
|                 | -  <dir>:                                         |
|                 |                                                   |
|                 |    -  : the GPIO as an input                      |
|                 |                                                   |
|                 |    -  1: the GPIO as an output                    |
|                 |                                                   |
|                 | -  <level>:                                       |
|                 |                                                   |
|                 |    -  : low level                                 |
|                 |                                                   |
|                 |    -  1: high level                               |
+-----------------+---------------------------------------------------+
| **Notes**       | Please refer to BFQ4004 Pin List for uses of      |
|                 | AT+SYSGPIO-related commands.                      |
+-----------------+---------------------------------------------------+
| **Examples**    | AT+SYSIOSETCFG=12,3,1 //Set GPIO12 to work as a   |
|                 | GPIO                                              |
|                 |                                                   |
|                 | AT+SYSGPIODIR=12,0 //Set GPIO12 to work as an     |
|                 | input                                             |
|                 |                                                   |
|                 | AT+SYSGPIOREAD=12 //Read GPIO12 level             |
+-----------------+---------------------------------------------------+

AT+WAKEUPGPIO – Configures a GPIO to Wake BFQ4004 up from Sleep Mode
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-----------------+---------------------------------------------------+
| **Set Command** | AT+WAK                                            |
|                 | EUPGPIO=<enable>,<trigger_GPIO>,<trigger_level>[, |
|                 | <awake_GPIO>,<awake_level>]                       |
+-----------------+---------------------------------------------------+
| **Response**    | OK                                                |
+-----------------+---------------------------------------------------+
| **Parameters**  | -  <enable>:                                      |
|                 |                                                   |
|                 |    -  : BFQ4004 can NOT be woken up from sleep by |
|                 |       GPIO.                                       |
|                 |                                                   |
|                 |    -  1: BFQ4004 can be woken up from sleep by    |
|                 |       GPIO.                                       |
|                 |                                                   |
|                 | -  <trigger_GPIO>: sets the GPIO to wake BFQ4004  |
|                 |    up; range of value:[0, 15].                    |
|                 |                                                   |
|                 | -  <trigger_level>:                               |
|                 |                                                   |
|                 |    -  : the GPIO wakes up BFQ4004 with low level. |
|                 |                                                   |
|                 |    -  1: the GPIO wakes up BFQ4004 with high      |
|                 |       level.                                      |
|                 |                                                   |
|                 | -  [<awake_GPIO>]: optional parameter to set a    |
|                 |    GPIO as a flag to indicate that BFQ4004 was    |
|                 |    awoken from sleep; range of value: [0, 15].    |
|                 |                                                   |
|                 | -  [<awake_level>]: optional parameter;           |
|                 |                                                   |
|                 |    -  : the awake_GPIO is set to low level after  |
|                 |       the wakeup process.                         |
|                 |                                                   |
|                 |    -  1: the awake_GPIO is set to high level      |
|                 |       after the wakeup process.                   |
+-----------------+---------------------------------------------------+
| **Notes**       | -  Since the system needs some time to wake up    |
|                 |    from sleep, it is suggested that wait at least |
|                 |    5ms before sending next AT command.            |
|                 |                                                   |
|                 | -  The values of <trigger_GPIO> and <awake_GPIO>  |
|                 |    should not be the same.                        |
|                 |                                                   |
|                 | -  After being woken up by <trigger_GPIO> from    |
|                 |    sleep, when BFQ4004 attempts to sleep again,   |
|                 |    it will check the status of the                |
|                 |    <trigger_GPIO>.                                |
|                 |                                                   |
|                 | -  if <trigger_GPIO> is still in the wakeup       |
|                 |    status, BFQ4004 will enter Associated mode     |
|                 |    instead.                                       |
|                 |                                                   |
|                 | -  If <trigger_GPIO> is NOT in the wakeup status, |
|                 |    BFQ4004 will enter sleep mode.                 |
+-----------------+---------------------------------------------------+
| **Examples**    | -  Set BFQ4004 to be woken from sleep, when GPIO0 |
|                 |    is at low level:                               |
|                 |                                                   |
|                 |    AT+WAKEUPGPIO=1,,                              |
|                 |                                                   |
|                 | -  Set BFQ4004 to be woken from sleep, when GPIO0 |
|                 |    is at high level, and after wake-up, GPIO13    |
|                 |    should be set to high level.                   |
|                 |                                                   |
|                 |    AT+WAKEUPGPIO=1,,1,13,1                        |
|                 |                                                   |
|                 | -  Disable BFQ4004 from being woken up from sleep |
|                 |    by a GPIO.                                     |
|                 |                                                   |
|                 |    AT+WAKEUPGPIO=                                 |
+-----------------+---------------------------------------------------+

Wi-Fi-Related AT Commands
=========================

.. _overview-3:

Overview
--------

+------------------+--------------------------------------------------+
| **Commands**     | **Description**                                  |
+==================+==================================================+
| AT+CWMODE_CUR    | Sets the Wi-Fi mode                              |
|                  | (Station/SoftAP/Station+SoftAP); configuration   |
|                  | not saved in flash.                              |
+------------------+--------------------------------------------------+
| AT+CWMODE_DEF    | Sets the default Wi-Fi mode                      |
|                  | (Station/SoftAP/Station+SoftAP); configuration   |
|                  | saved in flash.                                  |
+------------------+--------------------------------------------------+
| AT+CWJAP_CUR     | Connects to an AP; configuration not saved in    |
|                  | flash.                                           |
+------------------+--------------------------------------------------+
| AT+CWJAP_DEF     | Connects to an AP; configuration saved in flash. |
+------------------+--------------------------------------------------+
| AT+CWLAPOPT      | Sets the configuration of command AT+CWLAP.      |
+------------------+--------------------------------------------------+
| AT+CWLAP         | Lists available APs.                             |
+------------------+--------------------------------------------------+
| AT+CWQAP         | Disconnects from an AP.                          |
+------------------+--------------------------------------------------+
| AT+CWSAP_CUR     | Sets the current configuration of BFQ4004        |
|                  | SoftAP; configuration not saved in flash.        |
+------------------+--------------------------------------------------+
| AT+CWSAP_DEF     | Sets the configuration of BFQ4004 SoftAP;        |
|                  | configuration saved in flash.                    |
+------------------+--------------------------------------------------+
| AT+CWLIF         | Gets the IP addresses of the Stations the        |
|                  | BFQ4004 SoftAP is connected with.                |
+------------------+--------------------------------------------------+
| AT+CWDHCP_CUR    | Enables/Disables DHCP; configuration not saved   |
|                  | in the flash.                                    |
+------------------+--------------------------------------------------+
| AT+CWDHCP_DEF    | Enable/Disable DHCP; configuration saved in      |
|                  | flash.                                           |
+------------------+--------------------------------------------------+
| AT+CWDHCPS_CUR   | Sets the IP address range the SoftAP DHCP server |
|                  | can allocate; configuration not saved in flash.  |
+------------------+--------------------------------------------------+
| AT+CWDHCPS_DEF   | Sets the IP address range the SoftAP DHCP server |
|                  | can allocate; configuration saved in flash.      |
+------------------+--------------------------------------------------+
| AT+CWAUTOCONN    | Connects to an AP automatically on power-up or   |
|                  | not.                                             |
+------------------+--------------------------------------------------+
| AT+CIPSTA_CUR    | Sets the IP address of BFQ4004 Station;          |
|                  | configuration not saved in flash.                |
+------------------+--------------------------------------------------+
| AT+CIPSTA_DEF    | Sets the IP address of BFQ4004 Station;          |
|                  | configuration saved in flash.                    |
+------------------+--------------------------------------------------+
| AT+CIPAP_CUR     | Sets the IP address of BFQ4004 SoftAP;           |
|                  | configuration not saved in flash.                |
+------------------+--------------------------------------------------+
| AT+CIPAP_DEF     | Sets the IP address of BFQ4004 SoftAP;           |
|                  | configuration saved in flash.                    |
+------------------+--------------------------------------------------+
| AT+WPS           | Enables the WPS function.                        |
+------------------+--------------------------------------------------+
| AT+CWHOSTNAME    | Configures the name of BFQ4004 Station.          |
+------------------+--------------------------------------------------+
| AT+CWCOUNTRY_CUR | Sets current WiFi country code, not saved in     |
|                  | flash                                            |
+------------------+--------------------------------------------------+
| AT+CWCOUNTRY_DEF | Sets default WiFi country code, saved in flash   |
+------------------+--------------------------------------------------+

.. _command-descriptions-2:

Command Descriptions
--------------------

AT+CWMODE_CUR – Sets Current WiFi Mode Configuration, Not Saved in Flash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+----------------+----------------+----------------+
| **Command**    | Test:          | Query:         | Set:           |
|                |                |                |                |
|                | A              | AT+CWMODE_CUR? | |              |
|                | T+CWMODE_CUR=? |                | AT+CWMODE_CUR= |
|                |                | Function:      | | <mode>       |
|                |                | check current  |                |
|                |                | WiFi mode      | Function: set  |
|                |                |                | current WiFi   |
|                |                |                | mode           |
+----------------+----------------+----------------+----------------+
| **Response**   | +CWMODE_CUR:   | +CWMODE_CUR:   | OK             |
|                |                |                |                |
|                | <mode>         | <mode>         |                |
|                |                |                |                |
|                | OK             | OK             |                |
+----------------+----------------+----------------+----------------+
| **Parameters** | -  <mode>:                                       |
|                |                                                  |
|                |    -  1:                                         |
|                |       Station                                    |
|                |       mode                                       |
|                |                                                  |
|                |    -  2:                                         |
|                |       SoftAP                                     |
|                |       mode                                       |
|                |                                                  |
|                |    -  3:                                         |
|                |                                                  |
|                | Station+SoftAP                                   |
|                |       mode                                       |
+----------------+----------------+----------------+----------------+
| **Notes**      | The                                              |
|                | configuration                                    |
|                | changes will                                     |
|                | NOT be saved                                     |
|                | in flash.                                        |
+----------------+----------------+----------------+----------------+
| **Examples**   | A                                                |
|                | T+CWMODE_CUR=1                                   |
+----------------+----------------+----------------+----------------+

AT+CWMODE_DEF- Sets Default WiFi Mode Configuration, Saved in Flash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+----------------+----------------+----------------+
| **Command**    | Test:          | Query:         | Set:           |
|                |                |                |                |
|                | A              | AT+CWMODE_DEF? | |              |
|                | T+CWMODE_DEF=? |                | AT+CWMODE_DEF= |
|                |                | Function:      | | <mode>       |
|                |                | check current  |                |
|                |                | WiFi mode      | Function: set  |
|                |                |                | current WiFi   |
|                |                |                | mode           |
+----------------+----------------+----------------+----------------+
| **Response**   | +CWMODE_DEF:   | +CWMODE_DEF:   | OK             |
|                |                |                |                |
|                | <mode>         | <mode>         |                |
|                |                |                |                |
|                | OK             | OK             |                |
+----------------+----------------+----------------+----------------+
| **Parameters** | -  <mode>:                                       |
|                |                                                  |
|                |    -  1:                                         |
|                |       Station                                    |
|                |       mode                                       |
|                |                                                  |
|                |    -  2:                                         |
|                |       SoftAP                                     |
|                |       mode                                       |
|                |                                                  |
|                |    -  3:                                         |
|                |                                                  |
|                | Station+SoftAP                                   |
|                |       mode                                       |
+----------------+----------------+----------------+----------------+
| **Notes**      | The                                              |
|                | configuration                                    |
|                | changes will                                     |
|                | be saved in                                      |
|                | flash.                                           |
+----------------+----------------+----------------+----------------+
| **Examples**   | A                                                |
|                | T+CWMODE_DEF=1                                   |
+----------------+----------------+----------------+----------------+

AT+CWJAP_CUR – Connects to AP, Configuration Not Saved in Flash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-------------------------+
| **Command**    | | Query:                | | Set:                  |
|                | | AT+CWJAP_CUR?         | | AT+                   |
|                |                         | CWJAP_CUR=<ssid>,<pwd>, |
|                | Function: check         |                         |
|                | parameters of the AP    | [<bssid>,<pci_en>]      |
|                | BFQ4004 Station is      |                         |
|                | connected to.           | Function: specify       |
|                |                         | parameters of the AP    |
|                |                         | BFQ4004 wants to        |
|                |                         | connect to.             |
+----------------+-------------------------+-------------------------+
| **Response**   | +CW                     | OK                      |
|                | JAP_CUR:<ssid>,<bssid>, |                         |
|                |                         | or                      |
|                | <channel>,<rssi>        |                         |
|                |                         | +CWJAP_CUR:<error code> |
|                | OK                      |                         |
|                |                         | FAIL                    |
+----------------+-------------------------+-------------------------+
| **Parameters** | <ssid>: a string        | -  <ssid>: target AP    |
|                | parameter showing the   |    SSID, max length: 32 |
|                | SSID of the AP BFQ4004  |    bytes                |
|                | Station is connected    |                         |
|                | to.                     | -  <pwd>: target AP     |
|                |                         |    password, max        |
|                |                         |    length: 64-byte      |
|                |                         |    ASCII                |
|                |                         |                         |
|                |                         | -  [<bssid>]: optional, |
|                |                         |    target AP’s MAC      |
|                |                         |    address, used when   |
|                |                         |    multiple APs have    |
|                |                         |    the same SSID        |
|                |                         |                         |
|                |                         | -  [<pci_en>]:          |
|                |                         |    optional, disable    |
|                |                         |    the connection to    |
|                |                         |    WEP or OPEN AP, and  |
|                |                         |    can be used for PCI  |
|                |                         |    authentication.      |
|                |                         |                         |
|                |                         | -  <error code>: for    |
|                |                         |    reference only       |
|                |                         |                         |
|                |                         |    -  1: connection     |
|                |                         |       timeout           |
|                |                         |                         |
|                |                         |    -  2: wrong password |
|                |                         |                         |
|                |                         |    -  3: cannot find    |
|                |                         |       the target AP     |
|                |                         |                         |
|                |                         |    -  4: connection     |
|                |                         |       failed            |
|                |                         |                         |
|                |                         | This command requires   |
|                |                         | Station mode to work.   |
|                |                         | Escape character syntax |
|                |                         | is needed if SSID or    |
|                |                         | password contains       |
|                |                         | special characters,     |
|                |                         | such as , or “ or \\    |
+----------------+-------------------------+-------------------------+
| **Notes**      | The configuration                                 |
|                | changes will NOT be                               |
|                | saved in flash                                    |
+----------------+-------------------------+-------------------------+
| **Examples**   | AT+CWJA                                           |
|                | P_CUR="abc","123456789"                           |
|                |                                                   |
|                | For example, if the                               |
|                | target AP’s SSID is                               |
|                | "ab\,c" and the                                   |
|                | password is                                       |
|                |                                                   |
|                | "123456789"\", the                                |
|                | command is as follows:                            |
|                |                                                   |
|                | AT+CWJAP_CUR="a                                   |
|                | b\\\,c","123456789\"\\"                           |
|                |                                                   |
|                | If multiple APs have                              |
|                | the same SSID as "abc",                           |
|                | the target AP can be                              |
|                | found by BSSID:                                   |
|                |                                                   |
|                | AT+C                                              |
|                | WJAP_CUR="abc","1234567                           |
|                | 89","ca:d7:19:d8:a6:44"                           |
+----------------+-------------------------+-------------------------+

AT+CWJAP_DEF – Connects to AP, Configuration Saved in Flash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-------------------------+
| **Command**    | | Query:                | | Set:                  |
|                | | AT+CWJAP_DEF?         | | AT+                   |
|                |                         | CWJAP_DEF=<ssid>,<pwd>, |
|                | Function: check         |                         |
|                | parameters of the AP    | [<bssid>,<pci_en>]      |
|                | BFQ4004 Station is      |                         |
|                | connected to.           | Function: specify       |
|                |                         | parameters of the AP    |
|                |                         | BFQ4004 wants to        |
|                |                         | connect to.             |
+----------------+-------------------------+-------------------------+
| **Response**   | +CW                     | OK                      |
|                | JAP_DEF:<ssid>,<bssid>, |                         |
|                |                         | or                      |
|                | <channel>,<rssi>        |                         |
|                |                         | +CWJAP_DEF:<error code> |
|                | OK                      |                         |
|                |                         | FAIL                    |
+----------------+-------------------------+-------------------------+
| **Parameters** | <ssid>: a string        | -  <ssid>: target AP    |
|                | parameter showing the   |    SSID, max length: 32 |
|                | SSID of the AP BFQ4004  |    bytes                |
|                | Station is connected    |                         |
|                | to.                     | -  <pwd>: target AP     |
|                |                         |    password, max        |
|                |                         |    length: 64-byte      |
|                |                         |    ASCII                |
|                |                         |                         |
|                |                         | -  [<bssid>]: optional, |
|                |                         |    target AP’s MAC      |
|                |                         |    address, used when   |
|                |                         |    multiple APs have    |
|                |                         |    the same SSID        |
|                |                         |                         |
|                |                         | -  [<pci_en>]:          |
|                |                         |    optional, disable    |
|                |                         |    the connection to    |
|                |                         |    WEP or OPEN AP, and  |
|                |                         |    can be used for PCI  |
|                |                         |    authentication.      |
|                |                         |                         |
|                |                         | -  <error code>: for    |
|                |                         |    reference only       |
|                |                         |                         |
|                |                         |    -  1: connection     |
|                |                         |       timeout           |
|                |                         |                         |
|                |                         |    -  2: wrong password |
|                |                         |                         |
|                |                         |    -  3: cannot find    |
|                |                         |       the target AP     |
|                |                         |                         |
|                |                         |    -  4: connection     |
|                |                         |       failed            |
|                |                         |                         |
|                |                         | This command requires   |
|                |                         | Station mode to work.   |
|                |                         | Escape character syntax |
|                |                         | is needed if SSID or    |
|                |                         | password contains       |
|                |                         | special characters,     |
|                |                         | such as , or “ or \\    |
+----------------+-------------------------+-------------------------+
| **Notes**      | The configuration                                 |
|                | changes will be saved                             |
|                | in the system                                     |
|                | parameters area in the                            |
|                | flash                                             |
+----------------+-------------------------+-------------------------+
| **Examples**   | AT+CWJA                                           |
|                | P_DEF="abc","123456789"                           |
|                |                                                   |
|                | For example, if the                               |
|                | target AP’s SSID is                               |
|                | "ab\,c" and the                                   |
|                | password is                                       |
|                |                                                   |
|                | "123456789"\", the                                |
|                | command is as follows:                            |
|                |                                                   |
|                | AT+CWJAP_DEF="a                                   |
|                | b\\\,c","123456789\"\\"                           |
|                |                                                   |
|                | If multiple APs have                              |
|                | the same SSID as "abc",                           |
|                | the target AP can be                              |
|                | found by BSSID:                                   |
|                |                                                   |
|                | AT+C                                              |
|                | WJAP_DEF="abc","1234567                           |
|                | 89","ca:d7:19:d8:a6:44"                           |
+----------------+-------------------------+-------------------------+

AT+CWLAPOPT – Sets the Configuration for the Command AT+CWLAP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-----------------+---------------------------------------------------+
| **Set Command** | AT+CWLAPOPT=<sort_enable>,<mask>                  |
+-----------------+---------------------------------------------------+
| **Response**    | OK                                                |
|                 |                                                   |
|                 | or                                                |
|                 |                                                   |
|                 | ERROR                                             |
+-----------------+---------------------------------------------------+
| **Parameters**  | -  <sort_enable>: determines whether the result   |
|                 |    of the command AT+CWLAP will be listed in      |
|                 |    order according to RSSI:                       |
|                 |                                                   |
|                 |    -  : the result is not ordered according to    |
|                 |       RSSI.                                       |
|                 |                                                   |
|                 |    -  1: the result is ordered according to RSSI. |
|                 |                                                   |
|                 | -  <mask>: determines the parameters shown in the |
|                 |    result of AT+CWLAP; means not showing the      |
|                 |    parameter corresponding to the bit, and 1      |
|                 |    means showing it.                              |
|                 |                                                   |
|                 |    -  bit : determines whether <ecn> will be      |
|                 |       shown in the result of AT+CWLAP.            |
|                 |                                                   |
|                 |    -  bit 1: determines whether <ssid> will be    |
|                 |       shown in the result of AT+CWLAP.            |
|                 |                                                   |
|                 |    -  bit 2: determines whether <rssi> will be    |
|                 |       shown in the result of AT+CWLAP.            |
|                 |                                                   |
|                 |    -  bit 3: determines whether <mac> will be     |
|                 |       shown in the result of AT+CWLAP.            |
|                 |                                                   |
|                 |    -  bit 4: determines whether <ch> will be      |
|                 |       shown in the result of AT+CWLAP.            |
|                 |                                                   |
|                 |    -  bit 5: determines whether <freq offset>     |
|                 |       will be shown in the result of AT+CWLAP.    |
|                 |                                                   |
|                 |    -  bit 6: determines whether <freq             |
|                 |       calibration> will be shown in the result of |
|                 |       AT+CWLAP.                                   |
|                 |                                                   |
|                 |    -  bit 7: determines whether <pairwise_cipher> |
|                 |       will be shown in the result of AT+CWLAP.    |
|                 |                                                   |
|                 |    -  bit 8: determines whether <group_cipher>    |
|                 |       will be shown in the result of AT+CWLAP.    |
|                 |                                                   |
|                 |    -  bit 9: determines whether <bgn> will be     |
|                 |       shown in the result of AT+CWLAP.            |
|                 |                                                   |
|                 |    -  bit 1: determines whether <wps> will be     |
|                 |       shown in the result of AT+CWLAP.            |
+-----------------+---------------------------------------------------+
| **Examples**    |    AT+CWLAPOPT=1,247                              |
|                 |                                                   |
|                 |    The first parameter is 1, meaning that the     |
|                 |    result of the command AT+CWLAP will be ordered |
|                 |    according to RSSI;                             |
|                 |                                                   |
|                 |    The second parameter is 247, namely x7FF,      |
|                 |    meaning that the corresponding bits of <mask>  |
|                 |    are all set to 1 and all parameters will be    |
|                 |    shown in the result of AT+CWLAP.               |
+-----------------+---------------------------------------------------+

AT+CWLAP – Lists Available APs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-------------------------+
| **Command**    | Set:                    | Execute:                |
|                |                         |                         |
|                | AT+CWLAP[=<ssid>,<mac>, | AT+CWLAP                |
|                |                         |                         |
|                | <channel>,<scan_type>,  | Function: to list all   |
|                |                         | available APs.          |
|                | <scan_time_min>,        |                         |
|                |                         |                         |
|                | <scan_time_max>]        |                         |
|                |                         |                         |
|                | Function: to query the  |                         |
|                | APs with specific SSID  |                         |
|                | and MAC on a specific   |                         |
|                | channel.                |                         |
+----------------+-------------------------+-------------------------+
| **Response**   | +CWL                    | +CWL                    |
|                | AP:<ecn>,<ssid>,<rssi>, | AP:<ecn>,<ssid>,<rssi>, |
|                |                         |                         |
|                | <mac>,<                 | <mac>,<                 |
|                | channel>,<freq_offset>, | channel>,<freq_offset>, |
|                |                         | <freq_c                 |
|                | <freq_c                 | ali>,<pairwise_cipher>, |
|                | ali>,<pairwise_cipher>, |                         |
|                |                         | <gr                     |
|                | <gr                     | oup_cipher>,<bgn>,<wps> |
|                | oup_cipher>,<bgn>,<wps> |                         |
|                |                         | OK                      |
|                | OK                      |                         |
+----------------+-------------------------+-------------------------+
| **Parameters** | -  [<scan_type>]:                                 |
|                |    optional parameter                             |
|                |                                                   |
|                |    -  : active scan                               |
|                |                                                   |
|                |    -  1: passive scan                             |
|                |                                                   |
|                | -  [<scan_time_min>] :                            |
|                |    optional parameter,                            |
|                |    unit: ms, range:                               |
|                |    [,15]                                          |
|                |                                                   |
|                |    -  For active scan                             |
|                |       mode,                                       |
|                |       <scan_time_min>                             |
|                |       is the minimum                              |
|                |       scan time for                               |
|                |       each channel,                               |
|                |       default is .                                |
|                |                                                   |
|                |    -  For passive scan                            |
|                |       mode,                                       |
|                |       <scan_time_min>                             |
|                |       is meaningless                              |
|                |       and can be                                  |
|                |       omitted.                                    |
|                |                                                   |
|                | -  [<scan_time_max>] :                            |
|                |    optional parameter,                            |
|                |    unit: ms, range:                               |
|                |    [,15]                                          |
|                |                                                   |
|                |    -  For active scan                             |
|                |       mode,                                       |
|                |       <scan_time_max>                             |
|                |       is the maximum                              |
|                |       scan time for                               |
|                |       each channel. If                            |
|                |       it is set to be ,                           |
|                |       the default value                           |
|                |       of 12 ms will be                            |
|                |       used.                                       |
|                |                                                   |
|                |    -  For passive scan                            |
|                |       mode,                                       |
|                |       <scan_time_max>                             |
|                |       is the scan time                            |
|                |       for each channel,                           |
|                |       the default is 36                           |
|                |       ms.                                         |
|                |                                                   |
|                | -  <ecn>: encryption                              |
|                |    method.                                        |
|                |                                                   |
|                |    -  : OPEN                                      |
|                |                                                   |
|                |    -  1: WEP                                      |
|                |                                                   |
|                |    -  2: WPA_PSK                                  |
|                |                                                   |
|                |    -  3: WPA2_PSK                                 |
|                |                                                   |
|                |    -  4: WPA_WPA2_PSK                             |
|                |                                                   |
|                |    -  5:                                          |
|                |                                                   |
|                |         WPA2_Enterprise                           |
|                |          (AT can NOT                              |
|                |          connect to                               |
|                |                                                   |
|                |         WPA2_Enterprise                           |
|                |          AP for now.)                             |
|                |                                                   |
|                | -  <ssid>: string                                 |
|                |    parameter indicating                           |
|                |    the SSID of the AP.                            |
|                |                                                   |
|                | -  <rssi>: received                               |
|                |    signal strength from                           |
|                |    the AP.                                        |
|                |                                                   |
|                | -  <mac>: string                                  |
|                |    parameter indicating                           |
|                |    the MAC address of                             |
|                |    the AP.                                        |
|                |                                                   |
|                | -  <channel>: WiFi                                |
|                |    channel number.                                |
|                |                                                   |
|                | -  <freq_offset>:                                 |
|                |    frequency offset of                            |
|                |    the AP; unit: KHz.                             |
|                |    The value of ppm is                            |
|                |    <freq_offset>/2.4.                             |
|                |                                                   |
|                | -  <freq_cali>:                                   |
|                |    calibration for                                |
|                |    frequency offset.                              |
|                |                                                   |
|                | -  <pairwise_cipher>:                             |
|                |                                                   |
|                |    -  ：CIPHER_NONE     |                         |
|                |                                                   |
|                |    -  1：CIPHER_WEP40   |                         |
|                |                                                   |
|                |    -  2：CIPHER_WEP104  |                         |
|                |                                                   |
|                |    -  3：CIPHER_TKIP    |                         |
|                |                                                   |
|                |    -  4：CIPHER_CCMP    |                         |
|                |                                                   |
|                |                                                   |
|                |  -  5：CIPHER_TKIP_CCMP |                         |
|                |                                                   |
|                |    -  6：CIPHER_UNKNOWN |                         |
|                |                                                   |
|                | -  <group_cipher>: the                            |
|                |    definitions of                                 |
|                |    cipher types are the                           |
|                |    same as                                        |
|                |    <pairwise_cipher>                              |
|                |                                                   |
|                | -  <bgn>:                                         |
|                |                                                   |
|                |    -  Bit is for                                  |
|                |       802.11b mode;                               |
|                |       bit1 is for                                 |
|                |       802.11g mode;                               |
|                |       bit2 is for                                 |
|                |       802.11n mode;                               |
|                |                                                   |
|                |    -  if the value of                             |
|                |       the bit is 1, the                           |
|                |       corresponding                               |
|                |       802.11 mode is                              |
|                |       enabled; if the                             |
|                |       bit value is 0,                             |
|                |       the mode is                                 |
|                |       disabled.                                   |
|                |                                                   |
|                | -  <wps>：:WPS is       |                         |
|                |    disabled; 1:WPS is                             |
|                |    enabled                                        |
+----------------+-------------------------+-------------------------+
| **Examples**   | AT+CWLAP="Wi-Fi                                   |
|                | ","ca:d7:19:d8:a6:44",6                           |
|                |                                                   |
|                | or search for APs with                            |
|                | a designated SSID:                                |
|                |                                                   |
|                | AT+CWLAP="Wi-Fi"                                  |
|                |                                                   |
|                | or enable passive scan:                           |
|                |                                                   |
|                | AT+CWLAP=,,,1,,                                   |
+----------------+-------------------------+-------------------------+

AT+CWQAP – Disconnects from the AP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

=================== ========
**Execute Command** AT+CWQAP
**Response**        OK
**Parameters**      \-
=================== ========

AT+CWSAP_CUR – Configures the BFQ4004 SoftAP, Configuration Not Saved to Flash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-------------------------+
| **Command**    | Query:                  | Set:                    |
|                |                         |                         |
|                | AT+CWSAP_CUR?           | AT+                     |
|                |                         | CWSAP_CUR=<ssid>,<pwd>, |
|                | Function: to obtain the |                         |
|                | configuration           | <chl>,<ecn>[,<max       |
|                | parameters of the       | conn>]                  |
|                | BFQ4004 SoftAP.         |                         |
|                |                         | [,<ssid hidden>]        |
|                |                         |                         |
|                |                         | Function: to configure  |
|                |                         | the BFQ4004             |
|                |                         | SoftAP\ **.**           |
+----------------+-------------------------+-------------------------+
| **Response**   | +                       | OK                      |
|                | CWSAP_CUR:<ssid>,<pwd>, |                         |
|                |                         | or                      |
|                | <                       |                         |
|                | chl>,<ecn>,[<max_conn>, | ERROR                   |
|                |                         |                         |
|                | <ssid_hidden>]          |                         |
+----------------+-------------------------+-------------------------+
| **Parameters** | -  <ssid>: string                                 |
|                |    parameter, the SSID                            |
|                |    of the AP.                                     |
|                |                                                   |
|                | -  <pwd>: string                                  |
|                |    parameter, length of                           |
|                |    password: 8 ~ 64                               |
|                |    bytes ASCII.                                   |
|                |                                                   |
|                | -  <chl>: channel ID.                             |
|                |                                                   |
|                | -  <ecn>: encryption                              |
|                |    method                                         |
|                |                                                   |
|                |    -  : OPEN                                      |
|                |                                                   |
|                |    -  1: WEP                                      |
|                |                                                   |
|                |    -  2: WPA_PSK                                  |
|                |                                                   |
|                |    -  3: WPA2_PSK                                 |
|                |                                                   |
|                |    -  4: WPA_WPA2_PSK                             |
|                |                                                   |
|                | -  [<max_conn>]                                   |
|                |    (optional): maximum                            |
|                |    number of Stations                             |
|                |    to which BFQ4004                               |
|                |    SoftAP can be                                  |
|                |    connected to, range                            |
|                |    of [1, 8].                                     |
|                |                                                   |
|                | -  [<ssid_hidden>]                                |
|                |    (optional):                                    |
|                |                                                   |
|                |    -  : SSID is                                   |
|                |       broadcasted. (the                           |
|                |       default setting)                            |
|                |                                                   |
|                |    -  1: SSID is not                              |
|                |       broadcasted.                                |
+----------------+-------------------------+-------------------------+
| **Notes**      | -  The configuration                              |
|                |    will NOT be saved to                           |
|                |    the flash.                                     |
|                |                                                   |
|                | -  This command is                                |
|                |    available only when                            |
|                |    BFQ4004 is in softAP                           |
|                |    mode. See                                      |
|                |    AT+CWDHCP_CUR.                                 |
+----------------+-------------------------+-------------------------+
| **Examples**   | AT+CWSAP_CUR="BFQ                                 |
|                | 4004AP","123456789",5,3                           |
+----------------+-------------------------+-------------------------+

AT+CWSAP_DEF - Configures the BFQ4004 SoftAP, Configuration Saved to Flash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-------------------------+
| **Command**    | Query:                  | Set:                    |
|                |                         |                         |
|                | AT+CWSAP_DEF?           | AT+                     |
|                |                         | CWSAP_DEF=<ssid>,<pwd>, |
|                | Function: to obtain the |                         |
|                | configuration           | <chl>,<ecn>[,<max       |
|                | parameters of the       | conn>]                  |
|                | BFQ4004 SoftAP.         |                         |
|                |                         | [,<ssid hidden>]        |
|                |                         |                         |
|                |                         | Function: to configure  |
|                |                         | the BFQ4004             |
|                |                         | SoftAP\ **.**           |
+----------------+-------------------------+-------------------------+
| **Response**   | +                       | OK                      |
|                | CWSAP_DEF:<ssid>,<pwd>, |                         |
|                |                         | or                      |
|                | <                       |                         |
|                | chl>,<ecn>,[<max_conn>, | ERROR                   |
|                |                         |                         |
|                | <ssid_hidden>]          |                         |
+----------------+-------------------------+-------------------------+
| **Parameters** | -  <ssid>: string                                 |
|                |    parameter, the SSID                            |
|                |    of the AP.                                     |
|                |                                                   |
|                | -  <pwd>: string                                  |
|                |    parameter, length of                           |
|                |    password: 8 ~ 64                               |
|                |    bytes ASCII.                                   |
|                |                                                   |
|                | -  <chl>: channel ID.                             |
|                |                                                   |
|                | -  <ecn>: encryption                              |
|                |    method                                         |
|                |                                                   |
|                |    -  : OPEN                                      |
|                |                                                   |
|                |    -  1: WEP                                      |
|                |                                                   |
|                |    -  2: WPA_PSK                                  |
|                |                                                   |
|                |    -  3: WPA2_PSK                                 |
|                |                                                   |
|                |    -  4: WPA_WPA2_PSK                             |
|                |                                                   |
|                | -  [<max_conn>]                                   |
|                |    (optional): maximum                            |
|                |    number of Stations                             |
|                |    to which BFQ4004                               |
|                |    SoftAP can be                                  |
|                |    connected to, range                            |
|                |    of [1, 8].                                     |
|                |                                                   |
|                | -  [<ssid_hidden>]                                |
|                |    (optional):                                    |
|                |                                                   |
|                |    -  : SSID is                                   |
|                |       broadcasted. (the                           |
|                |       default setting)                            |
|                |                                                   |
|                |    -  1: SSID is not                              |
|                |       broadcasted.                                |
+----------------+-------------------------+-------------------------+
| **Notes**      | -  The configuration                              |
|                |    will be saved to the                           |
|                |    flash.                                         |
|                |                                                   |
|                | -  This command is                                |
|                |    available only when                            |
|                |    BFQ4004 is in softAP                           |
|                |    mode. See                                      |
|                |    AT+CWDHCP_DEF.                                 |
+----------------+-------------------------+-------------------------+
| **Examples**   | AT+CWSAP_DEF="BFQ                                 |
|                | 4004AP","123456789",5,3                           |
+----------------+-------------------------+-------------------------+

AT+CWLIF – Gets the IP Addresses of the Stations the BFQ4004 SoftAP Is Connected With
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+---------------------+-----------------------------------------------+
| **Execute Command** | AT+CWLIF                                      |
+---------------------+-----------------------------------------------+
| **Response**        | <ip_addr>,<mac>                               |
|                     |                                               |
|                     | OK                                            |
+---------------------+-----------------------------------------------+
| **Parameters**      | -  <ip_addr>: IP addresses of Stations to     |
|                     |    which BFQ4004 SoftAP is connected.         |
|                     |                                               |
|                     | -  <mac>: MAC address of Stations to which    |
|                     |    BFQ4004 SoftAP is connected.               |
+---------------------+-----------------------------------------------+
| **Notes**           | This command cannot get a static IP. It only  |
|                     | works when both DHCPs of the BFQ4004 SoftAP,  |
|                     | and of the Station to which BFQ4004 SoftAP is |
|                     | connected, are enabled.                       |
+---------------------+-----------------------------------------------+

AT+CWDHCP_CUR - Enables/Disables DHCP, Configuration Not Saved to Flash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-------------------------+
| **Command**    | Query:                  | Set:                    |
|                |                         |                         |
|                | AT+CWDHCP_CUR?          | AT                      |
|                |                         | +CWDHCP_CUR=<mode>,<en> |
|                | Function: to obtain the |                         |
|                | status of DHCP.         | Function: to            |
|                |                         | configure\ **.**\ DHCP. |
+----------------+-------------------------+-------------------------+
| **Response**   | +CWSAP_CUR:             | OK                      |
|                |                         |                         |
|                | <station_dhcp_status>,  |                         |
|                |                         |                         |
|                | <softap_dhcp_status>    |                         |
+----------------+-------------------------+-------------------------+
| **Parameters** | \-                      | -  <mode>:              |
|                |  <station_dhcp_status>: |                         |
|                |                         |    -  : Sets BFQ4004    |
|                |    -  : Station DHCP is |       SoftAP            |
|                |       disabled.         |                         |
|                |                         |    -  1: Sets BFQ4004   |
|                |    -  1: Station DHCP   |       Station           |
|                |       is enabled.       |                         |
|                |                         |    -  2: Sets both      |
|                | -                       |       SoftAP and        |
|                |   <softap_dhcp_status>: |       Station           |
|                |                         |                         |
|                |    -  : SoftAP DHCP is  | -  <en>:                |
|                |       disabled.         |                         |
|                |                         |    -  : Disables DHCP   |
|                |    -  1: SoftAP DHCP is |                         |
|                |          enabled.       |    -  1: Enables DHCP   |
+----------------+-------------------------+-------------------------+
| **Notes**      | -  The configuration                              |
|                |    changes will not be                            |
|                |    saved in flash.                                |
|                |                                                   |
|                | -  The Set Command                                |
|                |    interacts with                                 |
|                |    static-IP-related AT                           |
|                |    commands                                       |
|                |    (AT+CIPSTA-related                             |
|                |    and AT+CIPA-related                            |
|                |    commands):                                     |
|                |                                                   |
|                |    -  If DHCP is                                  |
|                |       enabled, static                             |
|                |       IP will be                                  |
|                |       disabled;                                   |
|                |                                                   |
|                |    -  If static IP is                             |
|                |       enabled, DHCP                               |
|                |       will be disabled;                           |
|                |                                                   |
|                |    -  Whether it is                               |
|                |       DHCP or static IP                           |
|                |       that is enabled                             |
|                |       depends on the                              |
|                |       last                                        |
|                |       configuration.                              |
+----------------+-------------------------+-------------------------+
| **Examples**   | AT+CWDHCP_CUR=,1                                  |
+----------------+-------------------------+-------------------------+

AT+CWDHCP_DEF - Enables/Disables DHCP, Configuration Saved to Flash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-------------------------+
| **Command**    | Query:                  | Set:                    |
|                |                         |                         |
|                | AT+CWDHCP_DEF?          | AT                      |
|                |                         | +CWDHCP_DEF=<mode>,<en> |
|                | Function: to obtain the |                         |
|                | status of DHCP.         | Function: to            |
|                |                         | configure\ **.**\ DHCP. |
+----------------+-------------------------+-------------------------+
| **Response**   | +CWSAP_DEF:             | OK                      |
|                |                         |                         |
|                | <station_dhcp_status>,  |                         |
|                |                         |                         |
|                | <softap_dhcp_status>    |                         |
+----------------+-------------------------+-------------------------+
| **Parameters** | \-                      | -  <mode>:              |
|                |  <station_dhcp_status>: |                         |
|                |                         |    -  : Sets BFQ4004    |
|                |    -  : Station DHCP is |       SoftAP            |
|                |       disabled.         |                         |
|                |                         |    -  1: Sets BFQ4004   |
|                |    -  1: Station DHCP   |       Station           |
|                |       is enabled.       |                         |
|                |                         |    -  2: Sets both      |
|                | -                       |       SoftAP and        |
|                |   <softap_dhcp_status>: |       Station           |
|                |                         |                         |
|                |    -  : SoftAP DHCP is  | -  <en>:                |
|                |       disabled.         |                         |
|                |                         |    -  : Disables DHCP   |
|                |    -  1: SoftAP DHCP is |                         |
|                |          enabled.       |    -  1: Enables DHCP   |
+----------------+-------------------------+-------------------------+
| **Notes**      | -  The configuration                              |
|                |    changes will not be                            |
|                |    saved in flash.                                |
|                |                                                   |
|                | -  The Set Command                                |
|                |    interacts with                                 |
|                |    static-IP-related AT                           |
|                |    commands                                       |
|                |    (AT+CIPSTA-related                             |
|                |    and AT+CIPA-related                            |
|                |    commands):                                     |
|                |                                                   |
|                |    -  If DHCP is                                  |
|                |       enabled, static                             |
|                |       IP will be                                  |
|                |       disabled;                                   |
|                |                                                   |
|                |    -  If static IP is                             |
|                |       enabled, DHCP                               |
|                |       will be disabled;                           |
|                |                                                   |
|                |    -  Whether it is                               |
|                |       DHCP or static IP                           |
|                |       that is enabled                             |
|                |       depends on the                              |
|                |       last                                        |
|                |       configuration.                              |
+----------------+-------------------------+-------------------------+
| **Examples**   | AT+CWDHCP_DEF=,1                                  |
+----------------+-------------------------+-------------------------+

AT+CWDHCPS_CUR - Sets the IP address Range the SoftAP DHCP Server Can Allocate, Configuration Not Saved to Flash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-------------------------+
| **Command**    | Query:                  | Set:                    |
|                |                         |                         |
|                | AT+CWDHCPS_CUR?         | A                       |
|                |                         | T+CWDHCPS_CUR=<enable>, |
|                | Function: to obtain the |                         |
|                | IP address range of the | <lease_ti               |
|                | SoftAP DHCP.            | me>,<start_IP>,<end_IP> |
|                |                         |                         |
|                |                         | Function: to set the IP |
|                |                         | address range of the    |
|                |                         | BFQ4004 SoftAP DHCP     |
|                |                         | server.                 |
+----------------+-------------------------+-------------------------+
| **Response**   | +CW                     | OK                      |
|                | DHCPS_CUR=<lease_time>, |                         |
|                |                         |                         |
|                | <start_IP>,<end_IP>     |                         |
+----------------+-------------------------+-------------------------+
| **Parameters** | -  <enable>:                                      |
|                |                                                   |
|                |    -  : Disable the                               |
|                |       settings and use                            |
|                |       the default IP                              |
|                |       range.                                      |
|                |                                                   |
|                |    -  1: Enable setting                           |
|                |       the IP range, and                           |
|                |       the parameters                              |
|                |       below have to be                            |
|                |       set.                                        |
|                |                                                   |
|                | -  <lease_time>: lease                            |
|                |    time; unit: minute;                            |
|                |    range [1, 288].                                |
|                |                                                   |
|                | -  <star\_ IP>: start                             |
|                |    IP address of the IP                           |
|                |    range that can be                              |
|                |    obtained from                                  |
|                |    BFQ4004 SoftAP DHCP                            |
|                |    server.                                        |
|                |                                                   |
|                | -  <end_IP>: end IP                               |
|                |    address of the IP                              |
|                |    range that can be                              |
|                |    obtained from                                  |
|                |    BFQ4004 SoftAP DHCP                            |
|                |    server.                                        |
+----------------+-------------------------+-------------------------+
| **Notes**      | -  The configuration                              |
|                |    will NOT be saved to                           |
|                |    the flash.                                     |
|                |                                                   |
|                | -  This AT command is                             |
|                |    enabled when BFQ4004                           |
|                |    is configured as                               |
|                |    SoftAP, with DHCP                              |
|                |    enabled. The IP                                |
|                |    address should be in                           |
|                |    the same network                               |
|                |    segment as the IP                              |
|                |    address of BFQ4004                             |
|                |    SoftAP.                                        |
+----------------+-------------------------+-------------------------+
| **Examples**   | A                                                 |
|                | T+CWDHCPS_CUR=1,3,"192.                           |
|                | 168.4.1","192.168.4.15"                           |
|                |                                                   |
|                | or                                                |
|                |                                                   |
|                | AT+CWDHCPS_CUR=                                   |
|                | //Disable the settings                            |
|                | and use the default IP                            |
|                | range.                                            |
+----------------+-------------------------+-------------------------+

AT+CWDHCPS_DEF - Sets the IP address Range the SoftAP DHCP Server Can Allocate, Configuration Saved to Flash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-------------------------+
| **Command**    | Query:                  | Set:                    |
|                |                         |                         |
|                | AT+CWDHCPS_DEF?         | A                       |
|                |                         | T+CWDHCPS_DEF=<enable>, |
|                | Function: to obtain the |                         |
|                | IP address range of the | <lease_ti               |
|                | SoftAP DHCP.            | me>,<start_IP>,<end_IP> |
|                |                         |                         |
|                |                         | Function: to set the IP |
|                |                         | address range of the    |
|                |                         | BFQ4004 SoftAP DHCP     |
|                |                         | server.                 |
+----------------+-------------------------+-------------------------+
| **Response**   | +CW                     | OK                      |
|                | DHCPS_DEF=<lease_time>, |                         |
|                |                         |                         |
|                | <start_IP>,<end_IP>     |                         |
+----------------+-------------------------+-------------------------+
| **Parameters** | -  <enable>:                                      |
|                |                                                   |
|                |    -  : Disable the                               |
|                |       settings and use                            |
|                |       the default IP                              |
|                |       range.                                      |
|                |                                                   |
|                |    -  1: Enable setting                           |
|                |       the IP range, and                           |
|                |       the parameters                              |
|                |       below have to be                            |
|                |       set.                                        |
|                |                                                   |
|                | -  <lease_time>: lease                            |
|                |    time; unit: minute;                            |
|                |    range [1, 288].                                |
|                |                                                   |
|                | -  <star\_ IP>: start                             |
|                |    IP address of the IP                           |
|                |    range that can be                              |
|                |    obtained from                                  |
|                |    BFQ4004 SoftAP DHCP                            |
|                |    server.                                        |
|                |                                                   |
|                | -  <end_IP>: end IP                               |
|                |    address of the IP                              |
|                |    range that can be                              |
|                |    obtained from                                  |
|                |    BFQ4004 SoftAP DHCP                            |
|                |    server.                                        |
+----------------+-------------------------+-------------------------+
| **Notes**      | -  The configuration                              |
|                |    will NOT be saved to                           |
|                |    the flash.                                     |
|                |                                                   |
|                | -  This AT command is                             |
|                |    enabled when BFQ4004                           |
|                |    is configured as                               |
|                |    SoftAP, with DHCP                              |
|                |    enabled. The IP                                |
|                |    address should be in                           |
|                |    the same network                               |
|                |    segment as the IP                              |
|                |    address of BFQ4004                             |
|                |    SoftAP.                                        |
+----------------+-------------------------+-------------------------+
| **Examples**   | A                                                 |
|                | T+CWDHCPS_DEF=1,3,"192.                           |
|                | 168.4.1","192.168.4.15"                           |
|                |                                                   |
|                | or                                                |
|                |                                                   |
|                | AT+CWDHCPS_DEF=                                   |
|                | //Disable the settings                            |
|                | and use the default IP                            |
|                | range.                                            |
+----------------+-------------------------+-------------------------+

AT+CWAUTOCONN – Automatically Connects to the AP on Power-up or Not
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-----------------+---------------------------------------------------+
| **Set Command** | AT+CWAUTOCONN=<enable>                            |
+-----------------+---------------------------------------------------+
| **Response**    | OK                                                |
+-----------------+---------------------------------------------------+
| **Parameters**  |    <enable>:                                      |
|                 |                                                   |
|                 | -  : does NOT auto-connect to AP on power-up.     |
|                 |                                                   |
|                 | -  1: connects to AP automatically on power-up    |
|                 |    (default).                                     |
+-----------------+---------------------------------------------------+
| **Notes**       | The configuration changes will be saved in the    |
|                 | system parameter area in the flash.               |
+-----------------+---------------------------------------------------+
| **Examples**    | AT+CWAUTOCONN=                                    |
+-----------------+---------------------------------------------------+

AT+CIPSTA_CUR – Sets the Current IP Address of the BFQ4004 Station, Configuration Not Saved in Flash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-------------------------+
| **Command**    | Query:                  | Set:                    |
|                |                         |                         |
|                | AT+CIPSTA_CUR?          | AT+CIPS                 |
|                |                         | TA_CUR=<ip>,[<gateway>, |
|                | Function: to obtain the |                         |
|                | IP address of the       | <netmask>]              |
|                | BFQ4004 Station.        |                         |
|                |                         | Function: to set the    |
|                |                         | current IP address of   |
|                |                         | the BFQ4004 Station.    |
+----------------+-------------------------+-------------------------+
| **Response**   | +CIPSTA_CUR:<ip>        | OK                      |
|                |                         |                         |
|                | +CIPSTA_CUR:<gateway>   |                         |
|                |                         |                         |
|                | +CIPSTA_CUR:<netmask>   |                         |
|                |                         |                         |
|                | OK                      |                         |
+----------------+-------------------------+-------------------------+
| **Parameters** | -  <ip>: string                                   |
|                |    parameter, the IP                              |
|                |    address of the                                 |
|                |    BFQ4004 Station.                               |
|                |                                                   |
|                | -  [<gateway>]:                                   |
|                |    gateway.                                       |
|                |                                                   |
|                | -  [<netmask>]:                                   |
|                |    netmask.                                       |
+----------------+-------------------------+-------------------------+
| **Notes**      | ️ **Warning:**                                    |
|                |                                                   |
|                | Only when the BFQ4004                             |
|                | Station is connected to                           |
|                | an AP can its IP                                  |
|                | address be queried.                               |
|                |                                                   |
|                | -  The configuration                              |
|                |    will NOT be saved to                           |
|                |    the flash.                                     |
|                |                                                   |
|                | -  The Set Command                                |
|                |    interacts with                                 |
|                |    DHCP-related AT                                |
|                |    commands                                       |
|                |    (AT+CWDHCP-related                             |
|                |    commands):                                     |
|                |                                                   |
|                |    -  If static IP is                             |
|                |       enabled, DHCP                               |
|                |       will be disabled;                           |
|                |                                                   |
|                |    -  If DHCP is                                  |
|                |       enabled, static                             |
|                |       IP will be                                  |
|                |       disabled;                                   |
|                |                                                   |
|                |    -  Whether it is                               |
|                |       DHCP or static IP                           |
|                |       that is enabled                             |
|                |       depends on the                              |
|                |       last                                        |
|                |       configuration.                              |
+----------------+-------------------------+-------------------------+
| **Examples**   | AT+CIPSTA_                                        |
|                | CUR="192.168.6.1","192.                           |
|                | 168.6.1","255.255.255.”                           |
+----------------+-------------------------+-------------------------+

AT+CIPSTA_DEF - Sets the Default IP Address of the BFQ4004 Station, Configuration Saved in Flash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-------------------------+
| **Command**    | Query:                  | Set:                    |
|                |                         |                         |
|                | AT+CIPSTA_DEF?          | AT+CIPS                 |
|                |                         | TA_DEF=<ip>,[<gateway>, |
|                | Function: to obtain the |                         |
|                | IP address of the       | <netmask>]              |
|                | BFQ4004 Station.        |                         |
|                |                         | Function: to set the    |
|                |                         | current IP address of   |
|                |                         | the BFQ4004 Station.    |
+----------------+-------------------------+-------------------------+
| **Response**   | +CIPSTA_DEF:<ip>        | OK                      |
|                |                         |                         |
|                | +CIPSTA_DEF:<gateway>   |                         |
|                |                         |                         |
|                | +CIPSTA_DEF:<netmask>   |                         |
|                |                         |                         |
|                | OK                      |                         |
+----------------+-------------------------+-------------------------+
| **Parameters** | -  <ip>: string                                   |
|                |    parameter, the IP                              |
|                |    address of the                                 |
|                |    BFQ4004 Station.                               |
|                |                                                   |
|                | -  [<gateway>]:                                   |
|                |    gateway.                                       |
|                |                                                   |
|                | -  [<netmask>]:                                   |
|                |    netmask.                                       |
+----------------+-------------------------+-------------------------+
| **Notes**      | ️ **Warning:**                                    |
|                |                                                   |
|                | Only when the BFQ4004                             |
|                | Station is connected to                           |
|                | an AP can its IP                                  |
|                | address be queried.                               |
|                |                                                   |
|                | -  The configuration                              |
|                |    will be saved to the                           |
|                |    flash.                                         |
|                |                                                   |
|                | -  The Set Command                                |
|                |    interacts with                                 |
|                |    DHCP-related AT                                |
|                |    commands                                       |
|                |    (AT+CWDHCP-related                             |
|                |    commands):                                     |
|                |                                                   |
|                |    -  If static IP is                             |
|                |       enabled, DHCP                               |
|                |       will be disabled;                           |
|                |                                                   |
|                |    -  If DHCP is                                  |
|                |       enabled, static                             |
|                |       IP will be                                  |
|                |       disabled;                                   |
|                |                                                   |
|                |    -  Whether it is                               |
|                |       DHCP or static IP                           |
|                |       that is enabled                             |
|                |       depends on the                              |
|                |       last                                        |
|                |       configuration.                              |
+----------------+-------------------------+-------------------------+
| **Examples**   | AT+CIPSTA_                                        |
|                | DEF="192.168.6.1","192.                           |
|                | 168.6.1","255.255.255.”                           |
+----------------+-------------------------+-------------------------+

AT+CIPAP_CUR – Sets the Current IP Address of the BFQ4004 SoftAP, Configuration Not Saved in Flash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-------------------------+
| **Command**    | Query:                  | Set:                    |
|                |                         |                         |
|                | AT+CIPAP_CUR?           | AT+CIP                  |
|                |                         | AP_CUR=<ip>,[<gateway>, |
|                | Function: to obtain the |                         |
|                | IP address of the       | <netmask>]              |
|                | BFQ4004 SoftAP.         |                         |
|                |                         | Function: to set the    |
|                |                         | current IP address of   |
|                |                         | the BFQ4004 SoftAP.     |
+----------------+-------------------------+-------------------------+
| **Response**   | +CIPAP_CUR:<ip>         | OK                      |
|                |                         |                         |
|                | +CIPAP_CUR:<gateway>    |                         |
|                |                         |                         |
|                | +CIPAP_CUR:<netmask>    |                         |
|                |                         |                         |
|                | OK                      |                         |
+----------------+-------------------------+-------------------------+
| **Parameters** | -  <ip>: string                                   |
|                |    parameter, the IP                              |
|                |    address of the                                 |
|                |    BFQ4004 SoftAP.                                |
|                |                                                   |
|                | -  [<gateway>]:                                   |
|                |    gateway.                                       |
|                |                                                   |
|                | -  [<netmask>]:                                   |
|                |    netmask.                                       |
+----------------+-------------------------+-------------------------+
| **Notes**      | -  The configuration                              |
|                |    will NOT be saved to                           |
|                |    the flash.                                     |
|                |                                                   |
|                | -  Currently, only                                |
|                |    supports class C IP                            |
|                |    addresses.                                     |
|                |                                                   |
|                | -  The Set Command                                |
|                |    interacts with                                 |
|                |    DHCP-related AT                                |
|                |    commands                                       |
|                |    (AT+CWDHCP-related                             |
|                |    commands):                                     |
|                |                                                   |
|                |    -  If static IP is                             |
|                |       enabled, DHCP                               |
|                |       will be disabled;                           |
|                |                                                   |
|                |    -  If DHCP is                                  |
|                |       enabled, static                             |
|                |       IP will be                                  |
|                |       disabled;                                   |
|                |                                                   |
|                |    -  Whether it is                               |
|                |       DHCP or static IP                           |
|                |       that is enabled                             |
|                |       depends on the                              |
|                |       last                                        |
|                |       configuration.                              |
+----------------+-------------------------+-------------------------+
| **Examples**   | AT+CIPAP_                                         |
|                | CUR="192.168.5.1","192.                           |
|                | 168.5.1","255.255.255."                           |
+----------------+-------------------------+-------------------------+

AT+CIPAP_DEF - Sets the Default IP Address of the BFQ4004 SoftAP, Configuration Saved in Flash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-------------------------+
| **Command**    | Query:                  | Set:                    |
|                |                         |                         |
|                | AT+CIPAP_DEF?           | AT+CIP                  |
|                |                         | AP_DEF=<ip>,[<gateway>, |
|                | Function: to obtain the |                         |
|                | IP address of the       | <netmask>]              |
|                | BFQ4004 SoftAP.         |                         |
|                |                         | Function: to set the    |
|                |                         | current IP address of   |
|                |                         | the BFQ4004 SoftAP.     |
+----------------+-------------------------+-------------------------+
| **Response**   | +CIPAP_DEF:<ip>         | OK                      |
|                |                         |                         |
|                | +CIPAP_DEF:<gateway>    |                         |
|                |                         |                         |
|                | +CIPAP_DEF:<netmask>    |                         |
|                |                         |                         |
|                | OK                      |                         |
+----------------+-------------------------+-------------------------+
| **Parameters** | -  <ip>: string                                   |
|                |    parameter, the IP                              |
|                |    address of the                                 |
|                |    BFQ4004 SoftAP.                                |
|                |                                                   |
|                | -  [<gateway>]:                                   |
|                |    gateway.                                       |
|                |                                                   |
|                | -  [<netmask>]:                                   |
|                |    netmask.                                       |
+----------------+-------------------------+-------------------------+
| **Notes**      | -  The configuration                              |
|                |    will be saved to the                           |
|                |    flash.                                         |
|                |                                                   |
|                | -  Currently, only                                |
|                |    supports class C IP                            |
|                |    addresses.                                     |
|                |                                                   |
|                | -  The Set Command                                |
|                |    interacts with                                 |
|                |    DHCP-related AT                                |
|                |    commands                                       |
|                |    (AT+CWDHCP-related                             |
|                |    commands):                                     |
|                |                                                   |
|                |    -  If static IP is                             |
|                |       enabled, DHCP                               |
|                |       will be disabled;                           |
|                |                                                   |
|                |    -  If DHCP is                                  |
|                |       enabled, static                             |
|                |       IP will be                                  |
|                |       disabled;                                   |
|                |                                                   |
|                |    -  Whether it is                               |
|                |       DHCP or static IP                           |
|                |       that is enabled                             |
|                |       depends on the                              |
|                |       last                                        |
|                |       configuration.                              |
+----------------+-------------------------+-------------------------+
| **Examples**   | AT+CIPAP_                                         |
|                | DEF="192.168.5.1","192.                           |
|                | 168.5.1","255.255.255."                           |
+----------------+-------------------------+-------------------------+

AT+WPS – Enables the WPS Function
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-----------------+---------------------------------------------------+
| **Set Command** | AT+WPS=<enable>                                   |
+-----------------+---------------------------------------------------+
| **Response**    | OK                                                |
+-----------------+---------------------------------------------------+
| **Parameters**  |    <enable>:                                      |
|                 |                                                   |
|                 | -  : disables WPS.                                |
|                 |                                                   |
|                 | -  1: enables WPS (Wi-Fi Protected Setup)         |
+-----------------+---------------------------------------------------+
| **Notes**       | -  WPS must be used when the BFQ4004 Station is   |
|                 |    enabled.                                       |
|                 |                                                   |
|                 | -  WPS does not support WEP (Wired-Equivalent     |
|                 |    Privacy) encryption.                           |
+-----------------+---------------------------------------------------+
| **Examples**    | AT+CWMODE=1                                       |
|                 |                                                   |
|                 | AT+WPS=1                                          |
+-----------------+---------------------------------------------------+

AT+CWHOSTNAME – Configures the Name of BFQ4004 Station
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-------------------------+
| **Command**    | Query:                  | Set:                    |
|                |                         |                         |
|                | AT+CWHOSTNAME?          | AT+ CWHOSTNAME          |
|                |                         | =<hostname>             |
|                | Function: to check the  |                         |
|                | name of the BFQ4004     | Function: to set the    |
|                | Station.                | name of the BFQ4004     |
|                |                         | Station.                |
+----------------+-------------------------+-------------------------+
| **Response**   | +CWHOSTNAME:<hostname>  | OK                      |
|                |                         |                         |
|                | OK                      | If the Station mode is  |
|                |                         | not enabled, the        |
|                | If the Station mode is  | command will return:    |
|                | not enabled, the        |                         |
|                | command will return:    | ERROR                   |
|                |                         |                         |
|                | +CWHOSTNAME:<null>      |                         |
|                |                         |                         |
|                | OK                      |                         |
+----------------+-------------------------+-------------------------+
| **Parameters** | <hostname>: the host                              |
|                | name of the BFQ4004                               |
|                | Station, the maximum                              |
|                | length is 32 bytes.                               |
+----------------+-------------------------+-------------------------+
| **Notes**      | -  The configuration                              |
|                |    changes are NOT                                |
|                |    saved in the flash.                            |
|                |                                                   |
|                | -  The default host                               |
|                |    name of the BFQ4004                            |
|                |    Station is                                     |
|                |    BFQ4004_XXXXXX;                                |
|                |    XXXXXX is the lower                            |
|                |    3 bytes of the MAC                             |
|                |    address, for                                   |
|                |    example,                                       |
|                |    +CWHOS                                         |
|                | TNAME:<BFQ4004_A378DA>.                           |
+----------------+-------------------------+-------------------------+
| **Examples**   | AT+CWMODE=1                                       |
|                |                                                   |
|                | AT+CWHOSTNAME="my_test"                           |
+----------------+-------------------------+-------------------------+

AT+CWCOUNTRY_CUR – Sets the Current Wi-Fi Country Code, Configuration Not Saved in Flash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-------------------------+
| **Command**    | Query:                  | Set:                    |
|                |                         |                         |
|                | AT+CWCOUNTRY_CUR?       | AT+ CWCPUNTRY_CUR=      |
|                |                         |                         |
|                | Function: to check the  | <country_               |
|                | current WiFi country    | policy>,<country_code>, |
|                | code of BQ4004          |                         |
|                |                         | <start_channel>,        |
|                |                         |                         |
|                |                         | <total_channel_count>   |
|                |                         |                         |
|                |                         | Function: to set the    |
|                |                         | current WiFi country    |
|                |                         | code of BFA4004.        |
+----------------+-------------------------+-------------------------+
| **Response**   | | +CWCOUNTRY_CUR:       | OK                      |
|                | | <country_policy>,     |                         |
|                | | <country_code>,       |                         |
|                | | <start_channel>,      |                         |
|                | | <total_channel_count> |                         |
|                |                         |                         |
|                | OK                      |                         |
|                |                         |                         |
|                | AT+CWCOUNTRY_CUR?       |                         |
|                | returns the actual      |                         |
|                | value of WiFi country   |                         |
|                | code, which may be      |                         |
|                | changed to the same as  |                         |
|                | the AP it connected to. |                         |
+----------------+-------------------------+-------------------------+
| **Parameters** | -  <country_policy>:                              |
|                |                                                   |
|                |    -  : will change the                           |
|                |       county code to be                           |
|                |       the same as the                             |
|                |       AP that BFQ4004                             |
|                |       is connected to                             |
|                |                                                   |
|                |    -  1: the country                              |
|                |       code will not                               |
|                |       change, always be                           |
|                |       the one set by                              |
|                |       command.                                    |
|                |                                                   |
|                | -  <country_code>:                                |
|                |    country code, the                              |
|                |    length can be 3                                |
|                |    characters at most;                            |
|                |    but the third                                  |
|                |    character is a                                 |
|                |    special character                              |
|                |    which will not be                              |
|                |    shown when querying                            |
|                |    by command                                     |
|                |    AT+CWCOUNTRY_CUR?                              |
|                |                                                   |
|                | -  <start_channel> :                              |
|                |    the channel number                             |
|                |    to start at.                                   |
|                |                                                   |
|                | -                                                 |
|                |   <total_channel_count>                           |
|                |    : channel count.                               |
+----------------+-------------------------+-------------------------+
| **Notes**      | The configuration                                 |
|                | changes are NOT saved                             |
|                | in the flash.                                     |
+----------------+-------------------------+-------------------------+
| **Examples**   | AT+CWMODE=1                                       |
|                |                                                   |
|                | AT+CW                                             |
|                | COUNTRY_CUR=1,”US”,1,13                           |
+----------------+-------------------------+-------------------------+

AT+CWCOUNTRY_DEF – Sets the Default Wi-Fi Country Code, Configuration Save in Flash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-------------------------+
| **Command**    | Query:                  | Set:                    |
|                |                         |                         |
|                | AT+CWCOUNTRY_DEF?       | AT+ CWCPUNTRY_DEF=      |
|                |                         | <country_               |
|                | Function: to check the  | policy>,<country_code>, |
|                | default WiFi country    |                         |
|                | code of BQ4004          | <start_channel>,        |
|                |                         |                         |
|                |                         | <total_channel_count>   |
|                |                         |                         |
|                |                         | Function: to set the    |
|                |                         | default WiFi country    |
|                |                         | code of BFA4004.        |
+----------------+-------------------------+-------------------------+
| **Response**   | | +CWCOUNTRY_DEF:       | OK                      |
|                | | <country_policy>,     |                         |
|                | | <country_code>,       |                         |
|                | | <start_channel>,      |                         |
|                | | <total_channel_count> |                         |
|                |                         |                         |
|                | OK                      |                         |
|                |                         |                         |
|                | AT+CWCOUNTRY_DEF?       |                         |
|                | returns the default     |                         |
|                | value of WiFi country   |                         |
|                | code stored in the      |                         |
|                | flash.                  |                         |
+----------------+-------------------------+-------------------------+
| **Parameters** | -  <country_policy>:                              |
|                |                                                   |
|                |    -  : will change the                           |
|                |       county code to be                           |
|                |       the same as the                             |
|                |       AP that BFQ4004                             |
|                |       is connected to                             |
|                |                                                   |
|                |    -  1: the country                              |
|                |       code will not                               |
|                |       change, always be                           |
|                |       the one set by                              |
|                |       command.                                    |
|                |                                                   |
|                | -  <country_code>:                                |
|                |    country code, the                              |
|                |    length can be 3                                |
|                |    characters at most;                            |
|                |    but the third                                  |
|                |    character is a                                 |
|                |    special character                              |
|                |    which will not be                              |
|                |    shown when querying                            |
|                |    by command                                     |
|                |    AT+CWCOUNTRY_DEF?                              |
|                |                                                   |
|                | -  <start_channel> :                              |
|                |    the channel number                             |
|                |    to start at.                                   |
|                |                                                   |
|                | -                                                 |
|                |   <total_channel_count>                           |
|                |    : channel count.                               |
+----------------+-------------------------+-------------------------+
| **Notes**      | The configuration                                 |
|                | changes are saved in                              |
|                | the user parameter area                           |
|                | of the flash.                                     |
+----------------+-------------------------+-------------------------+
| **Examples**   | AT+CWMODE=1                                       |
|                |                                                   |
|                | AT+CW                                             |
|                | COUNTRY_DEF=1,”US”,1,13                           |
+----------------+-------------------------+-------------------------+

TCP/IP-Related AT Commands
==========================

.. _overview-4:

Overview
--------

+---------------------+-----------------------------------------------+
| **Commands**        | **Description**                               |
+=====================+===============================================+
| AT+CIPSTATUS        | Gets the connection status                    |
+---------------------+-----------------------------------------------+
| AT+CIPDOMAIN        | DNS function                                  |
+---------------------+-----------------------------------------------+
| AT+CIPSTART         | Establishes TCP connection, UDP transmission  |
|                     | or SSL connection                             |
+---------------------+-----------------------------------------------+
| AT+CIPSSLSIZE       | Sets the size of SSL buffer                   |
+---------------------+-----------------------------------------------+
| AT+CIPSSLCCONF      | Configures the SSL client                     |
+---------------------+-----------------------------------------------+
| AT+CIPSEND          | Sends Data                                    |
+---------------------+-----------------------------------------------+
| AT+CIPSENDEX        | Sends data when length of data is <length>,   |
|                     | or when \\ appears in the data                |
+---------------------+-----------------------------------------------+
| AT+CIPSENDBUF       | Writes data into TCP-send-buffer              |
+---------------------+-----------------------------------------------+
| AT+CIPBUFRESET      | Resets the segment ID count                   |
+---------------------+-----------------------------------------------+
| AT+CIPBUFSTATUS     | Checks the status of TCP-send-buffer          |
+---------------------+-----------------------------------------------+
| AT+CIPCHECKSEQ      | Checks if a specific segment is sent or not   |
+---------------------+-----------------------------------------------+
| AT+CIPCLOSE         | Closes TCP/UDP/SSL connection                 |
+---------------------+-----------------------------------------------+
| AT+CIFSR            | Gets the local IP address                     |
+---------------------+-----------------------------------------------+
| AT+CIPMUX           | Configures the multiple connections mode      |
+---------------------+-----------------------------------------------+
| AT+CIPSERVER        | Creates or deletes TCP server                 |
+---------------------+-----------------------------------------------+
| AT+CIPSERVERMAXCONN | Set the maximum connections that server       |
|                     | allows                                        |
+---------------------+-----------------------------------------------+
| AT+CIPMODE          | Configures the transmission mode              |
+---------------------+-----------------------------------------------+
| AT+CIPSTO           | Sets timeout when BFQ4004 runs as TCP server  |
+---------------------+-----------------------------------------------+
| AT+PING             | Ping packets                                  |
+---------------------+-----------------------------------------------+
| AT+CIUPDATE         | Upgrades the software through network         |
+---------------------+-----------------------------------------------+
| AT+CIPDINFO         | Shows remote IP and remote port with +IPD     |
+---------------------+-----------------------------------------------+
| +IPD                | BFQ4004 receives network data                 |
+---------------------+-----------------------------------------------+
| AT+CIPRECVMODE      | Set TCP Receive Mode                          |
+---------------------+-----------------------------------------------+
| AT+CIPRECVDATA      | Get TCP Data in Passive Receive Mode          |
+---------------------+-----------------------------------------------+
| AT+CIPRECVLEN       | Get TCP Data Length in Passive Receive Mode   |
+---------------------+-----------------------------------------------+
| AT+CIPSNTPCFG       | Configures the time domain and SNTP server.   |
+---------------------+-----------------------------------------------+
| AT+CIPSNTPTIME      | Queries the SNTP time.                        |
+---------------------+-----------------------------------------------+
| AT+CIPDNS_CUR       | Sets user-defined DNS servers; configuration  |
|                     | not saved in flash                            |
+---------------------+-----------------------------------------------+
| AT+CIPDNS_DEF       | Sets user-defined DNS servers; configuration  |
|                     | saved in flash                                |
+---------------------+-----------------------------------------------+

.. _command-descriptions-3:

Command Descriptions
--------------------

AT+CIPSTATUS – Gets the Connection Status
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+---------------------+-----------------------------------------------+
| **Execute Command** | AT+CIPSTATUS                                  |
+---------------------+-----------------------------------------------+
| **Response**        | STATUS:<status>                               |
|                     |                                               |
|                     | | +CIPSTATUS:<li                              |
|                     | nk_ID>,<conn_type>,<remote_IP>,<remote_port>, |
|                     | | <local_port>,<tetype>                       |
+---------------------+-----------------------------------------------+
| **Parameters**      | -  <status>: status of the BFQ4004 Station    |
|                     |    interface.                                 |
|                     |                                               |
|                     |    -  2: The BFQ4004 Station is connected to  |
|                     |       an AP and a remote IP is obtained       |
|                     |       (connected to remote IP).               |
|                     |                                               |
|                     |    -  3: The BFQ4004 Station has established  |
|                     |       a TCP connection or is transmitting in  |
|                     |       UDP (communication established).        |
|                     |                                               |
|                     |    -  4: The TCP or UDP is disconnected and   |
|                     |       remote IP is lost, but BFQ4004 is still |
|                     |       connected to an AP (not connected to    |
|                     |       remote IP but is still connected to an  |
|                     |       AP).                                    |
|                     |                                               |
|                     |    -  5: The BFQ4004 Station is not connect   |
|                     |       to an AP (lost AP).                     |
|                     |                                               |
|                     | -  <link_ID>: ID of the connection (0~4),     |
|                     |    used for multiple connections.             |
|                     |                                               |
|                     | -  <conn_type>: string parameter, "TCP" or    |
|                     |    "UDP".                                     |
|                     |                                               |
|                     | -  <remote \_IP>: string parameter indicating |
|                     |    the remote IP address.                     |
|                     |                                               |
|                     | -  <remote_port>: the remote port number.     |
|                     |                                               |
|                     | -  <local_port>: BFQ4004 local port number.   |
|                     |                                               |
|                     | -  <tetype>:                                  |
|                     |                                               |
|                     |    -  : BFQ4004 runs as a client.             |
|                     |                                               |
|                     |    -  1: BFQ4004 runs as a server.            |
+---------------------+-----------------------------------------------+

AT+CIPDOMAIN – DNS Function
~~~~~~~~~~~~~~~~~~~~~~~~~~~

+---------------------+-----------------------------------------------+
| **Execute Command** | AT+CIPDOMAIN=<domain_name>                    |
+---------------------+-----------------------------------------------+
| **Response**        | +CIPDOMAIN:<IP_address>                       |
|                     |                                               |
|                     | OK                                            |
|                     |                                               |
|                     | or                                            |
|                     |                                               |
|                     | DNS Fail                                      |
|                     |                                               |
|                     | ERROR                                         |
+---------------------+-----------------------------------------------+
| **Parameters**      | -  <domain_name>: the domain name. Max length |
|                     |    is 64 bytes.                               |
|                     |                                               |
|                     | -  <IP_address>: the IP address corresponding |
|                     |    to the domain name.                        |
+---------------------+-----------------------------------------------+
| **Examples**        | AT+CWMODE=1 // set Station mode               |
|                     |                                               |
|                     | AT+CWJAP="SSID","password" // access to the   |
|                     | internet                                      |
|                     |                                               |
|                     | AT+CIPDOMAIN="www.beefi.io" // DNS function   |
+---------------------+-----------------------------------------------+

AT+CIPSTART – Establishes TCP Connection, UDP Transmission or SSL Connection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Establish TCP Connection
^^^^^^^^^^^^^^^^^^^^^^^^

+-----------------+------------------------+------------------------+
| **Set Command** | Single connection      | Multiple Connections   |
|                 | (AT+CIPMUX=):          | (AT+CIPMUX=1):         |
|                 |                        |                        |
|                 | | AT                   | |                      |
|                 | +CIPSTART=<conn_type>, | AT+CIPSTART=<link_ID>, |
|                 | | <r                   | | <conn_type>,         |
|                 | emote_IP/domain_name>, | | <r                   |
|                 | | <remote_port>        | emote_IP/domain_name>, |
|                 | | [,<TCP_keep_alive>]  | | <remote_po           |
|                 |                        | rt>[,<TCP_keep_alive>] |
+-----------------+------------------------+------------------------+
| **Response**    | OK                                              |
|                 |                                                 |
|                 | or                                              |
|                 |                                                 |
|                 | ERROR                                           |
|                 |                                                 |
|                 | If the TCP connection                           |
|                 | is already                                      |
|                 | established, the                                |
|                 | response is:                                    |
|                 |                                                 |
|                 | ALREADY CONNECTED                               |
+-----------------+------------------------+------------------------+
| **Parameters**  | -  <link_ID>: ID of                             |
|                 |    network connection                           |
|                 |    (0~4), used for                              |
|                 |    multiple                                     |
|                 |    connections.                                 |
|                 |                                                 |
|                 | -  <conn_type>: string                          |
|                 |    parameter                                    |
|                 |    indicating the                               |
|                 |    connection type:                             |
|                 |    "TCP", "UDP" or                              |
|                 |    "SSL".                                       |
|                 |                                                 |
|                 | -  <r                                           |
|                 | emote_IP/domain_name>:                          |
|                 |    string parameter                             |
|                 |    indicating the                               |
|                 |    remote IP address                            |
|                 |    or domain name to                            |
|                 |    connect to.                                  |
|                 |                                                 |
|                 | -  <remote_port>: the                           |
|                 |    remote port number.                          |
|                 |                                                 |
|                 | -  [<TCP_keep_alive>]:                          |
|                 |    optional; detection                          |
|                 |    time interval when                           |
|                 |    TCP is kept alive.                           |
|                 |                                                 |
|                 |    -  : disable TCP                             |
|                 |       keep-alive                                |
|                 |       (default)                                 |
|                 |                                                 |
|                 |    -  1 ~ 72:                                   |
|                 |       detection time                            |
|                 |       interval; unit:                           |
|                 |       second (s).                               |
+-----------------+------------------------+------------------------+
| **Notes**       | The configuration                               |
|                 | changes are saved in                            |
|                 | the user parameter                              |
|                 | area of the flash.                              |
+-----------------+------------------------+------------------------+
| **Examples**    | AT+CIPSTART=                                    |
|                 | "TCP","www.beefi.io",8                          |
|                 |                                                 |
|                 | AT+CIPSTART="                                   |
|                 | TCP","192.168.11.11",1                          |
|                 |                                                 |
|                 | For more information                            |
|                 | please see: BFQ4004 AT                          |
|                 | Command Examples.                               |
+-----------------+------------------------+------------------------+

Establish UDP Transmission
^^^^^^^^^^^^^^^^^^^^^^^^^^

+-----------------+------------------------+------------------------+
| **Set Command** | Single connection      | Multiple Connections   |
|                 | (AT+CIPMUX=):          | (AT+CIPMUX=1):         |
|                 |                        |                        |
|                 | | AT                   | |                      |
|                 | +CIPSTART=<conn_type>, | AT+CIPSTART=<link_ID>, |
|                 | | <r                   | | <conn_type>,         |
|                 | emote_IP/domain_name>, | | <r                   |
|                 | | <remote_port>        | emote_IP/domain_name>, |
|                 | | [,<l                 | | <remote_port>        |
|                 | ocal_port>,<UDP_mode>] | | [,<l                 |
|                 |                        | ocal_port>,<UDP_mode>] |
+-----------------+------------------------+------------------------+
| **Response**    | OK                                              |
|                 |                                                 |
|                 | or                                              |
|                 |                                                 |
|                 | ERROR                                           |
|                 |                                                 |
|                 | If the UDP                                      |
|                 | transmission is                                 |
|                 | already established,                            |
|                 | the response is:                                |
|                 |                                                 |
|                 | ALREADY CONNECTED                               |
+-----------------+------------------------+------------------------+
| **Parameters**  | -  <link_ID>: ID of                             |
|                 |    network connection                           |
|                 |    (0~4), used for                              |
|                 |    multiple                                     |
|                 |    connections.                                 |
|                 |                                                 |
|                 | -  <conn_type>: string                          |
|                 |    parameter                                    |
|                 |    indicating the                               |
|                 |    connection type:                             |
|                 |    "TCP", "UDP" or                              |
|                 |    "SSL".                                       |
|                 |                                                 |
|                 | -  <r                                           |
|                 | emote_IP/domain_name>:                          |
|                 |    string parameter                             |
|                 |    indicating the                               |
|                 |    remote IP address                            |
|                 |    or domain name to                            |
|                 |    connect to.                                  |
|                 |                                                 |
|                 | -  <remote_port>: the                           |
|                 |    remote port number.                          |
|                 |                                                 |
|                 | -  [<local_port>]:                              |
|                 |    optional; UDP port                           |
|                 |    of BFQ4004.                                  |
|                 |                                                 |
|                 | -  [<UDP_mode>]:                                |
|                 |    optional; In the                             |
|                 |    UDP transparent                              |
|                 |    transmission, the                            |
|                 |    value of this                                |
|                 |    parameter has to be                          |
|                 |    .                                            |
|                 |                                                 |
|                 |    -  : the                                     |
|                 |       destination peer                          |
|                 |       entity of UDP                             |
|                 |       will not change                           |
|                 |       (default).                                |
|                 |                                                 |
|                 |    -  1: the                                    |
|                 |       destination peer                          |
|                 |       entity of UDP                             |
|                 |       can change once.                          |
|                 |                                                 |
|                 |    -  2: the                                    |
|                 |       destination peer                          |
|                 |       entity of UDP is                          |
|                 |       allowed to                                |
|                 |       change.                                   |
|                 |                                                 |
|                 | ️ **Warning:**                                  |
|                 |                                                 |
|                 | To use <UDP_mode>,                              |
|                 | <local_port> must be                            |
|                 | set first.                                      |
+-----------------+------------------------+------------------------+
| **Examples**    | AT+CIPSTART="UDP",                              |
|                 | "192.168.11.11",1,12,2                          |
|                 |                                                 |
|                 | For more information                            |
|                 | please see: BFQ4004 AT                          |
|                 | Command Examples.                               |
+-----------------+------------------------+------------------------+

Establish SSL Connection
^^^^^^^^^^^^^^^^^^^^^^^^

+-----------------+---------------------------------------------------+
| **Set Command** | AT+CIPSTART=                                      |
|                 | [<link_ID>,]<conn_type>,<remote_IP>,<remote_port> |
|                 |                                                   |
|                 | [,<TCP keep alive>]                               |
+-----------------+---------------------------------------------------+
| **Response**    | OK                                                |
|                 |                                                   |
|                 | or                                                |
|                 |                                                   |
|                 | ERROR                                             |
|                 |                                                   |
|                 | If the TCP connection is already established, the |
|                 | response is:                                      |
|                 |                                                   |
|                 | ALREADY CONNECTED                                 |
+-----------------+---------------------------------------------------+
| **Parameters**  | -  <link_ID>: ID of network connection (0~4),     |
|                 |    used for multiple connections.                 |
|                 |                                                   |
|                 | -  <conn_type>: string parameter indicating the   |
|                 |    connection type: "TCP", "UDP" or "SSL".        |
|                 |                                                   |
|                 | -  <remote_IP/domain_name>: string parameter      |
|                 |    indicating the remote IP address or domain     |
|                 |    name to connect to.                            |
|                 |                                                   |
|                 | -  <remote_port>: the remote port number.         |
|                 |                                                   |
|                 | -  [<TCP_keep_alive>]: optional; detection time   |
|                 |    interval when TCP is kept alive.               |
|                 |                                                   |
|                 |    -  : disable TCP keep-alive (default)          |
|                 |                                                   |
|                 |    -  1 ~ 72: detection time interval; unit:      |
|                 |       second (s).                                 |
+-----------------+---------------------------------------------------+
| **Notes**       | -  BFQ4004 can only set one SSL connection at     |
|                 |    most.                                          |
|                 |                                                   |
|                 | -  SSL connection does not support UART-Wi-Fi     |
|                 |    passthrough mode (transparent transmission).   |
|                 |                                                   |
|                 | -  (HOW ABOUT MUTUAL SSL? ADD HERE?)              |
|                 |                                                   |
|                 | ..                                                |
|                 |                                                   |
|                 |    ️ **Warning:**                                 |
|                 |                                                   |
|                 |    SSL connection needs a large amount of memory. |
|                 |    Please use the command AT+CIPSSLSIZE=<size> as |
|                 |    neede to enlarge the SSL buffer size.          |
|                 |    Insufficient buffer size may cause system to   |
|                 |    reboot.                                        |
|                 |                                                   |
|                 |    #                                              |
+-----------------+---------------------------------------------------+
| **Examples**    | AT+CIPSTART="SSL","www.beefi.io",8443             |
+-----------------+---------------------------------------------------+

AT+CIPSSLSIZE – Sets the Size of the SSL Buffer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-----------------+---------------------------------------------------+
| **Set Command** | AT+CIPSSLSIZE=<size>                              |
+-----------------+---------------------------------------------------+
| **Response**    | OK                                                |
+-----------------+---------------------------------------------------+
| **Parameters**  | <size>: the size of the SSL buffer; range of      |
|                 | value: [248, 496].                                |
+-----------------+---------------------------------------------------+
| **Examples**    | AT+CIPSSLSIZE=496                                 |
+-----------------+---------------------------------------------------+

AT+CIPSSLCCONF – Configures the SSL Client
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-------------------------+
| **Command**    | Query:                  | Set:                    |
|                |                         |                         |
|                | AT+CIPSSLCCONF?         | AT+CIPSSLCCONF=<SSL     |
|                |                         | mode>                   |
|                | Function: gets the      |                         |
|                | configuration of the    | Function: sets the      |
|                | BFQ4004 SSL client.     | configuration of the    |
|                |                         | BFQ4004 SSL client.     |
+----------------+-------------------------+-------------------------+
| **Response**   | +CIPSSLCCONF:<SSL mode> | OK                      |
|                |                         |                         |
|                | OK                      |                         |
+----------------+-------------------------+-------------------------+
| **Parameters** | <SSL mode>: a value                               |
|                | from -3 representing 2                            |
|                | bits used to configure                            |
|                | the SSL as described                              |
|                | below:                                            |
|                |                                                   |
|                | -  Bit：if set to 1,    |                         |
|                |    certificate and                                |
|                |    private key will be                            |
|                |    enabled, so SSL                                |
|                |    server can verify                              |
|                |    BFQ4004; if 0, then                            |
|                |    certificate and                                |
|                |    private key will not                           |
|                |    be enable.                                     |
|                |                                                   |
|                | -  bit1：if set to 1,   |                         |
|                |    CA will be enabled,                            |
|                |    so BFQ4004 can                                 |
|                |    verify SSL server;                             |
|                |    if 0, CA will not be                           |
|                |    enabled.                                       |
|                |                                                   |
|                | (Looks like ESP8266 can                           |
|                | also do mutual SSL                                |
|                | according to the above                            |
|                | 2-bit settings? What                              |
|                | should be added to                                |
|                | cover mutual SSL                                  |
|                | feature BFQ4004                                   |
|                | provides?)                                        |
+----------------+-------------------------+-------------------------+
| **Notes**      | -  If certificates need                           |
|                |    to be enabled,                                 |
|                |    please call this                               |
|                |    command before SSL                             |
|                |    connection is                                  |
|                |    established.                                   |
|                |                                                   |
|                | -  If certificates need                           |
|                |    to be enabled,                                 |
|                |    please refer to the                            |
|                |    BFQ4004 SSL User                               |
|                |    Guide to generate                              |
|                |    certificates.                                  |
|                |                                                   |
|                |    -  esp_ca_cert.bin                             |
|                |       downloads to                                |
|                |       0xFB000 by                                  |
|                |       default                                     |
|                |                                                   |
|                |    -  e                                           |
|                | sp_cert_private_key.bin                           |
|                |       downloads to                                |
|                |       0xFC000 by                                  |
|                |       default                                     |
|                |                                                   |
|                |    -  Users can revise                            |
|                |       the                                         |
|                |       SYSTEM_PARTI                                |
|                | TION_SSL_CLIENT_CA_ADDR                           |
|                |       and                                         |
|                |                                                   |
|                |  SYSTEM_PARTITION_SSL_C                           |
|                | LIENT_CERT_PRIVKEY_ADDR                           |
|                |       in user_main.c to                           |
|                |       change the                                  |
|                |       downloading                                 |
|                |       addresses.                                  |
|                |                                                   |
|                | This configuration will                           |
|                | be saved in the user                              |
|                | parameter area of the                             |
|                | flash.                                            |
+----------------+-------------------------+-------------------------+
| **Examples**   | AT+CWMODE=1 // enable                             |
|                | sta mode                                          |
|                |                                                   |
|                | AT+                                               |
|                | CWJAP="SSID","PASSWORD"                           |
|                | // connect to an AP                               |
|                |                                                   |
|                | AT+CIPSNTPCFG=1,8 //                              |
|                | set SNTP time zone                                |
|                |                                                   |
|                | AT+CIPSNTPTIME? // get                            |
|                | SNTP time                                         |
|                |                                                   |
|                | AT+CIPSSLCCONF=2                                  |
|                |                                                   |
|                | AT+CIPSTART="S                                    |
|                | SL","192.168.3.38",8443                           |
+----------------+-------------------------+-------------------------+

AT+CIPSEND – Sends Data
~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-------------------------+
| **Command**    | Set Command:            | Execute Command:        |
|                |                         |                         |
|                | 1. Single connection:   | AT+CIPSEND              |
|                |    (+CIPMUX=)           |                         |
|                |                         | Function: to start      |
|                | AT+CIPSEND=<length>     | sending data in         |
|                |                         | transparent             |
|                | 2. Multiple             | transmission mode.      |
|                |    connections:         |                         |
|                |    (+CIPMUX=1)          |                         |
|                |                         |                         |
|                | AT+CIP                  |                         |
|                | SEND=<link_ID>,<length> |                         |
|                |                         |                         |
|                | 3. Remote IP and ports  |                         |
|                |    can be optionally    |                         |
|                |    set in UDP           |                         |
|                |    transmission:        |                         |
|                |                         |                         |
|                | |                       |                         |
|                | AT+CIPSEND=[<link_ID>,] |                         |
|                | | <length>              |                         |
|                |   [,<remote_IP>,        |                         |
|                | | <remote_port>]        |                         |
|                |                         |                         |
|                | Function: to configure  |                         |
|                | the data length in      |                         |
|                | normal transmission     |                         |
|                | mode.                   |                         |
+----------------+-------------------------+-------------------------+
| **Response**   | Send data of designated | Wrap return > after     |
|                | length.                 | executing this command. |
|                |                         |                         |
|                | Wrap return > after the | Enter transparent       |
|                | Set Command. Begin      | transmission, with a    |
|                | receiving serial data.  | 20-ms interval between  |
|                | When data length        | each packet, and a      |
|                | defined by              | maximum of 248 bytes    |
|                |                         | per packet.             |
|                | <length> is met, the    |                         |
|                | transmission of data    | When a single packet    |
|                | starts.                 | containing +++ is       |
|                |                         | received, BFQ4004       |
|                | If the connection       | returns to normal       |
|                | cannot be established   | command mode.           |
|                | or gets disrupted       |                         |
|                | during data             | Please wait for at      |
|                | transmission, the       | least one second before |
|                | system returns:         | sending the next AT     |
|                |                         | command.                |
|                | ERROR                   |                         |
|                |                         | This command can only   |
|                | If data is transmitted  | be used in transparent  |
|                | successfully, the       | transmission mode which |
|                | system returns:         | requires single         |
|                |                         | connection.             |
|                | SEND OK                 |                         |
|                |                         | For UDP transparent     |
|                | If it failed, the       | transmission, the value |
|                | system returns:         | of<UDP_mode> has to be  |
|                |                         | when using AT+CIPSTART. |
|                | SEND FAIL               |                         |
+----------------+-------------------------+-------------------------+
| **Parameters** | -  <link_ID>: ID of the | \-                      |
|                |       connection (~4),  |                         |
|                |       for multiple      |                         |
|                |       connections.      |                         |
|                |                         |                         |
|                | -  <length>: data       |                         |
|                |       length, MAX: 248  |                         |
|                |       bytes.            |                         |
|                |                         |                         |
|                | -  [<remote_IP>]:       |                         |
|                |       optional; remote  |                         |
|                |       IP address that   |                         |
|                |       can be set for    |                         |
|                |       UDP transmission. |                         |
|                |                         |                         |
|                | -  [<remote_port>]:     |                         |
|                |       optional; remote  |                         |
|                |       port that can be  |                         |
|                |       set for UDP       |                         |
|                |       transmission.     |                         |
+----------------+-------------------------+-------------------------+
| **Examples**   | AT+CIPSEND=124 //                                 |
|                | +CIPMUX=                                          |
|                |                                                   |
|                | AT+CIPSEND=2,124 //                               |
|                | +CIPMUX=1                                         |
+----------------+-------------------------+-------------------------+

AT+CIPSENDEX – Sends Data
~~~~~~~~~~~~~~~~~~~~~~~~~

+-----------------+---------------------------------------------------+
| **Set Command** | 1. Single connection: (+CIPMUX=)                  |
|                 |                                                   |
|                 | AT+CIPSENDEX=<length>                             |
|                 |                                                   |
|                 | 2. Multiple connections: (+CIPMUX=1)              |
|                 |                                                   |
|                 | AT+CIPSENDEX=<link_ID>,<length>                   |
|                 |                                                   |
|                 | 3. Remote IP and ports can be set in UDP          |
|                 |    transmission:                                  |
|                 |                                                   |
|                 | ..                                                |
|                 |                                                   |
|                 |    AT+CIPSENDEX                                   |
|                 | =[<link_ID>,]<length>[,<remote_IP>,<remote_port>] |
|                 |                                                   |
|                 | Function: to configure the data length in normal  |
|                 | transmission mode.                                |
+-----------------+---------------------------------------------------+
| **Response**    | Send data of designated length.                   |
|                 |                                                   |
|                 | Wrap return > after the Set Command. Begin        |
|                 | receiving serial data. When the requirement of    |
|                 | data length, determined by <length>, is met, or   |
|                 | when \\ appears in the data, the transmission     |
|                 | starts.                                           |
|                 |                                                   |
|                 | If connection cannot be established or gets       |
|                 | disconnected during transmission, the system      |
|                 | returns:                                          |
|                 |                                                   |
|                 | ERROR                                             |
|                 |                                                   |
|                 | If data are successfully transmitted, the system  |
|                 | returns:                                          |
|                 |                                                   |
|                 | SEND OK                                           |
|                 |                                                   |
|                 | If it failed, the system returns:                 |
|                 |                                                   |
|                 | SEND FAIL                                         |
+-----------------+---------------------------------------------------+
| **Parameters**  | -  <link_ID>: ID of the connection (~4), for      |
|                 |    multiple connections.                          |
|                 |                                                   |
|                 | -  <length>: data length, MAX: 248 bytes.         |
|                 |                                                   |
|                 | -  When the requirement of data length,           |
|                 |    determined by <length>, is met, or when \\     |
|                 |    appears, the transmission of data starts. Go   |
|                 |    back to the normal command mode and wait for   |
|                 |    the next AT command.                           |
|                 |                                                   |
|                 | -  When sending \\, please send it as \\\.        |
+-----------------+---------------------------------------------------+

AT+CIPSENDBUF – Writes Data Into the TCP-Send-Buffer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-----------------+---------------------------------------------------+
| **Set Command** | 1. Single connection: (+CIPMUX=)                  |
|                 |                                                   |
|                 | ..                                                |
|                 |                                                   |
|                 |    AT+CIPSENDBUF=<length>                         |
|                 |                                                   |
|                 | 2. Multiple connections: (+CIPMUX=1)              |
|                 |                                                   |
|                 | ..                                                |
|                 |                                                   |
|                 |    AT+CIPSENDBUF=<link_ID>,<length>               |
+-----------------+---------------------------------------------------+
| **Response**    |    <current segment_ID>,<segment_ID of which sent |
|                 |    successfully>                                  |
|                 |                                                   |
|                 |    OK                                             |
|                 |                                                   |
|                 |    >                                              |
|                 |                                                   |
|                 | -  Wrap return > begins receiving serial data;    |
|                 |    when the length of data defined by the         |
|                 |    parameter <length> is met, the data is sent;   |
|                 |    if the data length over the value of <length>, |
|                 |    the data will be discarded, and the command    |
|                 |    returns busy.                                  |
|                 |                                                   |
|                 | -  If the connection cannot be established, or if |
|                 |    it is not a TCP connection, or if the buffer   |
|                 |    is full, or some other error occurs, the       |
|                 |    command returns                                |
|                 |                                                   |
|                 | ..                                                |
|                 |                                                   |
|                 |    ERROR                                          |
|                 |                                                   |
|                 | -  If data is transmitted successfully,           |
|                 |                                                   |
|                 |    -  for single connection, the response is:     |
|                 |                                                   |
|                 | ..                                                |
|                 |                                                   |
|                 |    <segment_ID>,SEND OK                           |
|                 |                                                   |
|                 | -  for multiple connections, the response is:     |
|                 |                                                   |
|                 | ..                                                |
|                 |                                                   |
|                 |    <link_ID>,<segment_ID>,SEND OK                 |
|                 |                                                   |
|                 | -  If it failed, the system returns:              |
|                 |                                                   |
|                 | ..                                                |
|                 |                                                   |
|                 |    SEND FAIL                                      |
+-----------------+---------------------------------------------------+
| **Parameters**  | -  <link_ID>: ID of the connection (~4), for      |
|                 |    multiple connections.                          |
|                 |                                                   |
|                 | -  <segment_ID>: uint32; the ID assigned to each  |
|                 |    data packet, starting from 1; the ID number    |
|                 |    increases by 1 every time a data packet is     |
|                 |    written into the buffer.                       |
|                 |                                                   |
|                 | -  <length>: data length, MAX: 248 bytes.         |
+-----------------+---------------------------------------------------+
| **Notes**       | -  This command only writes data into the         |
|                 |    TCP-send-buffer, so it can be called           |
|                 |    continually, and the user need not wait for    |
|                 |    SEND OK; if a TCP segment is sent              |
|                 |    successfully, it will return <segment ID>,SEND |
|                 |    OK.                                            |
|                 |                                                   |
|                 | -  Before data length reaches the value defined   |
|                 |    by <length>, input +++ can switch back from    |
|                 |    data mode to command mode, and discard the     |
|                 |    data received before.                          |
|                 |                                                   |
|                 | -  This command can NOT be used for SSL           |
|                 |    connections.                                   |
+-----------------+---------------------------------------------------+

AT+BUFRESET – Resets the Segment ID Count
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-----------------+---------------------------------------------------+
| **Set Command** | 1. Single connection: (+CIPMUX=)                  |
|                 |                                                   |
|                 | ..                                                |
|                 |                                                   |
|                 |    AT+CIPBUFRESET                                 |
|                 |                                                   |
|                 | 2. Multiple connections: (+CIPMUX=1)              |
|                 |                                                   |
|                 | ..                                                |
|                 |                                                   |
|                 |    AT+CIPBUFRESET=<link_ID>                       |
+-----------------+---------------------------------------------------+
| **Response**    | OK                                                |
|                 |                                                   |
|                 | If the connection is not established or there is  |
|                 | still TCP data waiting to be sent, the response   |
|                 | will be:                                          |
|                 |                                                   |
|                 | ERROR                                             |
+-----------------+---------------------------------------------------+
| **Parameters**  | <link_ID>: ID of the connection (~4), for         |
|                 | multiple connections.                             |
+-----------------+---------------------------------------------------+
| **Notes**       | This command can only be used when AT+CIPSENDBUF  |
|                 | is used.                                          |
+-----------------+---------------------------------------------------+

AT+CIPBUFSTATUS – Checks the Status of the TCP-Send-Buffer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-----------------+---------------------------------------------------+
| **Set Command** | 1. Single connection: (+CIPMUX=)                  |
|                 |                                                   |
|                 | ..                                                |
|                 |                                                   |
|                 |    AT+CIPBUFSTATUS                                |
|                 |                                                   |
|                 | 2. Multiple connections: (+CIPMUX=1)              |
|                 |                                                   |
|                 | ..                                                |
|                 |                                                   |
|                 |    AT+CIPBUFSTATUS=<link_ID>                      |
+-----------------+---------------------------------------------------+
| **Response**    | <next segment_ID>,<segment_ID sent >,<segment_ID  |
|                 | successfully                                      |
|                 | sent>,<remain_buffer_size>,<queue_number>         |
|                 |                                                   |
|                 | OK                                                |
+-----------------+---------------------------------------------------+
| **Parameters**  | -  <next segment_ID>: the next segment ID         |
|                 |    obtained by AT+CIPSENDBUF;                     |
|                 |                                                   |
|                 | -  <segment_ID sent>: the ID of the TCP segment   |
|                 |    last sent;                                     |
|                 |                                                   |
|                 | -  Only when <next segment_ID> - <segment_ID      |
|                 |    sent> = 1, can AT+CIPBUFRESET be called to     |
|                 |    reset the count.                               |
|                 |                                                   |
|                 | -  <segment_ID successfully sent>: the ID of the  |
|                 |    last successfully sent TCP segment;            |
|                 |                                                   |
|                 | -  <remain_buffer_size>: the remaining size of    |
|                 |    the TCP-send-buffer in bytes;                  |
|                 |                                                   |
|                 | -  <queue_number>: available TCP queue number;    |
|                 |    it’s not reliable and should be used as a      |
|                 |    reference only.                                |
+-----------------+---------------------------------------------------+
| **Notes**       | This command can NOT be used for SSL connection.  |
+-----------------+---------------------------------------------------+
| **Examples**    | For example, in single connection, the command    |
|                 | AT+CIPBUFSTATUS returns:                          |
|                 |                                                   |
|                 | 2,15,1,2,7                                        |
|                 |                                                   |
|                 | Description:                                      |
|                 |                                                   |
|                 | -  2: means that the latest segment ID is 19; so  |
|                 |    when calling AT+CIPSENDBUF the next time, the  |
|                 |    segment ID returned is 20;                     |
|                 |                                                   |
|                 | -  15: means that the TCP segment with the ID 15  |
|                 |    is the last segment sent, but the segment may  |
|                 |    not be successfully sent;                      |
|                 |                                                   |
|                 | -  1: means that the TCP segment with the ID 1    |
|                 |    was sent successfully;                         |
|                 |                                                   |
|                 | -  2: means that the remaining size of the        |
|                 |    TCP-send-buffer is 2 bytes;                    |
|                 |                                                   |
|                 | -  7: the available TCP queue number; it is not   |
|                 |    reliable and should be used as a reference     |
|                 |    only; when the queue number is , no TCP data   |
|                 |    can be sent.                                   |
+-----------------+---------------------------------------------------+

AT+CIPCHECKSEQ – Checks If a Specific Segment Was Successfully Sent
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-----------------+---------------------------------------------------+
| **Set Command** | 1. Single connection: (+CIPMUX=)                  |
|                 |                                                   |
|                 | ..                                                |
|                 |                                                   |
|                 |    AT+CIPCHECKSEQ=<segment_ID>                    |
|                 |                                                   |
|                 | 2. Multiple connections: (+CIPMUX=1)              |
|                 |                                                   |
|                 | ..                                                |
|                 |                                                   |
|                 |    AT+CIPCHECKSEQ=<link_ID>,<segment_ID>          |
+-----------------+---------------------------------------------------+
| **Response**    | [<link ID>,]<segment_ID>,<status>                 |
|                 |                                                   |
|                 | OK                                                |
+-----------------+---------------------------------------------------+
| **Parameters**  | -  The command can only be used to check the      |
|                 |    status of the last 32 segments sent.           |
|                 |                                                   |
|                 | -  [<link_ID>]: ID of the connection (~4), for    |
|                 |    multiple connection;                           |
|                 |                                                   |
|                 | -  <segment_ID>: the segment ID obtained by       |
|                 |    calling AT+CIPSENDBUF;                         |
|                 |                                                   |
|                 | -  <status>:                                      |
|                 |                                                   |
|                 |    -  FALSE: the segment sending failed;          |
|                 |                                                   |
|                 |    -  TRUE: the segment was sent successfully.    |
+-----------------+---------------------------------------------------+
| **Notes**       | This command can only be used when AT+CIPSENDBUF  |
|                 | is used.                                          |
+-----------------+---------------------------------------------------+

AT+CIPCLOSE – Closes the TCP/UDP/SSL Connection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-------------------------+
| **Command**    | Set Command: (used in   | Execute Command: (used  |
|                | multiple connections)   | in multiple             |
|                |                         | connections)            |
|                | AT+CIPCLOSE=<link_ID>   |                         |
|                |                         | AT+CIPCLOSE             |
|                | Function: to close the  |                         |
|                | particular link_ID      | Function: to close all  |
|                | TCP/UDP connection.     | TCP/UDP connections.    |
+----------------+-------------------------+-------------------------+
| **Response**   | OK                                                |
+----------------+-------------------------+-------------------------+
| **Parameters** | <link_ID>: ID of the    | \-                      |
|                | connection to be        |                         |
|                | closed. When ID is 5,   |                         |
|                | all connections will be |                         |
|                | closed. In server mode, |                         |
|                | ID=5 has no effect.     |                         |
+----------------+-------------------------+-------------------------+
| **Examples**   | AT+CIPSEND=124 //                                 |
|                | +CIPMUX=                                          |
|                |                                                   |
|                | AT+CIPSEND=2,124 //                               |
|                | +CIPMUX=1                                         |
+----------------+-------------------------+-------------------------+

AT+CIFSR – Gets the Local IP Address
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+---------------------+-----------------------------------------------+
| **Execute Command** | AT+CIFSR                                      |
+---------------------+-----------------------------------------------+
| **Response**        | +CIFSR:APIP,<SoftAP_IP>                       |
|                     |                                               |
|                     | +CIFSR:APMAC,<SoftAP_MAC>                     |
|                     |                                               |
|                     | +CIFSR:STAIP,<Station_IP>                     |
|                     |                                               |
|                     | +CIFSR:STAMAC,<Station_MAC>                   |
|                     |                                               |
|                     | OK                                            |
+---------------------+-----------------------------------------------+
| **Parameters**      | <SoftAP_IP>: IP address of the BFQ4004        |
|                     | SoftAP.                                       |
|                     |                                               |
|                     | <Station_IP>: IP address of the BFQ4004       |
|                     | Station.                                      |
|                     |                                               |
|                     | <SoftAP_MAC>: MAC address of the BFQ4004      |
|                     | SoftAP.                                       |
|                     |                                               |
|                     | <Station_MAC>: MAC address of the BFQ4004     |
|                     | Station.                                      |
+---------------------+-----------------------------------------------+
| **Notes**           | Only when the BFQ4004 Station is connected to |
|                     | an AP can its Station IP can be queried.      |
+---------------------+-----------------------------------------------+

AT+CIPMUX – Enables or Disables Multiple Connections
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-------------------------+
| **Command**    | Query Command:          | Set Command:            |
|                |                         |                         |
|                | AT+CIPMUX?              | AT+CIPMUX=< mode>       |
|                |                         |                         |
|                | Function: checks the    | Function: sets the      |
|                | connection mode.        | connection mode.        |
+----------------+-------------------------+-------------------------+
| **Response**   | +CIPMUX:< mode>         | OK                      |
|                |                         |                         |
|                | OK                      |                         |
+----------------+-------------------------+-------------------------+
| **Parameters** | <mode>:                                           |
|                |                                                   |
|                | -  ：single connection. |                         |
|                |                                                   |
|                | -  1：multiple          |                         |
|                |    connections.                                   |
+----------------+-------------------------+-------------------------+
| **Notes**      | -  The default mode is                            |
|                |    single connection.                             |
|                |                                                   |
|                | -  Multiple connections                           |
|                |    can only be set when                           |
|                |    transparent                                    |
|                |    transmission is                                |
|                |    disabled                                       |
|                |    (AT+CIPMODE=).                                 |
|                |                                                   |
|                | -  This mode can only                             |
|                |    be changed after all                           |
|                |    connections are                                |
|                |    disconnected.                                  |
|                |                                                   |
|                | -  If the TCP server is                           |
|                |    running, it must be                            |
|                |    deleted                                        |
|                |    (AT+CIPSERVER=)                                |
|                |    before the single                              |
|                |    connection mode is                             |
|                |    activated.                                     |
+----------------+-------------------------+-------------------------+
| **Examples**   | AT+CIPMUX=1                                       |
+----------------+-------------------------+-------------------------+

AT+CIPSERVER – Creates or Deletes TCP Server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-----------------+---------------------------------------------------+
| **Set Command** | AT+CIPSERVER=<mode>[,<port>]                      |
+-----------------+---------------------------------------------------+
| **Response**    | OK                                                |
+-----------------+---------------------------------------------------+
| **Parameters**  | -  <mode>:                                        |
|                 |                                                   |
|                 |    -  : deletes server.                           |
|                 |                                                   |
|                 |    -  1: creates server.                          |
|                 |                                                   |
|                 | -  <port>: port number; 333 by default.           |
+-----------------+---------------------------------------------------+
| **Notes**       | -  A TCP server can only be created when multiple |
|                 |    connections are activated (AT+CIPMUX=1).       |
|                 |                                                   |
|                 | -  A server monitor will automatically be created |
|                 |    when the TCP server is created.                |
|                 |                                                   |
|                 | -  When a client is connected to the server, it   |
|                 |    will take up one connection and be assigned an |
|                 |    ID.                                            |
+-----------------+---------------------------------------------------+
| **Examples**    | AT+CIPMUX=1                                       |
|                 |                                                   |
|                 | AT+CIPSERVER=1,11                                 |
+-----------------+---------------------------------------------------+

AT+CIPSERVERMAXCONN – Sets the Maximum Connections Allowed by Server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-------------------------+
| **Command**    | Query Command:          | Set Command:            |
|                |                         |                         |
|                | AT+CIPSERVERMAXCONN?    | AT+CIPSERVERMAXCONN=<   |
|                |                         | num>                    |
|                | Function: obtains the   |                         |
|                | maximum number of       | Function: sets the      |
|                | clients allowed to      | maximum number of       |
|                | connect to the TCP or   | clients allowed to      |
|                | SSL server.             | connect to the TCP or   |
|                |                         | SSL server.             |
+----------------+-------------------------+-------------------------+
| **Response**   | +CIPSERVERMAXCONN:<     | OK                      |
|                | num>                    |                         |
|                |                         |                         |
|                | OK                      |                         |
+----------------+-------------------------+-------------------------+
| **Parameters** | <num>: the maximum                                |
|                | number of clients                                 |
|                | allowed to connect to                             |
|                | the TCP or SSL server,                            |
|                | range:[1~5].                                      |
+----------------+-------------------------+-------------------------+
| **Notes**      | AT                                                |
|                | +CIPSERVERMAXCONN=<num>                           |
|                | should be used to set                             |
|                | up the correct                                    |
|                | configuration before                              |
|                | creating a server.                                |
+----------------+-------------------------+-------------------------+
| **Examples**   | AT+CIPMUX=1                                       |
|                |                                                   |
|                | AT+CIPSERVERMAXCONN=2                             |
|                |                                                   |
|                | AT+CIPSERVER=1,8                                  |
+----------------+-------------------------+-------------------------+

AT+CIPMODE – Sets Transmission Mode
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-------------------------+
| **Command**    | Query Command:          | Set Command:            |
|                |                         |                         |
|                | AT+CIPMODE?             | AT+CIPMODE=< mode>      |
|                |                         |                         |
|                | Function: checks the    | Function: sets the      |
|                | transmission mode.      | transmission mode.      |
+----------------+-------------------------+-------------------------+
| **Response**   | +CIPMODE:< mode>        | OK                      |
|                |                         |                         |
|                | OK                      |                         |
+----------------+-------------------------+-------------------------+
| **Parameters** | <mode>:                                           |
|                |                                                   |
|                | -  : normal                                       |
|                |    transmission mode.                             |
|                |                                                   |
|                | -  1: UART-Wi-Fi                                  |
|                |    passthrough mode                               |
|                |    (transparent                                   |
|                |    transmission), which                           |
|                |    can only be enabled                            |
|                |    in TCP single                                  |
|                |    connection mode or                             |
|                |    in UDP mode when the                           |
|                |    remote IP and port                             |
|                |    do not change.                                 |
+----------------+-------------------------+-------------------------+
| **Notes**      | -  The configuration                              |
|                |    changes will NOT be                            |
|                |    saved in flash.                                |
|                |                                                   |
|                | -  During the                                     |
|                |    UART-Wi-Fi                                     |
|                |    passthrough                                    |
|                |    transmission, if the                           |
|                |    TCP connection                                 |
|                |    breaks, BFQ4004 will                           |
|                |    keep trying to                                 |
|                |    reconnect until +++                            |
|                |    is inputted to exit                            |
|                |    the transmission.                              |
|                |                                                   |
|                | -  If it is a normal                              |
|                |    TCP transmission and                           |
|                |    the TCP connection                             |
|                |    breaks, BFQ4004 will                           |
|                |    give a prompt and                              |
|                |    will not attempt to                            |
|                |    reconnect.                                     |
+----------------+-------------------------+-------------------------+
| **Examples**   | AT+CIPMODE=1                                      |
+----------------+-------------------------+-------------------------+

AT+CIPSTO – Sets the TCP Server Timeout
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-------------------------+
| **Command**    | Query Command:          | Set Command:            |
|                |                         |                         |
|                | AT+CIPSTO?              | AT+CIPSTO=< time>       |
|                |                         |                         |
|                | Function: checks the    | Function: sets the TCP  |
|                | TCP server timeout      | server timeout.         |
|                | setting.                |                         |
+----------------+-------------------------+-------------------------+
| **Response**   | +CIPSTO:< time>         | OK                      |
|                |                         |                         |
|                | OK                      |                         |
+----------------+-------------------------+-------------------------+
| **Parameters** | <time>: TCP server                                |
|                | timeout duration,                                 |
|                | range: ~72 seconds (s).                           |
+----------------+-------------------------+-------------------------+
| **Notes**      | -  BFQ4004 configured                             |
|                |    as a TCP server will                           |
|                |    disconnect from the                            |
|                |    TCP client that has                            |
|                |    not communicated                               |
|                |    with it for a                                  |
|                |    duration equal to                              |
|                |    the <time> set.                                |
|                |                                                   |
|                | -  If AT+CIPSTO=, the                             |
|                |    connection will                                |
|                |    never time out. This                           |
|                |    configuration is not                           |
|                |    recommended.                                   |
+----------------+-------------------------+-------------------------+
| **Examples**   | AT+CIPMUX=1                                       |
|                |                                                   |
|                | AT+CIPSERVER=1,11                                 |
|                |                                                   |
|                | AT+CIPSTO=1                                       |
+----------------+-------------------------+-------------------------+

AT+PING – Pings Packets
~~~~~~~~~~~~~~~~~~~~~~~

+-----------------+---------------------------------------------------+
| **Set Command** | AT+PING=<IP>                                      |
|                 |                                                   |
|                 | Function: ping packets.                           |
+-----------------+---------------------------------------------------+
| **Response**    | +<time>                                           |
|                 |                                                   |
|                 | OK                                                |
|                 |                                                   |
|                 | or                                                |
|                 |                                                   |
|                 | +timeout                                          |
|                 |                                                   |
|                 | ERROR                                             |
+-----------------+---------------------------------------------------+
| **Parameters**  | -  <IP>: string representing host IP address or   |
|                 |       domain name.                                |
|                 |                                                   |
|                 | -  <time>: the response time of ping.             |
+-----------------+---------------------------------------------------+
| **Examples**    | AT+PING="192.168.1.1"                             |
|                 |                                                   |
|                 | AT+PING="www.beefi.io"                            |
+-----------------+---------------------------------------------------+

AT+CIUPDATE – Updates the Software Through Wi-Fi
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+---------------------+-----------------------------------------------+
| **Execute Command** | AT+CIUPDATE                                   |
|                     |                                               |
|                     | Function: updates software.                   |
+---------------------+-----------------------------------------------+
| **Response**        | +CIUPDATE:<action>                            |
|                     |                                               |
|                     | OK                                            |
+---------------------+-----------------------------------------------+
| **Parameters**      | <action>:                                     |
|                     |                                               |
|                     | -  1: find the server.                        |
|                     |                                               |
|                     | -  2: connect to server.                      |
|                     |                                               |
|                     | -  3: get the software version.               |
|                     |                                               |
|                     | -  4: start updating.                         |
+---------------------+-----------------------------------------------+
| **Notes**           | -  The speed of the upgrade depends on the    |
|                     |    connection quality of the network.         |
|                     |                                               |
|                     | -  ERROR will be returned if the upgrade      |
|                     |    fails due to unfavorable network           |
|                     |    conditions. Please wait for some time      |
|                     |    before retrying.                           |
|                     |                                               |
|                     | -  If using BeeFi’s AT BIN (/BFQ4004/bin/at), |
|                     |    AT+CIUPDATE will download a new AT BIN     |
|                     |    from the BeeFi Cloud.                      |
|                     |                                               |
|                     | -  If using a user-compiled AT BIN, users     |
|                     |    need to make their own AT+CIUPDATE         |
|                     |    upgrade. BeeFi provides a demo as a        |
|                     |    reference for local upgrade (see:          |
|                     |    /BFQ4004/example/at\ *)*.                  |
|                     |                                               |
|                     | -  It is suggested that users call AT+RESTORE |
|                     |    to restore the factory default AT settings |
|                     |    after upgrading the AT firmware.           |
+---------------------+-----------------------------------------------+

AT+CIPDINFO – Shows the Remote IP and Port with +IPD
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-----------------+---------------------------------------------------+
| **Set Command** | AT+CIPDINFO=<mode>                                |
|                 |                                                   |
|                 | Function: sets whether to show remote IP and port |
|                 | with +IPD.                                        |
+-----------------+---------------------------------------------------+
| **Response**    | OK                                                |
+-----------------+---------------------------------------------------+
| **Parameters**  | <mode>:                                           |
|                 |                                                   |
|                 | -  : does not show the remote IP and port with    |
|                 |    +IPD.                                          |
|                 |                                                   |
|                 | -  1: shows the remote IP and port with +IPD.     |
+-----------------+---------------------------------------------------+
| **Examples**    | AT+CIPDINFO=1                                     |
+-----------------+---------------------------------------------------+

+IPD – Receives Network Data
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-------------------------+
| **Command**    | Single connection:      | Multiple connection:    |
|                |                         |                         |
|                | (+CIPMUX=)+IPD,<len>    | (+CIPMU                 |
|                |                         | X=)+IPD,<link_ID>,<len> |
|                | [,<rem                  |                         |
|                | ote_IP>,<remote_port>]: | [,<rem                  |
|                |                         | ote_IP>,<remote_port>]: |
|                | <data>                  |                         |
|                |                         | <data>                  |
+----------------+-------------------------+-------------------------+
| **Parameters** |    The command is valid                           |
|                |    in normal command                              |
|                |    mode. When the                                 |
|                |    module receives                                |
|                |    network data, it                               |
|                |    will send the data                             |
|                |    through the serial                             |
|                |    port using the +IPD                            |
|                |    command.                                       |
|                |                                                   |
|                | -  [<remote_IP>]:                                 |
|                |    remote IP, enabled                             |
|                |    by command                                     |
|                |    AT+CIPDINFO=1.                                 |
|                |                                                   |
|                | -  [<remote_port>]:                               |
|                |    remote port, enabled                           |
|                |    by command                                     |
|                |    AT+CIPDINFO=1.                                 |
|                |                                                   |
|                | -  <link_ID>: ID number                           |
|                |    of connection.                                 |
|                |                                                   |
|                | -  <len>: data length.                            |
|                |                                                   |
|                | -  <data>: data                                   |
|                |    received.                                      |
+----------------+-------------------------+-------------------------+

AT+CIPRECVMODE – Sets TCP Receive Mode
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-------------------------+
| **Command**    | Query Command:          | Set Command:            |
|                |                         |                         |
|                | AT+CIPRECVMODE?         | AT+CIPRECVMODE=<mode>   |
|                |                         |                         |
|                | Function: checks the    | Function: sets the      |
|                | receive mode of TCP     | receive mode of TCP     |
|                | data.                   | data.                   |
+----------------+-------------------------+-------------------------+
| **Response**   | +CIPRECVMODE:<mode>     | OK                      |
|                |                         |                         |
|                | OK                      |                         |
+----------------+-------------------------+-------------------------+
| **Parameters** | <mode>: the receive                               |
|                | mode of TCP data.                                 |
|                |                                                   |
|                | -  : active mode                                  |
|                |    (default) – BFQ4004                            |
|                |    will send all the                              |
|                |    received TCP data                              |
|                |    instantly to host                              |
|                |    MCU through UART                               |
|                |    with header “+IPD".                            |
|                |                                                   |
|                | -  1: passive mode –                              |
|                |    BFQ4004 will keep                              |
|                |    the received TCP                               |
|                |    data in an internal                            |
|                |    buffer (default is                             |
|                |    292 bytes), and wait                           |
|                |    for host MCU to read                           |
|                |    the data. If the                               |
|                |    buffer is full, the                            |
|                |    TCP transmission                               |
|                |    will be blocked.                               |
+----------------+-------------------------+-------------------------+
| **Notes**      | -  The configuration is                           |
|                |    for normal TCP                                 |
|                |    transmission only,                             |
|                |    and cannot be used                             |
|                |    on SSL, UDP or WiFi-                           |
|                |    UART passthrough                               |
|                |    modes.                                         |
|                |                                                   |
|                | -  If the passive mode                            |
|                |    is enabled, when                               |
|                |    BFQ4004 receives TCP                           |
|                |    data, it will prompt                           |
|                |    the following                                  |
|                |    message in different                           |
|                |    scenarios:                                     |
|                |                                                   |
|                | -  For multiple                                   |
|                |    connection mode                                |
|                |    (AT+CIPMUX=1), the                             |
|                |    message is:                                    |
|                |    +IPD,<link_ID>,<len>                           |
|                |                                                   |
|                | -  For single                                     |
|                |    connection mode                                |
|                |    (AT+CIPMUX=), the                              |
|                |    message is:                                    |
|                |    +IPD,<len>                                     |
|                |                                                   |
|                | -  <len> is the total                             |
|                |    length of TCP data                             |
|                |    in buffer                                      |
+----------------+-------------------------+-------------------------+
| **Examples**   | AT+CIPRECVMODE=1                                  |
+----------------+-------------------------+-------------------------+

AT+CIPRECVDATA – Gets TCP Data In Passive Receive Mode
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-----------------+------------------------+------------------------+
| **Set Command** | Single connection mode | Multiple connections   |
|                 |                        | mode                   |
|                 | (AT+CIPMUX=):          |                        |
|                 |                        | (AT+CIPMUX=1):         |
|                 | AT+CIPRECVDATA=<len>   |                        |
|                 |                        | AT+CIPRE               |
|                 |                        | CVDATA=<link_ID>,<len> |
+-----------------+------------------------+------------------------+
| **Response**    | +CIPRECVDAT                                     |
|                 | A:<actual_leng>,<data>                          |
|                 |                                                 |
|                 | OK                                              |
+-----------------+------------------------+------------------------+
| **Parameters**  | -  <link_ID>:                                   |
|                 |    connection ID in                             |
|                 |    multiple connection                          |
|                 |    mode.                                        |
|                 |                                                 |
|                 | -  <len>: data length                           |
|                 |    requested, max is                            |
|                 |    248 bytes for each                           |
|                 |    request.                                     |
|                 |                                                 |
|                 | -  <actual_len>:                                |
|                 |    length of the data                           |
|                 |    actually received                            |
|                 |                                                 |
|                 | -  <data>: the data                             |
|                 |    received                                     |
+-----------------+------------------------+------------------------+
| **Notes**       | In case of                                      |
|                 | disconnection, the                              |
|                 | buffered TCP data will                          |
|                 | still be there and can                          |
|                 | be read by MCU until a                          |
|                 | new connection is                               |
|                 | established. If the                             |
|                 | newly established                               |
|                 | connection happens to                           |
|                 | use the same link ID,                           |
|                 | the previously                                  |
|                 | buffered data in the                            |
|                 | last connection will                            |
|                 | be lost.                                        |
+-----------------+------------------------+------------------------+
| **Examples**    | AT+CIPRECVMODE=1                                |
|                 |                                                 |
|                 | // For example, if                              |
|                 | host MCU got a message                          |
|                 | of receiving 1 bytes                            |
|                 | data in connection                              |
|                 | with connection , the                           |
|                 | message will be as                              |
|                 | following: +IPD,,1                              |
|                 |                                                 |
|                 | // then you can read                            |
|                 | those 100 bytes by                              |
|                 | using the command                               |
|                 | below                                           |
|                 |                                                 |
|                 | AT+CIPRECVDATA=,1                               |
+-----------------+------------------------+------------------------+

AT+CIPREVLEN – Gets TCP Data Length in Passive Received Mode
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-------------------+-------------------------------------------------+
| **Query Command** | AT+CIPRECVLEN?                                  |
+-------------------+-------------------------------------------------+
| **Response**      | +CIPRECVLEN:<data length of link0>,<data length |
|                   | of link1>,<data length of link2>,<data length   |
|                   | of link3>,<data length of link4>                |
|                   |                                                 |
|                   | OK                                              |
+-------------------+-------------------------------------------------+
| **Parameters**    | <data length of link#>: length of the data      |
|                   | currently buffered for the particular link      |
|                   | number.                                         |
+-------------------+-------------------------------------------------+
| **Examples**      | AT+CIPRECVLEN?                                  |
|                   |                                                 |
|                   | +CIPRECVLEN:1,,,,                               |
|                   |                                                 |
|                   | OK                                              |
+-------------------+-------------------------------------------------+

AT+CIPSNTPCFG – Sets the Configuration of SNTP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-------------------------+
| **Command**    | Query Command:          | Set Command:            |
|                |                         |                         |
|                | AT+CIPSNTPCFG?          | AT+CIPSNTPCFG=<enable>  |
|                |                         |                         |
|                | Function: checks the    | [,<tim                  |
|                | SNTP configuration.     | ezone>][,<SNTP_server>, |
|                |                         |                         |
|                |                         | <SNTP_s                 |
|                |                         | erver1>,<SNTP_server2>] |
|                |                         |                         |
|                |                         | Function: sets the SNTP |
|                |                         | configuration.          |
+----------------+-------------------------+-------------------------+
| **Response**   | +CIPSNTPCFG:<enable>,   | OK                      |
|                |                         |                         |
|                | <                       |                         |
|                | timezone>,<SNTP_server> |                         |
|                |                         |                         |
|                | [,<SNTP_server1>,       |                         |
|                |                         |                         |
|                | <SNTP_server2>]         |                         |
|                |                         |                         |
|                | OK                      |                         |
+----------------+-------------------------+-------------------------+
| **Parameters** | -  <enable>:                                      |
|                |                                                   |
|                | -  : SNTP is disabled;                            |
|                |                                                   |
|                | -  1: SNTP is enabled.                            |
|                |                                                   |
|                | -  <timezone>: time                               |
|                |    zone; range:                                   |
|                |    [-11,13]; if SNTP is                           |
|                |    enabled, the                                   |
|                |    <timezone> must be                             |
|                |    set;                                           |
|                |                                                   |
|                | -  <SNTP server>:                                 |
|                |    optional parameter                             |
|                |    indicating the first                           |
|                |    SNTP server;                                   |
|                |                                                   |
|                | -  <SNTP server1>:                                |
|                |    optional parameter                             |
|                |    indicating the                                 |
|                |    second SNTP server;                            |
|                |                                                   |
|                | -  <SNTP server2>:                                |
|                |    optional parameter                             |
|                |    indicating the third                           |
|                |    SNTP server.                                   |
+----------------+-------------------------+-------------------------+
| **Notes**      | If the <SNTP server>                              |
|                | parameters are not set,                           |
|                | servers                                           |
|                | "cn.ntp.org                                       |
|                | .cn","ntp.sjtu.edu.cn",                           |
|                | and "us.pool.ntp.org"                             |
|                | (change to                                        |
|                | “0.pool.ntp.org”,                                 |
|                | “1.pool.ntp.org” and                              |
|                | “2.pool.ntp.org”?) will                           |
|                | be used by default.                               |
+----------------+-------------------------+-------------------------+
| **Examples**   | AT+CIPSNTPCFG=1,8,"0.p                            |
|                | ool.ntp.org","1.pool.nt                           |
|                | p.org","2.pool.ntp.org"                           |
+----------------+-------------------------+-------------------------+

AT+CIPSNTPTIME – Checks the SNTP Time
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-------------------+-------------------------------------------------+
| **Query Command** | AT+CIPSNTPTIME?                                 |
+-------------------+-------------------------------------------------+
| **Response**      | +CIPSNTPTIME:<time>                             |
|                   |                                                 |
|                   | OK                                              |
+-------------------+-------------------------------------------------+
| **Parameters**    | <time>: SNTP time                               |
|                   |                                                 |
|                   | OK                                              |
+-------------------+-------------------------------------------------+
| **Examples**      | AT+CWMODE=1 //set as station mode               |
|                   |                                                 |
|                   | AT+CWJAP="DemoAP","password" //connect to       |
|                   | router, access the internet                     |
|                   |                                                 |
|                   | AT+CIPSNTPCFG=1,8 //set time zone               |
|                   |                                                 |
|                   | AT+CIPSNTPTIME? //get time                      |
|                   |                                                 |
|                   | For example:                                    |
|                   |                                                 |
|                   | +CIPSNTPTIME:Thu Aug 04 14:48:05 2019           |
|                   |                                                 |
|                   | OK                                              |
+-------------------+-------------------------------------------------+

AT+CIPDNS_CUR – Sets User-defined DNS Servers, Configuration Not Saved to Flash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-------------------------+
| **Command**    | Query Command:          | Set Command:            |
|                |                         |                         |
|                | AT+CIPDNS_CUR?          | AT+CIPDNS_CUR=<enable>  |
|                |                         |                         |
|                | Function: gets the      | [,<DNS_server>,         |
|                | current DNS server.     |                         |
|                |                         | <DNS_server1>]          |
|                |                         |                         |
|                |                         | Function: sets          |
|                |                         | user-defined DNS        |
|                |                         | servers.                |
+----------------+-------------------------+-------------------------+
| **Response**   | [+CIPDNS_CUR:<DNS       | OK                      |
|                | server0>]               |                         |
|                |                         |                         |
|                | [+CIPDNS_CUR:<DNS       |                         |
|                | server1>]               |                         |
|                |                         |                         |
|                | OK                      |                         |
+----------------+-------------------------+-------------------------+
| **Parameters** | -  <enable>:                                      |
|                |                                                   |
|                | -  : disables                                     |
|                |    user-defined DNS                               |
|                |    servers;                                       |
|                |                                                   |
|                | -  1: enables                                     |
|                |    user-defined DNS                               |
|                |    servers.                                       |
|                |                                                   |
|                | -  <DNS server>:                                  |
|                |    optional parameter                             |
|                |    indicating the first                           |
|                |    DNS server;                                    |
|                |                                                   |
|                | -  <DNS server1>:                                 |
|                |    optional parameter                             |
|                |    indicating the                                 |
|                |    second DNS server;                             |
+----------------+-------------------------+-------------------------+
| **Notes**      | -  For command:                                   |
|                |    AT+CIPDNS_CUR=                                 |
|                |    (disable                                       |
|                |    user-defined DNS                               |
|                |    servers),                                      |
|                |    "28.67.222.222" will                           |
|                |    be used as DNS                                 |
|                |    server by default.                             |
|                |    And the DNS server                             |
|                |    may change according                           |
|                |    to the configuration                           |
|                |    of the router the                              |
|                |    BFQ4004 is connected                           |
|                |    to.                                            |
|                |                                                   |
|                | -  | For command:                                 |
|                |      AT+CIPDNS_CUR=1                              |
|                |      (enable                                      |
|                |      user-defined DNS                             |
|                |      servers, but the                             |
|                |      <DNS server>                                 |
|                |      parameters are not                           |
|                |      set), servers                                |
|                |    | "28.67.222.222"                              |
|                |      will be used as                              |
|                |      DNS server by                                |
|                |      default.                                     |
|                |                                                   |
|                | -  <DNS server> and                               |
|                |    <DNS server1> cannot                           |
|                |    be set to the same                             |
|                |    server.                                        |
+----------------+-------------------------+-------------------------+
| **Examples**   | AT+CIP                                            |
|                | DNS_CUR=1,"28.67.22.22"                           |
+----------------+-------------------------+-------------------------+

AT+CIPDNS_DEF – Sets User-defined DNS Servers, Configuration Saved to Flash
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-------------------------+
| **Command**    | Query Command:          | Set Command:            |
|                |                         |                         |
|                | AT+CIPDNS_DEF?          | AT+CIPDNS_DEF=<enable>  |
|                |                         |                         |
|                | Function: gets the      | [,<DNS_server>,         |
|                | current DNS server.     |                         |
|                |                         | <DNS_server1>]          |
|                |                         |                         |
|                |                         | Function: sets          |
|                |                         | user-defined DNS        |
|                |                         | servers.                |
+----------------+-------------------------+-------------------------+
| **Response**   | [+CIPDNS_DEF:<DNS       | OK                      |
|                | server0>]               |                         |
|                |                         |                         |
|                | [+CIPDNS_DEF:<DNS       |                         |
|                | server1>]               |                         |
|                |                         |                         |
|                | OK                      |                         |
+----------------+-------------------------+-------------------------+
| **Parameters** | -  <enable>:                                      |
|                |                                                   |
|                | -  : disables                                     |
|                |    user-defined DNS                               |
|                |    servers;                                       |
|                |                                                   |
|                | -  1: enables                                     |
|                |    user-defined DNS                               |
|                |    servers.                                       |
|                |                                                   |
|                | -  <DNS server>:                                  |
|                |    optional parameter                             |
|                |    indicating the first                           |
|                |    DNS server;                                    |
|                |                                                   |
|                | -  <DNS server1>:                                 |
|                |    optional parameter                             |
|                |    indicating the                                 |
|                |    second DNS server;                             |
+----------------+-------------------------+-------------------------+
| **Notes**      | -  For command:                                   |
|                |    AT+CIPDNS_DEF=                                 |
|                |    (disable                                       |
|                |    user-defined DNS                               |
|                |    servers),                                      |
|                |    "28.67.222.222" will                           |
|                |    be used as DNS                                 |
|                |    server by default.                             |
|                |    And the DNS server                             |
|                |    may change according                           |
|                |    to the configuration                           |
|                |    of the router the                              |
|                |    BFQ4004 is connected                           |
|                |    to.                                            |
|                |                                                   |
|                | -  | For command:                                 |
|                |      AT+CIPDNS_DEF=1                              |
|                |      (enable                                      |
|                |      user-defined DNS                             |
|                |      servers, but the                             |
|                |      <DNS server>                                 |
|                |      parameters are not                           |
|                |      set), servers                                |
|                |    | "28.67.222.222"                              |
|                |      will be used as                              |
|                |      DNS server by                                |
|                |      default.                                     |
|                |                                                   |
|                | -  <DNS server> and                               |
|                |    <DNS server1> cannot                           |
|                |    be set to the same                             |
|                |    server.                                        |
+----------------+-------------------------+-------------------------+
| **Examples**   | AT+CIP                                            |
|                | DNS_DEF=1,"28.67.22.22"                           |
+----------------+-------------------------+-------------------------+

.. _section-1:

HTTP-Related AT Commands
========================

.. _overview-5:

Overview
--------

============ ===========================================
**Commands** **Description**
============ ===========================================
AT+CHTTPURL  Set HTTP server port and address.
AT+CHTTPPH   Set path of POST/GET.
AT+CHTTPTP   Set command type of HTTP (GET or POST).
AT+CHTTPDT   Set name and value pair of data in HTTP.
AT+CHTTPTR   Send HTTP package and return received data.
============ ===========================================

.. _command-descriptions-4:

Command Descriptions
--------------------

AT+CHTTPURL – Sets HTTP Server Port and Address
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-------------------------+
| **Command**    | Query Command:          | Set Command:            |
|                |                         |                         |
|                | AT+CHTTPURL?            | AT+CHTTPURL=<port>,     |
|                |                         |                         |
|                | Function: gets the      | <IP_address>            |
|                | current port and IP     |                         |
|                | address of the HTTP     | Function: sets port and |
|                | server.                 | IP address of the       |
|                |                         | target HTTP server.     |
+----------------+-------------------------+-------------------------+
| **Response**   | +CHTTP                  | OK                      |
|                | URL=<port>,<IP_address> |                         |
|                |                         | or                      |
|                | OK                      |                         |
|                |                         | <error_code>            |
+----------------+-------------------------+-------------------------+
| **Parameters** | -  <port>: a number                               |
|                |    representing the                               |
|                |    port of the HTTP                               |
|                |    server.                                        |
|                |                                                   |
|                | -  <IP_address>: a                                |
|                |    string representing                            |
|                |    the IP address or                              |
|                |    domain name of the                             |
|                |    HTTP server.                                   |
|                |                                                   |
|                | -  <error_code>: a hex                            |
|                |    number in the form                             |
|                |    of “x7+Standard HTTP                           |
|                |    error code”.                                   |
+----------------+-------------------------+-------------------------+
| **Notes**      | If resource is not                                |
|                | found, standard HTTP                              |
|                | error code = 404, the                             |
|                | set command would                                 |
|                | return the following                              |
|                | error code:                                       |
|                |                                                   |
|                | x7194                                             |
|                |                                                   |
|                | Because                                           |
|                | hex(x7+44)=0x7194                                 |
|                |                                                   |
|                | For a complete list of                            |
|                | standard HTTP/1.1 error                           |
|                | codes please refer to:                            |
|                | RFC 2616:                                         |
|                | https://tool                                      |
|                | s.ietf.org/html/rfc2616                           |
+----------------+-------------------------+-------------------------+
| **Examples**   | AT+C                                              |
|                | HTTPURL=8,"192.168..18"                           |
+----------------+-------------------------+-------------------------+

AT+CHTTPPH – Sets Path of POST/GET
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------+-------------------------+-------------------------+
| **Command**    | Query Command:          | Set Command:            |
|                |                         |                         |
|                | AT+CHTTPPH?             | AT+CHTTPPH=<path>       |
|                |                         |                         |
|                | Function: gets paths of | Function: sets path of  |
|                | POST/GET.               | POST/GET.               |
+----------------+-------------------------+-------------------------+
| **Response**   | +CHTTPPH=<path>         | OK                      |
|                |                         |                         |
|                | OK                      |                         |
+----------------+-------------------------+-------------------------+
| **Parameters** | <path>: a string                                  |
|                | representing the path                             |
|                | of POST/GET.                                      |
+----------------+-------------------------+-------------------------+
| **Examples**   | AT+CHTTPPH=”/userLogin"                           |
+----------------+-------------------------+-------------------------+

AT+CHTTPCTP – Sets Command Type of HTTP (GET or POST)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

=============== ==================================================
**Set Command** AT+CHTTPCTP=<type>
                Function: sets command type of either POST or GET.
**Response**    OK
**Parameters**  <type>: a number representing GET or POST command.
                
                -  : GET (default);
                
                -  1: POST.
**Examples**    AT+CHTTPCTP=1
=============== ==================================================

AT+CHTTPCDT – Sets Name and Value Pair of Data in HTTP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-----------------+---------------------------------------------------+
| **Set Command** | AT+CHTTPCDT=<name>,<value>                        |
|                 |                                                   |
|                 | Function: sets name and value pair of data in     |
|                 | HTTP.                                             |
+-----------------+---------------------------------------------------+
| **Response**    | OK                                                |
+-----------------+---------------------------------------------------+
| **Parameters**  | <name>: a string representing the name of the     |
|                 | data;                                             |
|                 |                                                   |
|                 | <value>: a string representing the value          |
|                 | corresponding to the name.                        |
+-----------------+---------------------------------------------------+
| **Examples**    | AT+CHTTPCTP=”username”,”admin”                    |
+-----------------+---------------------------------------------------+

AT+CHTTPTR – Sends HTTP Package and Return Received Data
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+---------------------+-----------------------------------------------+
| **Execute Command** | AT+CHTTPTR                                    |
|                     |                                               |
|                     | Function: sends HTTP package and return       |
|                     | received data.                                |
+---------------------+-----------------------------------------------+
| **Response**        | <reply_data>                                  |
|                     |                                               |
|                     | OK                                            |
|                     |                                               |
|                     | or                                            |
|                     |                                               |
|                     | <error_code>                                  |
+---------------------+-----------------------------------------------+
| **Parameters**      | <reply_data>: data received from HTTP server. |
|                     |                                               |
|                     | <error_code>: a hex number in the form of     |
|                     | “x7+Standard HTTP error code”.                |
+---------------------+-----------------------------------------------+
| **Notes**           | If resource is not found, standard HTTP error |
|                     | code = 404, the set command would return the  |
|                     | following error code:                         |
|                     |                                               |
|                     | x7194                                         |
|                     |                                               |
|                     | Because hex(x7+44)=0x7194                     |
|                     |                                               |
|                     | For a complete list of standard HTTP/1.1      |
|                     | error codes please refer to: RFC 2616:        |
|                     | https://tools.ietf.org/html/rfc2616           |
+---------------------+-----------------------------------------------+
| **Examples**        | AT+CHTTPTR                                    |
+---------------------+-----------------------------------------------+

Example operation: (is this correct?)

GET:

| AT+CHTTPURL=8,"192.168..18"
| AT+CHTTPPH=”/usr/local/http"
| AT+CHTTPTP=0
| AT+CHTTPTR
| <reply_data> // GET data

POST:

| AT+CHTTPURL=8,"192.168..18"
| AT+CHTTPPH=”/usr/local/http"
| AT+CHTTPTP=1
| AT+CHTTPCDT=”field1”,”value1” // only 1 name-value pair at a time
| AT+CHTTPTR
| AT+CHTTPCDT=”field2”,”value2”
| AT+CHTTPTR
| …

Espressif’s HTTP commands:

AT+HTTPCLIENT=<opt>,<content-type>,[<url>],[<host>],[<path>],<transport_type>,[<data>][,"http_req_header"][,"http_req_header"][...]

AT+HTTPGETSIZE

AT+HTTPGETSIZE=<url>

Should we follow their commands?

Internet-of-Things (IoT)-Related AT Commands
============================================

MQTT Commands Overview
----------------------

=============== ===============
**Commands**    **Description**
=============== ===============
AT+CMQNEW       
AT+CMQCON       
AT+CMQDISCON    
AT+CMQSUB       
AT+CMQUNSUB     
AT+CMQPUB       
AT+CMQTTSNEW    
AT+CMQTTSNEWEXT 
=============== ===============

CoAP Commands Overview
----------------------

============= ===============
**Commands**  **Description**
============= ===============
AT+CCOAPNEW   
AT+CCOAPSEND  
AT+CCOAPCSEND 
AT+CCOAPDEL   
============= ===============

TLS Commands Overview
---------------------

============ ===============
**Commands** **Description**
============ ===============
AT+CTLSCFG   
AT+CTLSCONN  
AT+CTLSCLOSE 
AT+CTLSSEND  
AT+CTLSRECV  
AT+CSETCA    
============ ===============

AWS IoT Core AT Commands
========================

Customizing AT Firmware
=======================

Compiling AT project
--------------------

If users want to customize AT source code, or add customized AT
commands, please copy the folder “at” in the examples to the root
directory of the corresponding BFQ4004 SDK , and then enter
BFQ4004_SDK/at folder to develop and compile the custom AT project. For
details, please refer to BFQ4004 Getting Started Guide.

Customize AT Functions
----------------------

-  OTA：

The official AT firmware launched by BeeFi supports the command
AT+CIUPDATE by default, which helps update AT firmware to the latest
version from BeeFi Cloud.

For the customized AT firmware, users have to implement this function by
themselves to update the firmware from their own cloud. Please refer to
the OTA example detailed in\ *at_upgrade.c*.

-  [STRIKEOUT:SmartConfig：]

[STRIKEOUT:The official AT firmware launched by Espressif supports the
commands AT+CWSTARTSMART and AT+CWSTOPSMART.]

[STRIKEOUT:If users don’t need SmartConfig, you can compile AT Project
and disable CONFIG_AT_SMARTCONFIG_COMMAND_ENABLE in user_config.h for
smaller bin size and more memory.]

Add User-defined AT Commands
----------------------------

TBD

**Revision History**

======== =============================== ==========
Revision Description                     Date
V0.1.0   Initial internal review version 2020-07-26
======== =============================== ==========

|image1|

Disclaimer and Copyright Notice

Information in this document, including URL references, is subject to
change without notice. Please visit http://www.beefi.io/ for the latest
information.

THIS CODUMENT IS PROVIDED AS IS WITH NO WARRANTIES WHATSOEVER, INCLUDING
ANY WARRANTY OF MERCHANTABILITY, NON-INFRINGEMENT, FITNESS FOR ANY
PARTICULAR PURPOSE, OR ANY WARRANTY OTHERWISE ARISING OUT OF ANY
PROPOSAL, SPECIFICATION OR SAMPLE.

All liability, including liability for infringement of any proprietary
rights, relating to the use of information in this document, is
disclaimed. No licenses express or implied, by estoppel or otherwise, to
any intellectual property rights are granted herein.

The Wi-Fi Alliance Member logo is a trademark of the Wi-Fi Alliance. The
Bluetooth logo is a registered trademark of Bluetooth SIG.

All trade names, trademarks and registered trademarks mentioned in this
document are property of their respective owners and are hereby
acknowledged.

Copyright©2020 BeeFi Technologies Inc. All rights reserved.

.. |image1| image:: f/media/image3.png
   :width: 1.75208in
   :height: 0.60764in
