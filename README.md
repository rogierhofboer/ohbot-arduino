Ohbot arduino driver. 
=================

V1.8 - Servo Controller for Ohbot Robot using Ohbrain board
----------------

This sketch needs the following libraries which are both available under GNU public licence: 

* Adafruit Neopixel 
* VarSpeedServo

To install the Adafruit Neopixel library: 

1. Select Sketch, Include Library, Manage Libraries. 
2. In the box that says Filter your search type Adafruit Neopixel.
3. Click on the box that appears and click the Install button.

To install the VarSpeedServo library: 
1. Download [this zip file.](https://github.com/netlabtoolkit/VarSpeedServo/releases/download/v1.1.3/VarSpeedServo.zip) 
2. Inside the Arduino IDE select: Sketch → Include Library → Add .ZIP Library.
3. Browse to where you downloaded VarSpeedServo.zip � select it and click Open.

_This sketch also needs the wire library which is included in the Arduino environment_

Overview
-----------

The Servo Controller for Ohbot Robot receives commands on the serial port and converts these to instructions
for moving servo motors and controlling LEDs.  It also allows the analogue inputs on the Arduino to be polled

|Version | Change |
| ------ | ------ |
|V1.5 | Added eye light LED support, correction to input response.|
|V1.6 | Draft add I2C support for inputs.|
|V1.7 | Added demo program support|
|V1.8 | Remapped pinlist for 32U4 based board|

Commands:

m, d, a, x, n, t, r, l, i, g, e, h, c, v

MOVE
---

```arduino
mss,ttt[,vvv]  
```

|Param|Description |
| --- | --- |
| ss |servo number 0 to  11 |
|ttt | position in degrees, if >180 then uS pulse width|
|vvv |speed 1-250, 1 slowest, 0 = full speed.|

*defaults to centre (90 deg) and full speed with no parameters*

DETACH
------
```arduino
dss       
```

detaches servo `ss`

DETACH ALL
-----

```arduino
dx        
```

ATTACH
-------------

``` arduino
ass
```
attaches servo ss


ATTACH ALL
-----------

```arduino
ax        
``` 

Attach all specified servos


SET MAX PULSE
------

```arduino
xss,uuuu      
```

set max value uuu  in uS pulse width for servo ss rep 180 deg

SET MIN PULSE
-------

```arduino
nss,uuu   
```

set min value uuu in uS pulse width for servo ss rep 0 deg

STORE
----

```arduino
t    
```

store min and max values for all servos in EEPROM

RESET
-------------------

```arduino
r
```

sets all servos to midpoint.

LED
------------------

```arduino
lnn,rrr,ggg,bbb
```

|Param|Description           |
| --- | ---                  |
| nn  | led number (00 or 01)|
| rrr | red value (0-255)    |
| ggg | green value (0-255)  |
| bbb | blue value (0-255)   |

set led nn - 0 or 1 if  2 eyes used to r, g b values. 

To turn eyes off:

```arduino
l01,0,0,0
```

READ Analog
-----------------

```arduino
ipp
```

read Analog port pp.
responds with vpp,vvv where v is value of analog port.

MONITOR Port
----------

```arduino
hpp,e,ttt
```

start monitoring port pp

e = event to change and ttt parameter

e = 1 change greater than ttt 0 or not included any change

e = 2 value rises above threshold ttt

e = 3 value falls above threshold ttt

for events 2 and 3, it will trigger once, and be reset when value falls back below/above threshold.
kpp
stop monitoring port pp

special commands for setup
e5798     erase eeprom
Commands for I2C on D2,D3

ca,uuuu
set port address of I2C device to be addressed.

cw,bb,bb,bb...
write bytes bb...

cr,nn
read nn bytes from device
returns

Version
------

v04,vvv,vvv,vvv....
v - version number. 
returns version number

Ports
------

Digital 4-13 servos or pin 13 for leds

Analog A0-A5 inputs

I2C - 2 default ports used.

D2 I2C SDA Also servo 90

D3 I2C SCL Also servo 91

D0 Serial1 Rx Also servo 92

D1 Serial1 Tx Also servo 93

For reference with Ohbot

| Servo | Motor |
|------ | ----- |
|Servo 0|HeadNod|
|Servo 1|Head turn|
|Servo 2|Eye turn|
|Servo 3|Lid Blink|
|Servo 4|Top Lip|
|Servo 5|Bottom Lip|
|Servo 6|Eye tilt|

This Servo Controller for Ohbot Robot is free software; you can redistribute it and/or modify it under the terms of the GNU Lesser General Public License as published by the Free Software Foundation; either version 2.1 of the License, or (at your option) any later version.

This software is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU Lesser General Public License for more details.

You should have received a copy of the GNU Lesser General Public License along with this library; if not, write to the Free Software Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA  02110-1301  USA
