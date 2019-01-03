UnoJoy - Encoder version
======

	This version of UnoJoy! (created by Alam Chatham) allows you to use optical encoders or incremental encoders in place of a potentiometer, swill allowing you to easily turn an Arduino Uno or Mega into a PS3-compatible USB game controller.
	It's still in BETA phase, but its stable to use if correctly configured.


Getting Started
===============

	Hi there!  Welcome to using UnoJoy!

	UnoJoy lets you use a plain, unmodified Arduino Uno
	to create native USB joysticks.  It is a three-part system:

	Drivers - Needed to re-flash the Arduino's USB communication chip
	Software - The UnoJoy library for Arduino
	Firmware - Code to load onto Arduino's USB communication chip

	In order to make UnoJoy work, you'll need to take care of
	all three parts.  We're here to make that process as easy as
	possible.


	Drivers
	=======

	In the UnoJoy directory, there are installer files for the drivers
	you'll need for the DFU bootloader.  Choose the correct one for your OS:
	WindowsUnoJoyDriverInstaller.exe
	LionUnoJoyDrivers.pkg
	SnowLeopardUnoJoyDrivers.pkg

	On Windows, you'll also need to download and install Atmel's FLIP tool:
	http://www.atmel.com/tools/FLIP.aspx

	On Linux you'll need to install dfu-programmer. you can get it by typing to your terminal:
	sudo apt-get install dfu-programmer
	or
	sudo aptitude install dfu-programmer 
	depending on your distribution.
	You can also build it from source: https://github.com/dfu-programmer/dfu-programmer
	You also have to make the flashing script runnable by typing:
	chmod +x TurnIntoAJoystick.sh
	into your terminal when in UnoJoy directory.


	Software
	========

	To get started, first, go to the UnoJoyArduinoEncoderSample
	or the MegaJoyEncoderSample folder. Open up the .ino file
	and upload that code to your Arduino (don't mix codes and/or
	firmwares, this can be bad). Now, we move onto the hardware


	Hardware
	========

	Now that we have the proper code on the Arduino, we need
	to reprogram the communications chip on the Arduino.
	In order to do this, you need to first put the Arduino
	into 'DFU' (Device Firmware Update) mode. The official
	documentation for this is here

	http://arduino.cc/en/Hacking/DFUProgramming8U2

	----HOW TO PUT YOUR ARDUINO INTO DFU MODE----
	You do that by shorting two of the pins on the block of 6 pins between
	the USB connector.  Using a piece of wire or other small metal object,
	connect the 2 pins closest to the USB connector together.
	(the ones that turn from o to | in the diagram)
	
	The board is like this \/
	__________________________________________________________________
			  o o o     				  	  |
	USB Type B Port	  o o o    				  	  |
									  |	
									  |	
									  |	
									  |
	DC Port								  |
	__________________________________________________________________|
	
	
	Make the connection/short-circuit like this \/
	__________________________________________________________________
			    | o o 				  	  |
	USB Type B Port	    | o o				  	  |
									  |	
									  |	
									  |	
									  |
	DC Port								  |
	__________________________________________________________________|	
							
	The connection can't be kept, it's only like a button push, not a hold button.
	
	It should disconnect and reconnect (making the noises
	if your computer is configured to it), and now shows up
	to your system as 'Arduino UNO DFU', or showing the 
	chip's name, like 'ATMega16U2'.
	
	In OSX, you will get no feedback from your computer, but
	the lights on the Arduino will stop flashing.


	ONCE YOU ARE IN DFU MODE
	========================

	Once the Arduino is in DFU mode, to update the firmware, simply click:

	Windows: TurnIntoAJoystick.bat
			 
	OSX:     TurnIntoAJoystick.command
	
	Linux:   ./TurnIntoAJoystic.sh

	IMPORTANT: Once you update the firmware, you'll need to 
	unplug and plug the Arduino back in for it to show up with
	the new firmware - it'll just hang out in DFU mode until you do.

	When you plug the Arduino in again now, it will show up to your
	computer as an 'UnoJoy Joystick'.  You can check this by doing
	the steps in the next section.

	HOW TO CHECK WHICH MODE YOU ARE IN
	==================================

	On Windows 7, you can check it out by going to
		Start->Devices and Printers
		and you should see it there under 'Unspecified'
		In Arduino mode, it will appear as 'Arduino UNO (COM 23)'
		In DFU mode, it will appear as 'Arduino UNO DFU' or showing the chip's name.
		In UnoJoy mode, it will appear at the top as 'UnoJoy Joystick'

	On OSX, you should see it:
		Snow Leopard: Apple->About This Mac->More Info...->USB
		Lion: Apple->About This Mac->More Info...->System Report->USB
		You may need to refresh (command-R) to see it update.
		In Arduino mode, it will appear as 'Arduino UNO'
		In DFU mode, it will appear as 'Arduino UNO DFU' or showing the chip's name.
		In UnoJoy mode, it will appear at the top as 'UnoJoy Joystick'
	
	On Linux, you can type lsusb to your terminal.
		In response you'll get list of all connected usb devices.
		From there you should find:
		In Arduino mode, you should see  a device named Arduino Uno etc.
		In DFU mode, you should see  a device named Atmel corp. etc.
		In UnoJoy mode, you should see a device named Cygnal Integrated Products etc.

