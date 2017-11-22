# te923tool
A tool for reading data from Hideki weater stations (and some other) like te923

see http://te923.fukz.org for more Informations

# About

A few years ago, I got a Mebus TE923 weather station. There was a very terrible java program shipped with this tool. I looked for a better software runing on linux if possible. But I found only closed source software witch costs money. So I startet to build my own software.

I user a windows software within a virtual maschine to reverse engineering the protocol used by the device. After some exhausting hours I got a very small command line tool witch reads the data from the weather station. I’ve called te923tool.

The te923tool supports most weather stations based on Hideki weather station like IROX Pro X, Mebus TE923 or TFA Nexus. Some other hardware is supported but not all devices are testet yet. Feel free to make a test and give me a feedback if it works or fix the programm if it not works.

# Building

The software is shipped only as source code. After you downloaded the source code just untar and compile it.

## Note

### You have to install libusb first. Te923 requires libusb.
  ```
tar xvzf te923tool*
cd te923tool*
make all
  ```
This will build a te923con binary file which is all you need. Feel free to copy it to /usr/bin or make a link.

# Usage

The usage of the tool is very simple. There are some command line options you can use.

Parameter | Description
------ | ----------
-D | gives you a debug output. Its usefull if you send me an email for debugging.
-d | Dumps all data stored in internel memory (for hardware with small memory - 208 values).
-b | Dump from stations with big memory (new hardware versions) ### experimental.
-s | Gets the status from the device. See status info for more details.
-i | Sets the output for invalid values (unreachable sensors), default is hidden.
-h | prints a help text
-v | prints the version number of the te923 tool

If you start the tool (you have to start it as root), you get a colon separated line with all values. Unknown values
(if sensor is not present) are hidden.

  ```
T0:H0:T1:H1:T2:H2:T3:H3:T4:H4:T5:H5:PRESS:UV:FC:STORM:WD:WS:WG:WC:RC

-  T0    - temperature from internal sensor in °C
-  H0    - humidity from internal sensor in % rel
-  T1..5 - temperature from external sensor 1..4 in °C
-  H1..5 - humidity from external sensor 1...4 in % rel
-  PRESS - air pressure in mBar
-  UV    - UV index from UV sensor
-  FC    - station forecast, see below for more details
-  STORM - stormwarning; 0 - no warning, 1 - fix your dog
-  WD    - wind direction in n x 22.5°; 0 -> north
-  WS    - wind speed in m/s
-  WG    - wind gust speed in m/s
-  WC    - windchill temperature in °C
-  RC    - rain counter (maybe since station starts measurement) as value


   weather forecast means (as precisely as possible)
     0 - heavy snow
     1 - little snow
     2 - heavy rain
     3 - little rain
     4 - cloudy
     5 - some clouds
     6 - sunny
  ```

If you use the option -s you get a status report of the device. The output is

  ```
SYSSW:BARSW:EXTSW:RCCSW:WINSW:BATR:BATU:BATW:BAT5:BAT4:BAT5:BAT2:BAT1

 SYSSW  - software version of system controller
 BARSW  - software version of barometer
 EXTSW  - software version of UV and channel controller
 RCCSW  - software version of rain controller
 WINSW  - software version of wind controller
 BATR   - battery of rain sensor (1-good (not present), 0-low)
 BATU   - battery of UV sensor (1-good (not present), 0-low)
 BATW   - battery of wind sensor (1-good (not present), 0-low)
 BAT5   - battery of sensor 5 (1-good (not present), 0-low)
 BAT4   - battery of sensor 4 (1-good (not present), 0-low)
 BAT3   - battery of sensor 3 (1-good (not present), 0-low)
 BAT2   - battery of sensor 2 (1-good (not present), 0-low)
 BAT1   - battery of sensor 1 (1-good (not present), 0-low)
  ```
# License

This program is free software, published under the terms of the GNU General Public License.
