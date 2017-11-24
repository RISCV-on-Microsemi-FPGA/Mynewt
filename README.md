# Blinky on Mi-V Soft Processors

## Overview
This example project is based on Apache Blinky is a skeleton for Apache Mynewt projects.
To know more about the Apache Mynewt and the Newt build tool, please refer
[Getting Started Guide](http://mynewt.apache.org/os/introduction/).

This example project is the port of Mynewt on Microsemi's Mi-V Soft Processors.
This example projects demonstrates the Mynewt kernel running on Mi-V Soft processor
platform. It runs the simple blinky application which blinks LED on the board.

## Using SoftConsole to Build the project
SoftConsole is Microsemi's  Eclipse based IDE which can be used on Windows as 
well as Linux platforms. 
Fore more details about SoftConsoler, refer [SoftConsole](https://www.microsemi.com/products/fpga-soc/design-resources/design-software/softconsole#downloads)

For this example project we use SoftConsole IDE to develope Mynewt application.

Apache Mynewt uses Newt tool to build the Mynewt sources. However the use of 
Software developement IDEs is also supported.
The page [Using an IDE to Develop Mynewt Applications] http://mynewt.apache.org/faq/ide/
provides a link which describes how to use the Eclipse IDE to develop Mynewt 
applications.

This SoftConsole project is a created as "Makefile project with existing code" 
The sources to be compiled are managed through Mynewt package management systems.

The executable gets generated in microsemi_mynewt_blinky\bin\targets\my_blinky_sim\app\apps\blinky folder

## Creating Debug configuration
1. Select the project in the Project Explorer and from the SoftConsole application 
menu select Run > Debug Configurations...
2. In the Debug Configurations dialog select GDB OpenOCD Debugging and click on 
the New launch configuration button which will create a new debug launch 
configuration for the previously selected project.
3. On the Main tab use brouwse button to choose the blinky.elf created at
<Project root folder >\bin\targets\my_blinky_sim\app\apps\blinky.
4) For a RISC-V target the Debugger tab settings must be configured as follows:

OpenOCD Setup > Config options: 
                    --file board/microsemi-riscv.cfg 
GDB Client Setup > Commands:
                    set mem inaccessible-by-default off 
                    set arch riscv:rv32

## Mi-V Soft processor
This example uses a Mi-V Soft processor MiV_RV32IMA_L1_AHB. The design is 
built for debugging MiV_RV32IMA_L1_AHB through the SmartFusion2 FPGA programming 
JTAG port using a FlashPro5. To achieve this the CoreJTAGDebug IP is used to 
connect to the JTAG port of the MiV_RV32IMA_L1_AHB.

Optionally, The design can be build to use Olimex ARM-USB-TINY-H JTAG probe. 
For this,The JTAG pins must be routed through Fabric to the top level pins.

All the platform/design specific definitions such as peripheral base addresses,
system clock frequency etc. are included in hw_platform.h. The hw_platform.h is 
located at the root folder of this project.

## Target hardware
This example project is targeted at a SmartFusion2 M2S150 advanced development kit
design which has CoreTimer enabled. 
The example project is built using a clock frequency of 83MHz. Trying to execute 
this example project on a different design will result in incorrect baud rate 
being used by CoreUART and timer load value.

This example project can be used with another design using a different clock
configuration. This can be achieved by overwriting the content of this example
project's "hw_platform.h" file with the correct data from your Libero design.

An example design for SmartFusion2 150 Ad. Dev Kit is available at 
[SmartFusion2 150 Ad. Dev Kit](https://github.com/RISCV-on-Microsemi-FPGA/M2S150-Advanced-Dev-Kit/tree/master/Libero/)

