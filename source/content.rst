**Project 1 Introduction**

**Version 1.0.0**

Version Notes：

========== ======= ================================
Date       Version Description
========== ======= ================================
2020/05/12 1.0.0   Phase-1 AT commands, first draft
\                  
========== ======= ================================

**Table of Contents**

1 Command Description 1

2 Basic AT Commands 2

2.1 Overview 2

2.2 Commands 2

2.2.1 AT \- Test AT 2

2.2.2 ATE \- Configure echo of AT commands 2

2.2.2 AT+RST \- Restart module 2




1 Command Description
======================


Each command set contains four types of AT commands：

+-----------------+--------------+-----------------------------------+
| type            | format       | description                       |
+=================+==============+===================================+
| Test Command    | AT+<x>=?     | Queries the Set Command’s         |
|                 |              | internal parameters and their     |
|                 |              | range of values.                  |
+-----------------+--------------+-----------------------------------+
| Query Command   | AT+<x>?      | Return the current value of       |
|                 |              | parameters.                       |
+-----------------+--------------+-----------------------------------+
| Set Command     | AT+<x>=<...> | Sets the value of user-defined    |
|                 |              | parameters in commands,           |
|                 |              |                                   |
|                 |              | and runs these commands.          |
+-----------------+--------------+-----------------------------------+
| Execute Command | AT+<x>       | Runs commands with no             |
|                 |              | user-defined parameters.          |
+-----------------+--------------+-----------------------------------+



3. String values need to be included in double quotation marks, for
   example: AT+CWSAP="BFQ756290","21030826", 1,4

4. The default baud rate is 115200

5. AT commands have to be capitalized, and must end with a new line (CR
   LF)


2 Basic AT Commands
====================================

2.1 Overview
------------

=========== =============================================
commands    description
=========== =============================================
AT          Test AT
ATE         Configure echo of AT commands
AT+RST      Restart module
AT+GMR      Check version info
AT+RESTORE  Restore factory default setting
AT+UART_CUR Current UART configuration, Not save in Flash
AT+UART_DEF Default UART configuration, save in Flash
AT+SYSRAM   Check the available RAM size
=========== =============================================

2.2 Commands
------------

2.2.1 AT \- Test AT
~~~~~~~~~~~~~~~~~~

=============== ==
Execute Command AT
=============== ==
Response        OK
Parameters       \-
=============== ==

2.2.2 ATE \- Configure echo of AT commands
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

=============== ==
Execute Command AT
=============== ==
Response        OK
Parameters      \-
=============== ==

2.2.2 AT+RST \- Restart module
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

=============== ======
Execute Command AT+RST
=============== ======
Response        OK
Parameters      \-
=============== ======

