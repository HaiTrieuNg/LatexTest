.. |br| raw:: html

     <br/>

ion 1.0.0**

Version Notes：

========== =========== ================================
**Date**   **Version** **Description**
========== =========== ================================
2020/05/12 1.0.0       Phase-1 AT commands, first draft
\                      
========== =========== ================================

**Table of Contents**

1 Command Description 1

2 Basic AT Commands 2

2.1 Overview 2

2.2 Commands 2

2.2.1 AT - Test AT 2

2.2.2 ATE - Configure echo of AT commands 2

2.2.2 AT+RST - Restart module 2

**1 Command Description**

Each command set contains four types of AT commands：

+-----------------+------------+-------------------------------------+
| **type**        | **format** | **description**                     |
+=================+============+=====================================+
| Test Command    | AT+<x>=?   | Queries the Set Command’s internal  |
|                 |            | parameters and their range of       |
|                 |            | values.                             |
+-----------------+------------+-------------------------------------+
| Query Command   | AT+<x>?    | Return the current value of         |
|                 |            | parameters.                         |
+-----------------+------------+-------------------------------------+
| Set Command     | AT+<x>=<…> | Sets the value of user-defined      |
|                 |            | parameters in commands,             |
|                 |            |                                     |
|                 |            | and runs these commands.            |
+-----------------+------------+-------------------------------------+
| Execute Command | AT+<x>     | Runs commands with no user-defined  |
|                 |            | parameters.                         |
+-----------------+------------+-------------------------------------+

1. String values need to be included in double quotation marks, for
   example: AT+CWSAP=”BFQ756290”,”21030826”, 1,4

1. The default baud rate is 115200

1. AT commands have to be capitalized, and must end with a new line (CR
      LF)

**2 Basic AT Commands**

**2.1 Overview**

============ =============================================
**commands** **description**
============ =============================================
AT           Test AT
ATE          Configure echo of AT commands
AT+RST       Restart module
AT+GMR       Check version info
AT+RESTORE   Restore factory default setting
AT+UART_CUR  Current UART configuration, Not save in Flash
AT+UART_DEF  Default UART configuration, save in Flash
AT+SYSRAM    Check the available RAM size
============ =============================================

**2.2 Commands**

**2.2.1 AT - Test AT**

=================== ======
**Execute Command** **AT**
=================== ======
Response            OK
Parameters          -
=================== ======

**2.2.2 ATE - Configure echo of AT commands**

=================== ======
**Execute Command** **AT**
=================== ======
Response            OK
Parameters          -
=================== ======

**2.2.2 AT+RST - Restart module**

=================== ==========
**Execute Command** **AT+RST**
=================== ==========
Response            OK
Parameters          -
\                   
\                   
=================== ==========

Note

Note 1

Note2

Note3

#

Important

Important content

More important informations

#

Code-block python

def some_function():

interesting = False

print 'This line is highlighted.'

print 'This one is not...'

print '...but this one is.'

#

BF4004Q


Packing List
============

   |image0|\ |image1|\ |image2|

   |image3|\ |image4|\ |image5|

.. note::
     -Some attention content |br|
     -Some attention content |br|
     -Some attention content |br|

.. important::
     Some attention content |br|

Introduction
============

   LoRaWan Gatewayâ€™s interfaces and connectors are illustrated below:

   **Ports and Connectors**

1. Antenna Port (2.4G Wi-Fi)

2. Ethernet Port (Support PoE)

3. Console Port

4. Nano SIM Socket

5. TF Card Socket

6. Ground Pad

7. Ground Pad

8. Antenna Port (GPS)

9. Antenna Port (Lora)

..

   **LED**

A. Power

B. Ethernet

C. LoRa1

D. NB-IoT Active

E. LoRa2 or NB-IoT Status

F. WLAN

Installation
============

   LoRaWan Gateway can be installed in two ways:

-  Pole Mounting

-  Wall Mounting

Pole Mounting
-------------

   **Step 1**: Fix the mount kit on the bottom of the device with four
   M5*8 screws as shown below:



   **Step 2**: Slide the Steel band clamps through the rectangular hole
   of the mount kit, wrap the band clamps around the pole, lock them and
   then tighten the clamps using a screwdriver.


Wall Mounting
-------------

   **Step 1**: Use Ã˜5mm drill head, drill 4 holes on the wall according
   to the dimension of the following picture and then plug the srew
   anchors in the wall;


   **Step 2**: Use the tapping screws, attach the device to the wall.



QC Card
=======



Warranty Card
=============

   Please fill in (*asterisk must be filled), and safekeep the warranty
   certificate.

   Please fill in the information of product:

   \*Product Model:
   \____________________________________________________________\_

   \*Product ID:
   \_______________________________________________________________\_

   Please fill in the information of customer:

   Userâ€™s Name:
   \______________________________________________________________\_

   Address:
   \__________________________________________________________________\_

   `Tel:
   \_______________________\_ <Tel:________________________>`__\ \______________________________________________\_

   E-mail:
   \___________________________________________________________________\_

   Please fill in the information of distributor:

   \*Distributor:
   \_______________________________________________________________\_

   \*Tel:
   \_____________________________________________________________________\_

   \* Date of Purchase:
   \__________________________________________________________\_

**
**

**Revision History**

======== =============== ==========
Revision Description     Date
1.00     Initial version 2018-07-29
======== =============== ==========

.. |image0| image:: f/media/image4.emf
   :width: 1.91944in
   :height: 1.91944in
.. |image1| image:: f/media/image5.emf
   :width: 1.91944in
   :height: 1.91944in
.. |image2| image:: f/media/image6.emf
   :width: 1.91944in
   :height: 1.91944in
.. |image3| image:: f/media/image7.emf
   :width: 1.91944in
   :height: 1.91944in
.. |image4| image:: f/media/image8.emf
   :width: 1.91944in
   :height: 1.91944in
.. |image5| image:: f/media/image9.emf
   :width: 1.91944in
   :height: 1.91944in

