# ESP32 With Arduino IDE
How to setup your Arduino IDE for ESP32 Microcontrollers 

1- ON YOU ARDUINO IDE, GO TO 'File' then 'Preferences' 

![Screenshot 2022-08-21 060534](https://user-images.githubusercontent.com/109004035/185773558-4eebe24c-552e-427e-ab62-974eb007431a.jpg)

2- In the 'Additional Boards Manager URLs' paste this link : https://dl.espressif.com/dl/package_esp32_index.json

![Screenshot 2022-08-21 060514](https://user-images.githubusercontent.com/109004035/185773560-118b8521-258b-411b-bf77-ea3edd94dfbd.jpg)

3- Go to 'Tools' then ' Board' and pick 'Boards manager' . You can access it from the left side bar on newer Arduino IDEs releases too!

![Screenshot 2022-08-21 060910](https://user-images.githubusercontent.com/109004035/185773643-cb2e0a9f-3c56-4e36-bb0c-a0f99641d476.jpg)

4- Search for 'ESP32' , and install the ' ESP32 by espressif systems' .

![Screenshot 2022-08-21 061124](https://user-images.githubusercontent.com/109004035/185773690-00ed1348-d12e-4460-85e4-9fbc21882997.jpg)

**From this point, you should be able to see the new ESP32 boards under 'Tools' then ' Boards' and then ' ESP32'**

![Screenshot 2022-08-21 061546](https://user-images.githubusercontent.com/109004035/185773762-a34ab7dd-ded7-4c54-ae86-5023ba85a477.jpg)

## Testing
After you are done with the setups, it's time to test if every thing is working fine!

Plug your ESP32 to your PC, go to 'Tools' then 'Boards' and then ' ESP32' and select ' ESP32 Dev Module'

![Screenshot 2022-08-21 062045](https://user-images.githubusercontent.com/109004035/185773921-42e749e0-ba8b-4f9b-995b-f3ab8a75d951.jpg)

then select the right COM.

Now, go to 'File' then 'examples' and from ' Basics' pick 'AnalogReadSerial'

![Screenshot 2022-08-21 062613](https://user-images.githubusercontent.com/109004035/185774029-11332658-8503-44d9-9637-6a8afab44f29.jpg)

After uploading the code, go to your Serial monitor, and you should be able to see the readings, try touching the pins!

![Screenshot 2022-08-21 070722](https://user-images.githubusercontent.com/109004035/185775106-366e9a2d-0342-4830-9a50-ecf7b93f0bbc.jpg)

![Screenshot 2022-08-21 070747](https://user-images.githubusercontent.com/109004035/185775110-5ae47ab6-eb3b-411d-849c-31928f595b4e.jpg)


### Troubleshooting 
In case your ESP32 is not working, or you cant see the COM on your IDE,

1) Nowadays there are a lot of cheap (Chinese) USB cables that can only be used for charging or powering devices. I assume these have only 2 out of 4 wires: ground and +5V, but no data lines. If you would use a cable like that, the result would be what is described. So make sure you have a 'real' USB cable by testing it on another device. Don't just check if it charges your phone, but check if you are actually able to transfer data.

2) The USB connection is not handled by the ESP32, as an ESP32 only has serial lines (rx and tx), no USB. A dev board typically includes some sort of USB to serial converter chip (sometimes refered to as FTDI). This chip communicates with your computer, resulting in the creation of a virtual COM port. If you have a driver for that chip installed, otherwise it won't work. Without a driver the chip probably turns up as unsupported or unrecognized device in your hardware list. Although the ESP32 module may be the same, you might have a dev board with a different USB to serial converter than other devices you might have tested on your computer. So if one dev board works and another one doesn't, that does not necessarily mean the board is defective. You might just need to install a driver for the USB to serial chip on your dev board.

With a good cable and the right driver installed, your PC should present a COM port even if you would completely remove the ESP32 module from the board, because the USB communication is not handled by the ESP32.

I did run into the same problem, but is solved.
It's important to learn which USB to UART bridge is on the ESP32.

The link for the CH340:
https://sparks.gogo.co.nz/ch340.html

For my case, it worked after installing the [CP210x Windows Drivers with Serial Enumerator](https://www.silabs.com/documents/public/software/CP210x_Windows_Drivers_with_Serial_Enumeration.zip)

You can also check [Here](https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers?tab=overview) For more details on this regard.

Hope this helps!
