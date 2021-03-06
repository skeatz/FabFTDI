# FabFTDI Projects
This repository contains all my FabFTDI projects:
FabFTDI projects which make use of avr microcontrollers are based on the V-USB library from [obdev](https://www.obdev.at/products/vusb/index.html) and the AVR-CDC work done by [K Ishikawa](http://www.recursion.jp/prose/avrcdc/) at recursion.jp.

A few points about the AVR-CDC protocol with Atmel microcontrollers - AVR-CDC enables a PC to communicate with a low-speed USB device (AVR microcontroller) through a virtual COM port.

The table below (from **recursion.jp**) lists the specifications for AVR-CDC with different AVR microcontrollers:
* AVR-CDC with USART (ATmega8/48/88/168/328)
    * speed: 600 - 38400 bps
    * datasize: 5 - 8 bits
    * parity: none/even/odd
    * stopbit: 1/2
    * controls: DTR, RTS, CTS
* AVR-CDC with USART (ATtiny2313)
    * speed: 600 - 38400 bps
    * datasize: 8
    * parity: none
    * stopbit: 1
* AVR-CDC without USART (ATtiny45/85)
    * speed: 1200 - 4800 bps
    * datasize: 8
    * stopbit: 1...


1. **[CH340G-based FabFTDI](fabftdi-ch340g.md)**
   * speeds up to 2 Mbps (loopback)
   * tested up to 250 kbps with ESP8266 module
   * uses hardware USB-to-TTL chip
   * low cost (USD0.40 per IC for 10 pcs)
2. **[ATmega8-based FabFTDI](fabftdi-mega8.md)**
   * speeds up to 2 Mbps (loopback)
   * tested up to 250 kbps with ESP8266 module
   * hardware UART
   * uses V-USB/AVR-CDC library
3. **[ATtiny2313-based FabFTDI](fabftdi-tiny2313.md)**
   * speed up to 57600 bps
   * hardware UART
   * uses V-USB library
4. **[ATtiny45-based FabFTDI (w/crystal)](fabftdi-tiny45x.md)**
   * speeds up to 4800 bps
   * uses V-USB library
5. **[ATtiny45-based FabFTDI (w/internal PLL)](fabftdi-tiny45.md)**
   * speeds up to 4800 bps
   * uses V-USB library

![Fab FTDI collection](images/fabftdi_board-collection.png)

Collection of FabFTDI boards (from left): CH340g-based, ATmega8-based, ATtiny2313-based, ATtiny45-based w/crystal, ATtiny45-based w/internal oscillator

*Copyright (c) Steven Chew*...

*MIT license*
