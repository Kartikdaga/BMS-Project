

## Texas Instruments

### INA228 (current sensor)
https://www.ti.com/product/INA228

### LM5009A (voltage regulator)
https://www.ti.com/product/LM5009A


## diyBMS Controller Changes

You need to add a "blob" of solder across solder bridge JP4 on the DIYBMS controller to enable RS485 termination resistor.


# SHUNT

The design is based on 50mV shunts, such as the Murata range

* 3020-01100-0 [150A](https://uk.farnell.com/murata-power-solutions/3020-01100-0/dc-shunt-150a-0-05v-screw/dp/2932602)
* 3020-0110X-0 [200A](https://uk.rs-online.com/web/p/shunts/8103277/) or [500A](https://uk.rs-online.com/web/p/shunts/8233570/)

technically, any 50mV shunt can be used, but the PCB is drilled specifically for the footprints of these devices.

Larger rating shunts will work, but won't fit onto the PCB

## PICKING THE CORRECT SHUNT 

Always pick a shunt at least 25% higher rating than you expect your maximum current load to be.

The INA chip uses 40.96mV maximum shunt voltage, so 50mV shunts are ideal for this range.

The maximum shunt current reading is calculated by this formula:

"Total shunt amp rating" * (40.96 / "Shunt mV scale")

For example a 200amp/50mV shunt:

200 * (40.96 / 50) = 163.84amp maximum reading.


# CODE

Source code is located in the code file.


## Programming ATTINY1614

Use the file diyBMSCurrentMonitor_ATtiny1614.hex from the releases section.  This is precompiled for you, so after this all you need to do is use AVRDUDE to program the device.

AVRDUDE can be downloaded from [here](http://savannah.nongnu.org/projects/avrdude)

Change "COM8" to match your environment.  

```
avrdude -v -p attiny1614 -C avrdude.conf -c jtag2updi -b 115200 -P "COM8" -U flash:w:diyBMSCurrentMonitor_ATtiny1614.hex:i
```

Credit: https://creativecommons.org/licenses/by-nc-sa/2.0/uk/
