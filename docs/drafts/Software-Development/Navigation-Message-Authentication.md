---
title: Navigation Message Authentication
description: Galileo E1B Open Service – Navigation Message Authentication Geotagging Photos, Task List, Map,  Path Tracking, GNSS SkyMap
---
## Galileo E1B Open Service – Navigation Message Authentication
### How to use P-9 Race receiving Galileo E1b
This page is <b>draft</b> on how to use P-9 Race by Columbus with PIC2BIM mobile app (Android) and in future iOS, credit to Columbus

The P-9 Race uses the NEO-M9N module from ublox, which supports receiving Galileo E1b and supports OSNMA Raw Data observations.

* Before use, you need to enable the Basic raw data on the P-9 Race.

<img src="/media/media_p-9-race-01-raw-data.png" width="229" height="73" />

Here is the parameter adjustment software for the P-9 Race: [<u>'u-center'</u>](https://www.u-blox.com/en/product/u-center)

* Download and run u-center, 

* then click View - 
    * Generation 9 Configuration view - Advanced Configuration. 
    * Search for 'sfrbx', select 'USB', and click
        * 'Set in RAM', 
        * 'Set in BBR', 
        * 'Set in Flash'.

<img src="/media/media_p-9-race-02-raw-data-u-center.png" width="229" height="73" />

* Search for 'measx', 
    * select 'USB', and click 
        * 'Set in RAM', 
        * 'Set in BBR', 
        * 'Set in Flash'. 

* Finally, click 'Send config changes'.

<img src="/media/media_p-9-race-03-raw-data-u-center.png" width="229" height="73" />


If all changes in the red circle are checked, it means the configuration has been successfully applied.

Here is the interface description of the NEO-M9N receiver module used in the P-9 Race: 

[u-blox M9 standard precision GNSS firmware
Protocol version 32.01](https://www.u-blox.com/sites/default/files/u-blox-M9-SPG-4.04_InterfaceDescription_UBX-21022436.pdf)

You can now proceed with OSNMA data parsing. For details, you can refer to: [<u>osnmaPython</u>](https://github.com/astromarc/osnmaPython) listed below

#### Software Development
PIC2BIM (EGNSS4ALL) is a geotagging photo mobile phone application, which is Open-Source for see following Readme iOS-Developer and Android-Developer.
[[Web-Console]]

