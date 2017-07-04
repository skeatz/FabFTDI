##FabFTDI - ATmega8

* ATmega8A-AU based Fab FTDI
* tested up to:
  * 2 Mbps on loopback
  * 250000 bps with ESP8266
* uses V-USB library
  * AVR-CDC from [Recursion.jp](http://www.recursion.jp/prose/avrcdc/)

##Schematic & Board Layout

![FabFTDI-mega8 schematic](images/fabftdi-mega8-01.png)

I opted to use a 12 MHz crystal in my design because I had some handy (bought for my CH340g-based FabFTDI). Also, ***the compiled .hex file is for an ATmega8 with 12 MHz crystal***. If you are using a different crystal oscillator, you will need to recompile from [source](http://www.recursion.jp/prose/avrcdc/download.html).

Only the TXD and RXD pins are implemented on the FTDI interface (no RTS/CTS).

The FTDI-Vcc is 3.6V. This means that it can work directly with 3.3V-based systems like the ESP8266. If you are interfacing with 5V boards, **do not connect the FTDI-Vcc to the target Vcc**, as I have not implemented 3.6V zeners for the USB D+ and D- lines.

![FabFTDI-mega8 board layout](images/fabftdi-mega8-02.png)

Mill and stuff the PCB.

![FabFTDI board after milling](images/fabftdi-mega8-03.png)

![FabFTDI board after stuffing](images/fabftdi-mega8-04.png)

##Programming the Fab FTDI board

Unlike the CH340g-based FabFTDI, the ATmega8-based FabFTDI board uses the V-USB software library to implement USB-to-TTL conversion, i.e. it has to be programmed with the correct firmware before it can be used.

You need both an ISP programmer like the [FabISP](http://docs.academany.org/FabAcademy-Tutorials/_book/en/week4_electronic_production/fabisp.html) and [avrdude](http://savannah.nongnu.org/projects/avrdude) to program the FabFTDI-mega8 board. Instructions for installing avrdude can be found in the Fab Academy [tutorials](http://docs.academany.org/FabAcademy-Tutorials/_book/en/week4_electronic_production/fabisp.html) page. If you are using a different speed crystal oscillator, you will need to re-compile the firmware from [source](http://www.recursion.jp/prose/avrcdc/download.html).

Download the [FabFTDI-mega8 firmware](files/mega8/cdcmega8.hex).

Flash the firmware onto the FabFTDI-mega8 board using avrdude:

`avrdude -c usbtiny -p m8 -U flash:w:cdcmega8.hex -U lfuse:w:0xff:m -U hfuse:w:0x8f:m`

If you have managed to successfully flash the firmware onto the FabFTDI-mega8 board, give yourself a **pat** on the back. You are almost home.

![Flashing the firmware](images/fabftdi-mega8-05.png)

##Testing the Board

Plug the FabFTDI-mega8 board into your computer's USB port. Your computer should recognise the FabFTDI-mega8 board directly, as it implements the HIDinterface protocol.

On Windows machines, look for the COMport under Control Panel > System > Device Manager. On Linux or OSX machines, type the commands:
```
lsusb
ls /dev/ttyU*
```
The FabFTDI-mega8 should appear as ***ID 16c0:05e1 Van Ooijen Technische Informatica Free shared USB VID/PID pair for CDC devices*** and ***/dev/ttyACM0***

To perform loopback test on the FabFTDI-mega8 board, jumper the TXD and RXD pins. Open your favorite terminal emulation software, e.g. Arduino IDE or picocom. Select the device port.

E.g. for Arduino IDE on Linux, select Tools > Port > /dev/ttyACM0. Click Serail Monitor (**Ctrl+Shift+M**). Select *Both NL & CR*. Select the desired baud rate. Type a message on the transmit window and press **Enter** or click the **Send** button. You should see the message appearing ont the received data window.

![Loopback test](images/fabftdi-mega8-07.png)

As stated at the start of this tutorial, I have tested the FabFTDI-mega8 board up to 2 Mbps on loopback and 250 kbps on an ESP8266 module.

You can substitute the ATmega8A-AU with the ATmega328p-AU as the 2 devices are pin compatible.

Good luck and have fun with your FabFTDI board!

##Files

[Eagle Schematic](files/mega8/fabftdi-mega8.sch)

[Eagle PCB layout](files/mega8/fabftdi-mega8.brd)

[FabFTDI-mega8 firmware (12MHz crystal)](files/mega8/cdcmega8.hex)

[Firmware for ATmega328p (12MHz crystal)](files/mega8/cdcmega328p.hex)
