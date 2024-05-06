---
h1: "AVR clean up and install"
title: "Update firmware on 3dc3dchameleon"
date: "2024-05-06"
description: Clean up old IDE, from control panel uninstall the current IDE.
---
        



Delete appdata folders, they may be hidden.

![](static/img/copy-of-avr-clean-up-and-install-1.png)
Make sure the hidden items box is checked in the view tab.

![](static/img/copy-of-avr-clean-up-and-install-2.png)

My files are located here:

C:.Users.broth.AppData.Local

Delete the Arduino15 folder.

Now install the Arduino IDE. I am using the windows installed version 1.8.19, let the installer use default install locations. It should be C:.Program Files (x86).Arduino

![](static/img/copy-of-avr-clean-up-and-install-3.png)

Open the Arduino IDE so it builds folders and we can go ahead and install the ISP programmer. Leave the blank sketch open for now.

Open system device manager.

![](static/img/copy-of-avr-clean-up-and-install-4.png)

![](static/img/copy-of-avr-clean-up-and-install-5.png)

![](static/img/copy-of-avr-clean-up-and-install-6.png)

In device manager look for com &amp; LPT ports, there may not be any yet.

Plug in the Arduino UNO into the USB check device manager again:

![](static/img/copy-of-avr-clean-up-and-install-7.png)

If you have an actual Arduino, it will call it out in the device manager. Note the com port.

If you have a clone, it might not know what the device is. In this screen shot, it know the device is a CH340 device and it had a driver for it. 

If you see a device, but it is unknown, you will need a CH340 driver. 

Links to driver:

Driver page:

<https://learn.sparkfun.com/tutorials/how-to-install-ch340-drivers/all>

Direct download:

[https://cdn.sparkfun.com/assets/learn.tutorials/8/4/4/CH341SER.EXE?.gl=1.13829hw..ga.NjczNDUwMDY0LjE3MDM3ODI0OTk...ga.T369JS7J9N.MTcwMzc4MjQ5OS4xLjAuMTcwMzc4MjQ5OS42MC4wLjA](https://cdn.sparkfun.com/assets/learn_tutorials/8/4/4/CH341SER.EXE?_gl=1*13829hw*_ga*NjczNDUwMDY0LjE3MDM3ODI0OTk.*_ga_T369JS7J9N*MTcwMzc4MjQ5OS4xLjAuMTcwMzc4MjQ5OS42MC4wLjA).

![](static/img/copy-of-avr-clean-up-and-install-8.png)

After downloading the driver, leave your device plugged in USB and press__ install__. After install is successful, go back to device manager and make sure the status of the board has changed like the one in the screen shot above. You are now ready to use the device. Make sure to note the com port. 

Back to the Arduino IDE, upload a blank sketch to your board to clear it out. Go to tools and make sure board says Arduino Uno, then in port make sure you are set to the same com port we saw in device manager.

 ![](static/img/copy-of-avr-clean-up-and-install-9.png)

Then hit the right arrow to upload:

![](static/img/copy-of-avr-clean-up-and-install-10.png)

This is what it will look like when the upload has completed successfully.

Now use an example sketch to turn your UNO into an ISP programer.

Got to File&gt;Eamples&gt;11.Arduino ISP&gt;ArduinoISP

![](static/img/copy-of-avr-clean-up-and-install-11.png)

This will open a new sketch, now press the upload arrow to upload to your UNO.

![](static/img/copy-of-avr-clean-up-and-install-12.png)

This is what it looks like when the upload completes successfully.

Now that the Arduino IDE is installed and your UNO is now a ISP programmer, we can close all the Arduino IDE windows. 

We need to install some path variables in windows so we can use AVRDUDE from command line easier. 

You need to add these 2 paths, one for the EXE and one for the config file:

C:.Program Files (x86).Arduino.hardware.tools.avr.bin

C:.Program Files (x86).Arduino.hardware.tools.avr.etc

In windows, go to control panel, system and security, then system

![](static/img/copy-of-avr-clean-up-and-install-13.png)

![](tatic/img/copy-of-avr-clean-up-and-install-14.png)

Then scroll down to Advanced system settings

![](static/img/copy-of-avr-clean-up-and-install-15.png)

Then click Environment variables:

![](static/img/copy-of-avr-clean-up-and-install-16.png)

In the system variable box, highlight PATH then click edit:

![](static/img/copy-of-avr-clean-up-and-install-17.png)

Press New and paste in the 2 variables from above, it should look like this:

![](static/img/copy-of-avr-clean-up-and-install-18.png)

Press Ok and close the windows. 

Now open command prompt go to the Windows key and type cmd to search:

![](static/img/copy-of-avr-clean-up-and-install-19.png)

Click Command Prompt to open it.

![](static/img/copy-of-avr-clean-up-and-install-20.png)

Type in __avrdude __and press enter, if you get this display of the help screen, everything is setup correctly. 

WIRING THE UNO TO THE CHAMELEON

![](static/img/copy-of-avr-clean-up-and-install-21.jpeg)

![](static/img/copy-of-avr-clean-up-and-install-22.jpeg)

3D Chameleon header pins

![](static/img/copy-of-avr-clean-up-and-install-23.jpeg)

Now with your UNO connected to USB and your Chameleon board connected to the ICSP pin run this command as a test. (Update your com port)

avrdude -P com8 -b 19200 -c avrisp -p m328p -v

![](static/img/copy-of-avr-clean-up-and-install-24.png)

This is the full output of the command, you should see all the settings at the bottom.

![](static/img/copy-of-avr-clean-up-and-install-25.png)

![](static/img/copy-of-avr-clean-up-and-install-26.png)

Now that AVR is working as we expect it to, we need to flash the Chameleon firmware. 

Download Firmware from here: <https://www.3dchameleon.com/forum/getting-started/mk3-firmware-upgrade-instructions>

Direct [link](60eeab_0ac45769fbd4485e9481d403cfe817ef.zip) here 

You will download a ZIP file, right click and extract all, you will see the .HEX file we need.

![](static/img/copy-of-avr-clean-up-and-install-27.png)

Right click and copy that file to a common location, I am going to use Desktop

![](static/img/copy-of-avr-clean-up-and-install-28.png)

![](static/img/copy-of-avr-clean-up-and-install-29.png)

With the file on your Desktop, we will head back to command line.

Change directory to the HEX file location, here mine is C:.Users.broth.OneDrive.Desktop&gt;

Update the command for your user name:

cd C:.Users.__broth__.OneDrive.Desktop

Now is the same folder as the .HEX file we can run the command to flash the firmware to the Chameleon board, remember to update your com port:

avrdude -P com7 -b 19200 -c avrisp -p m328p -v -e -U flash:w:SelectorFirmwareMK3.1.hex:i

![](static/img/copy-of-avr-clean-up-and-install-30.png)

While flashing you should see send and receive lights flashing on the UNO, this is a good sign. 

Once completed successfully, this is the full output you should see. Note the fuse information at the bottom is there, that’s how you know you are getting the full output.

![](static/img/copy-of-avr-clean-up-and-install-31.png)

![](static/img/copy-of-avr-clean-up-and-install-32.png)