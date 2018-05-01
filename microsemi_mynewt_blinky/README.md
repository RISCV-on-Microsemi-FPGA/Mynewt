# Mynewt on Mi-V Soft Processors

## Overview
This example project is based on Apache Blinky which is a skeleton for Apache Mynewt projects.
To know more about the Apache Mynewt and the Newt build tool, refer
[Getting Started Guide](http://mynewt.apache.org/os/introduction/).

This example project is the port of Mynewt on Microsemi's Mi-V Soft Processors.
This example projects demonstrates the Mynewt kernel running on Mi-V Soft processor
platform. It runs the simple blinky application which blinks LED on the board.

## Using SoftConsole to Build the project
SoftConsole is Microsemi's  Eclipse based IDE which can be used on Windows as 
well as Linux platforms. 

For this example project we use SoftConsole IDE to develope Mynewt application.

Apache Mynewt uses Newt tool to build the Mynewt sources. However the use of 
Software developement IDEs is also supported.
The page [Using an IDE to Develop Mynewt Applications](http://mynewt.apache.org/faq/ide/)
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

### Documentation for Microsemi RISC-V processor, SoftConsole toochain, Debug Tools, FPGA design etc.
To know more please refer: [Documentation](https://github.com/RISCV-on-Microsemi-FPGA/Documentation)

### Test Platform and FPGA design:
This project is tested on foloowing hardware platforms:

RISCV-Creative-Board
- [IGLOO2 Creative board Mi-V Sample Design](https://github.com/RISCV-on-Microsemi-FPGA/RISC-V-Creative-Board/Programming_The_Target_Device/PROC_SUBSYSTEM_MIV_RV32IMA_BaseDesign)

PolarFire-Eval-Kit
- [SmartFusion2 Advanced Development Kit RISC-V Sample Design](https://github.com/RISCV-on-Microsemi-FPGA/PolarFire-Eval-Kit/Programming_The_Target_Device\MIV_RV32IMA_L1_AHB_BaseDesign)

M2S150-Advanced-Dev-Kit
- [SmartFusion2 Advanced Development Kit RISC-V Sample Design](https://github.com/RISCV-on-Microsemi-FPGA/M2S150-Advanced-Dev-Kit/Programming_The_Target_Device/PROC_SUBSYSTEM_BaseDesign)

The RISC-V creative board design is running at 66Mhz clock.
The PolarFire Eval Kit design is running at 50Mhz clock.
The SmartFusion2 Adv. Development kit design is running at 83Mhz clock.

You must configure the configure the clocks at followin location in code as per your Libero design: 
apache-mynewt-core\hw\mcu\microsemi\src\ext\riscv_hal\riscv_hal\hw_platform.h
 #define SYS_CLK_FREQ    66000000UL

hw\mcu\microsemi\rv32\src\hal_os_tick.c
 #define RTC_FREQ        66000000UL


### Microsemi SoftConsole Tool-chain:
To know more please refer: [SoftConsole](https://github.com/RISCV-on-Microsemi-FPGA/SoftConsole)
