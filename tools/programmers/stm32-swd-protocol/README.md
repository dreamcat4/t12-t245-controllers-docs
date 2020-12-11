# Programmers

Along with connecting up a hardware programmer device, as detailed in this section. You will also need to install a suitable programmer software tool to run on your PC. Which can connect to it and talk over the SWD protocol.

This section assumes that you have already installed necessary [software tools for STM32 platform](/tools/software/STM32CubeIDE). In particular you must [Install OpenOCD](/tools/software/STM32CubeIDE#install-openocd). This is the tool we use in this guide. Perhaps it's a good idea to go and do that first.

Other than OpenOCD there are 2 other SWD software tools: J-Link and ST-Link. And a version of ST-Link is also embedded and distributed within the STM32Cube**IDE**. However the software tool we use here is OpenOCD. So those tools are not covered here.

BTW Many thanks and a Credit to Paul Ferster of OpenOCD project on Freenode IRC. For so much patience, guidance and help with SWD protocol on OpenOCD with the TUMPA v2. Additionally Paul helped to properly document many specific information in regards to the `openocd` toolchain, with its special flags etc. To help provide all these steps in the README here. 

<!-- MarkdownTOC -->

* [Connecting Hardware](#connecting-hardware)
	* [SWD Programmers / Debuggers](#swd-programmers--debuggers)
	* [STM32 OLED Controller PCB \(Target device\)](#stm32-oled-controller-pcb-target-device)
		* [Finding the target pin assignments in STM32Cube**MX** Tool](#finding-the-target-pin-assignments-in-stm32cubemx-tool)
* [Connecting a hardware Debugger](#connecting-a-hardware-debugger)
		* [TIAO TUMPA v2 Jumper settings](#tiao-tumpa-v2-jumper-settings)
	* [Connecting a Logic Analyzer](#connecting-a-logic-analyzer)
* [Connecting over SWD](#connecting-over-swd)
	* [With OpenOCD](#with-openocd)
		* [With a TIAO TUMPA v2 hardware debugger](#with-a-tiao-tumpa-v2-hardware-debugger)
		* [Failed Connection](#failed-connection)
		* [Successful Connection](#successful-connection)

<!-- /MarkdownTOC -->

<a id="connecting-hardware"></a>
## Connecting Hardware

<a id="swd-programmers--debuggers"></a>
### SWD Programmers / Debuggers

The debugger I have here is the [TIAO TUMPA v2](https://www.tiaowiki.com/w/TIAO_USB_Multi_Protocol_Adapter_User%27s_Manual). Which includes an SWD header and is supported by OpenOCD.

If you cannot get that device then there are a variety cheap J-Link clones / compatible devices available. For example this one [on aliexpress](https://www.aliexpress.com/item/32743219240.html).

![JLink clone](example-jlink-clone.png)

<a id="stm32-oled-controller-pcb-target-device"></a>
### STM32 OLED Controller PCB (Target device)

***Example:*** Here is the connections for the 64 LQFP version of the MCU

![SWD Debug Pins on LQFP-64 version 'Ve2.1S'](/controllers/stm32-t12-oled/Ve2.1S/blue-pcb/rct6-64-pin/debug-pins.jpg)

Most of the other PCB versions tend to have a line of 4 pinx marked up as **SWD** or **C D G V**  on the silkskreen, this is the header for the SWD Debugging Interface. That we wish to connect through.

<a id="finding-the-target-pin-assignments-in-stm32cubemx-tool"></a>
#### Finding the target pin assignments in STM32Cube**MX** Tool

These STM32 microprocessors have partially reassignable pin configurations. However if you open the `.ioc` file in the STM32Cube**IDE**. Then it will open up the **MX** Tool in a sub window.

![Opening MX Tool](/tools/software/STM32CubeIDE/open-ioc-file-STM32CubeMX-from-within-IDE.png)

<a id="connecting-a-hardware-debugger"></a>
## Connecting a hardware Debugger

There are different SWD debuggers / programmers available. Whichever device you have, I also recommend connecting up a **logic analyzer** if you have one. In order to confirm that the device is being activated and is connecting as expected.


You will need to connect to the following pins on your debugger:

* SWDCLK - 1Mhz clock signal that the debugger generates. Clock is only generated whilst the device is actually trying to connect over SWD. If the operation times out then it will appear only briefly.

* SWDIO - This is the single bi-directional data line. In this sense, it is a 1 wire interface like I2C. Devices take turns to put data over the bus. In sync with the 1Mhz default clock speed.

* GND - The 2 devices should ideally be voltage referenced to each other via  acommon Ground. Barring any other grounding constraints. In which case you are on your own.

* NRST (optional) - This is the RESET pin labelled `NRST`, on the STM32F103 MCU. This allows your debugger / programmer to send a reset signal to the device to force it to reboot. Just before starting to talk to it over SWD. Alternatively you can temporarily trigger NRST manually yourself by shorting it to ground with a pair of metal tweezers.

By dragging NRST LOW (0v) then it puts the MCU in a reset state. Which then stops the processor loading up the current firmware on it's integrated flash. And then allows you to bypass any ways the current firmware my attemt to ignore the SWD debugging interface. This NRST reset method is known to work with all STM32 MCUs. Since it gives no time for the firmware a chance to load.

There is also a `+3.3v` output on your programmer device. To bus-power the target devie via the programmer. Do not connect that line. Leave it open because usually the programmer is only able to source enough extra power for just the STM32 MCU itself. And not all the other stuff connected to the +3v3 line on the target device.

Instead you must independantly power the taget device (the STM32 OLED Controller PCB) by connecting it to a +24v DC power source. Then the chip will get enough power on it's +3v3 rail to respond to the SWD queries coming from the debugger device. Which is GND referenced.

<a id="tiao-tumpa-v2-jumper-settings"></a>
#### TIAO TUMPA v2 Jumper settings

The following pin settings were selected on the TUMPA v2 programmer. They are **COLOR** coded with the diagram below:

* [SWD_EN](https://www.tiaowiki.com/w/TIAO_USB_Multi_Protocol_Adapter_User%27s_Manual#SWD_Enable_Jumper)
   * SWD Enabled = ON (**GREEN**)

* [SWD Header](https://www.tiaowiki.com/w/TIAO_USB_Multi_Protocol_Adapter_User%27s_Manual#SWD_Header) (All except `+v3.3` and `SWO`)
  * SWDCLK --> 'C' on stm32 PCB (**YELLOW**)
  * GND --> 'G' on stm32 PCB (**BLACK**)
  * SWDIO --> 'D' on stm32 PCB (**BLUE**)
  * NRST --> to 'NRST' on stm32 MCU (**RED**)

*On my TUMPA:*

![TUMPA Jumber Settings](tiao-tumpa-v2-jumper-settings.png)

<a id="connecting-a-logic-analyzer"></a>
### Connecting a Logic Analyzer

If you have a logic analyzer then also connect it onto the following lines:

* GND --> GND
* SWDCLK --> Connect SWD Clock to a Data channel on the logic analyzer. *Do not connect to the logic analyzer's clock!*
* SWDIO --> Connect SWD Data line to a Data channel on the logic analyzer
* NRST --> Connect the MCU Reset signal to a Data channel on the logic analyzer

**Here are some example traces from the logic analyzer:**

When communication fails because the target device was not powered:

![SWD no response from target](logic-analyzer-trace-swd-no-response-from-target.png)

When communication is successful, because the target device is correctly receiving power:

![SWD successful communications start](logic-analyzer-trace-swd-begin.png)

<a id="connecting-over-swd"></a>
## Connecting over SWD

<a id="with-openocd"></a>
### With OpenOCD

For this section you must first [Install OpenOCD](/tools/software/STM32CubeIDE#install-openocd).

<a id="with-a-tiao-tumpa-v2-hardware-debugger"></a>
#### With a TIAO TUMPA v2 hardware debugger

These `openocd` commands are **specially only for the TUMPA v2** programmer device. If you use a different SWD programmer then it is ***highly likely*** that you will need to run `openocd` with a very different set of configuration options than is being shown here:

If you did not install `openocd` tool system wide. You can run the compiled binary directly from it's source folder with a command like this:

```sh
src/openocd -d4 -s tcl -f interface/ftdi/tumpa.cfg -f interface/ftdi/swd-resistor-hack.cfg -c "transport select swd" -f target/stm32f1x.cfg -c "reset_config srst_only connect_assert_srst"
```

* `-d4` flag - this is an optional extra logging level
* `-s tcl` - this tells `openocd` to look under the `tcl` folder for the latest config files
* `-f interface/ftdi/tumpa.cfg -f interface/ftdi/swd-resistor-hack.cfg` - these flags specific for my TUMPA v2 programmer device.
* `-c "transport select swd"` - tells `openocd` to use the `SWD` transport protocol
* `-f target/stm32f1x.cfg` - tells `openocd` to target the `STM32F1xx` family of processors. Ours is an `F103`.
* -c "reset_config srst_only connect_assert_srst" - this command `reset_config` is being passed 2 further flags. `reset_config` command tells `openocd` to configure certain flags. As follows:
  * `srst_only`, the 1st flag: Tell the programmer to enable its reset pin. Because we have connected the programmer's `NRST` to the `NRST` pin on the target device STM32.
  * `connect_assert_srst`, the 2nd flag. Tell the programmer to hold RESET low (active low) on the NRST line. During the session over SWD protocol. At the end of the session, when you quit `openocd` or finish flashing. Then it will let go of `NRST` and let the target device boot up.

<a id="failed-connection"></a>
#### Failed Connection

If there is a problem communicating. Then most often that will manifest itself as 'no response from the target device'. Here is an example of that response from `openocd` program. I simply turned off the `+24v` supply. So it could not get power.

```sh
θ66° [id:~/.dev/stm32/openocd] master(+0/-0) 130 ± src/openocd -s tcl -f interface/ftdi/tumpa.cfg -f interface/ftdi/swd-resistor-hack.cfg -c "transport select swd" -f target/stm32f1x.cfg -c "reset_config srst_only connect_assert_srst"
Open On-Chip Debugger 0.10.0+dev-01266-gd8ac0086-dirty (2020-05-27-14:47)
Licensed under GNU GPL v2
For bug reports, read
    http://openocd.org/doc/doxygen/bugs.html
none separate

Info : FTDI SWD mode enabled
Warn : Transport "swd" was already selected
swd
srst_only separate srst_nogate srst_push_pull connect_assert_srst

Info : Listening on port 6666 for tcl connections
Info : Listening on port 4444 for telnet connections
Info : clock speed 1000 kHz


θ64° [id:~/.dev/stm32/openocd] master(+0/-0) 1 ± 
```

There is no error message, and `openocd` just exits with a return code of `-1`. However if we append the `-d3` flag. For debug logging level `3`. Then we see an `error code -4` message:

```sh
Debug: 267 5 arm_dap.c:106 dap_init_all(): Initializing all DAPs ...
Debug: 268 5 core.c:636 adapter_system_reset(): SRST line asserted
Debug: 269 5 ftdi.c:1211 ftdi_swd_switch_seq(): JTAG-to-SWD
Debug: 270 5 command.c:626 run_command(): Command 'dap init' failed with error code -4
User : 271 5 command.c:692 command_run_line(): 
Debug: 272 5 command.c:626 run_command(): Command 'init' failed with error code -4
User : 273 5 command.c:692 command_run_line(): 
Debug: 274 5 target.c:1978 target_free_all_working_areas_restore(): freeing all working areas
Debug: 275 5 ftdi.c:1216 ftdi_swd_switch_seq(): SWD-to-JTAG
θ69° [id:~/.dev/stm32/openocd] master(+0/-0) 1 ± 

```

And finally with `-d4` we see:

```sh
Debug: 335 5 ftdi.c:1072 ftdi_swd_run_queue(): Executing 2 queued transactions
Debug: 336 5 mpsse.c:500 mpsse_clock_data():  8 bits
Debug: 337 5 mpsse.c:458 buffer_write_byte(): 19
Debug: 338 5 mpsse.c:458 buffer_write_byte(): 00
Debug: 339 5 mpsse.c:458 buffer_write_byte(): 00
Debug: 340 5 mpsse.c:458 buffer_write_byte(): 00
Debug: 341 5 mpsse.c:857 mpsse_flush(): write 49+1, read 6
Debug: 342 5 mpsse.c:458 buffer_write_byte(): 87
Debug: 343 5 mpsse.c:832 write_cb(): transferred 50 of 50
Debug: 344 5 mpsse.c:834 write_cb():  19 10 00 ff ff ff ff ff ff ff 9e e7 ff ff ff ff ff ff ff 00 19 00 00 a5 29 03 00 2b 05 19 00 00
Debug: 345 5 mpsse.c:834 write_cb():  81 2b 04 19 03 00 1e 00 00 00 1b 00 00 19 00 00 00 87
Debug: 346 5 mpsse.c:794 read_cb():  32 60 ff ff ff ff ff ff
Debug: 347 5 mpsse.c:817 read_cb(): raw chunk 8, transferred 6 of 6
Debug: 348 5 ftdi.c:1098 ftdi_swd_run_queue(): JUNK DP read reg 0 = ffffffff
Debug: 349 5 command.c:626 run_command(): Command 'dap init' failed with error code -4
User : 350 6 command.c:692 command_run_line(): 
Debug: 351 6 command.c:626 run_command(): Command 'init' failed with error code -4
```

This all simply means that OpenOCD tried to establish a connection over SWD protocol. But there was no response from the other end. There was some type of a problem with the communication to the target device.

Failed connection is typically be one of these things:

* Bad wiring of the SWD connection lines. Check them with multimeter.
* The target device is not being powered correctly. Or well enough through it's own independant power supply. Does it have a strong `+3v3` on it's power rails?
* Your hardware programmer device is not configured into the correct communications mode for SWD (if it has jumpers)
* `openocd` program not given appropriate `root` or `udev` permissions on the operating system, to access the USB interface of the USB programmer device. This might have happened if you did not `sudo make install` the openocd program yet. And were trying to run it from the source code folder only.
* Target device is somehow broken. For example has a bad solder joint to pins, or GPIO is burnt out by ESD shock. 

<a id="successful-connection"></a>
#### Successful Connection

If you have established a successful connection, you should see in terminal some output like this:

```sh
θ63° [id:~/.dev/stm32/openocd] master(+0/-0) 130 ± src/openocd -s tcl -f interface/ftdi/tumpa.cfg -f interface/ftdi/swd-resistor-hack.cfg -c "transport select swd" -f target/stm32f1x.cfg -c "reset_config srst_only connect_assert_srst"
Open On-Chip Debugger 0.10.0+dev-01266-gd8ac0086-dirty (2020-05-27-14:47)
Licensed under GNU GPL v2
For bug reports, read
    http://openocd.org/doc/doxygen/bugs.html
none separate

Info : FTDI SWD mode enabled
Warn : Transport "swd" was already selected
swd
srst_only separate srst_nogate srst_push_pull connect_assert_srst

Info : Listening on port 6666 for tcl connections
Info : Listening on port 4444 for telnet connections
Info : clock speed 1000 kHz
Info : SWD DPIDR 0x1ba01477
Info : stm32f1x.cpu: hardware has 6 breakpoints, 4 watchpoints
Info : stm32f1x.cpu: external reset detected
Info : starting gdb server for stm32f1x.cpu on 3333
Info : Listening on port 3333 for gdb connections

```
