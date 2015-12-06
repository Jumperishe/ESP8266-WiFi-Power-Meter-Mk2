# ESP8266 WiFi-Power-Meter-Mk1
ESP8266 WiFi SOC based Webserver Power Meter to calculate accurate kilowatt consumption from digital electricity meters. These meters emit LED pulses of usually 1000 pulses per hour per KW hr, these are detected, timed and converted into the Kilowatt/Hr equivalent and stored on the micro webserver as a web page. The data may then be retrieved via a tablet, smartphone, PC or Pi micro using a standard HTTP request for display or further processing. The message takes the form :-
  HTTP:// your-local-IP-address/gpio/0 0r 1/2/3/4 there are 5 messages at present in various forms of presentation.
  
It has been tested on the Landis-Gyr EM5100 meter and works accurately and reliably although at present it wont indicate whether the power is being imported or exported, this is a function of this particular meter. A Mk2 wifi ESP meter is being tested which has a simple add-on module that connects to the existing Mk1 unit to indicate + or - power.

REQUIREMENTS

The power meter consists  of a light reader module ($1-50), an ESP8266 wifi module and a 5v power supply. There are a number of different ESP8266 modules but by far the easiest to use is the ESP8266-12 Dev Kit module (nodeMCU (LUA)) Aus$8-12, this has all the required parts to program the device on the one module plus some additional ports for other usage. The LUA language usually used with this module is not used in this project. 
NOTE that the ESP8266 runs on 3.3V NOT 5V but the module mentioned above has a built in regulator so while programming it the power comes from the +5v USB port. You will also need a suitable 5v - 9v power source when running on its own. There are pics of all the components in the images folder.

This project uses the ESP8266 core library for Arduino which then allows you to program in Arduino code and use Arduino library and IDE. Download the ESP8266 Core library from https://github.com/esp8266/Arduino and the Arduino IDE from the Arduino website. You will probably need to flash the ESP8266 with the latest firmware version, if required just google on how to find and do this. You will need the firmware flasher utility and flash into 0x00000 location. Download this software (.ino file) and put it in your Arduino projects folders. Set your SSID and password and meter pulse rate (default is 1000kw/hr), set the IP address and gateway etc. If you are using DHP comment out the 4 lines of code as indicated in the script/sketch. To program the module hold down the ESP flash button and press and release reset and upload the Power Meter software to your ESP8266 with the Arduino IDE.

INSTALL

Bend the light detector so it will contact the flat meter surface and locate it over the pulsing LED and power the module with 3.3v from the ESP8266, adjust pot' until the LED on the module flashes in sympathy and temporarily just stick it in place with tape or bluetack. Attach the output (and ground) from light module to the ESP8266, the output to GPIO4 (D2), and GPIO5 (D1) may be connected to an external LED if required via a 470ohm resistor or thereabouts. If the pulses are registering OK with the ESP8266 the External LED will flash in sympathy. 

If you decide to use the basic ESP8266-01 module then connect the light module output to GPIO0 also connect the ground, the external LED to GPIO2 via resistor to 3.3v but remember you have to power the module with 3.3v. Then change the GPIO entries in the software accordingly. Note with the basic models of ESP it is advisable to add a reset button to ensure it starts correctly after power up this is due to the GPIO pins having a dual purpose with the programming function. Initially set in debug mode and use the IDE serial monitor to watch module progress.

Ping the address of the ESP to ensure it is connected to wifi and make an HTTP request e.g http://192.168.0.100/gpio/0 and you should get an instant data return something like this :- Power Consumption : 3.435 KWs indicating your current power import or export. Try other messages /1/2/3/4 the replies are all slightly different. Whether the data reading is import or export will be determined in the MK2 version which will just require an additional module and software upgrade, all the rest stays the same.
