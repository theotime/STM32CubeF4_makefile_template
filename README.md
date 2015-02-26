# STM32CubeF4 Makefile template #

STM32F4-DISCOVERY Makefile template for linux. Should work for other board.

## Install Toolchain (Debian/Ubuntu) ##
```
sudo add-apt-repository -y ppa:terry.guo/gcc-arm-embedded
sudo apt-get update
sudo apt-get -y install gcc-arm-none-eabi gdb-arm-none-eabi binutils-arm-none-eabi openocd
```

## STM32CubeMX ##

This tool is not mandatory to dev on STM32 boards. You need java to run it.
Download STM32CubeMX from [STM32 website](http://www.st.com/web/catalog/tools/FM147/CL1794/SC961/SS1533/PF259242?sc=stm32cube#)

```
unzip stm32cubemx.zip
java -jar SetupSTM32CubeMX-4.6.0.exe
java -jar /usr/local/STMicroelectronics/STM32Cube/STM32CubeMX/STM32CubeMX.exe
```

## Using STM32CubeF4 ##

  * [Get the sources](http://www.st.com/web/catalog/tools/FM147/CL1794/SC961/SS1743/PF259243#). Download it, extract it and copy in your favorite folder (eg. /opt/).
  * Documentation
    * [UM1730 - Getting started with STM32CubeF4 firmware package for STM32F4xx series](http://www.st.com/st-web-ui/static/active/en/resource/technical/document/user_manual/DM00107720.pdf)
    * [UM1472 - Discovery kit for STM32F407/417 lines](http://www.st.com/st-web-ui/static/active/en/resource/technical/document/user_manual/DM00039084.pdf)
    * [UM1725 - Description of STM32F4xx HAL drivers](http://www.st.com/st-web-ui/static/active/en/resource/technical/document/user_manual/DM00105879.pdf)
    * [PM0214 - STM32F3 and STM32F4 Series Cortex®-M4 programming manual](http://www.st.com/web/en/resource/technical/document/programming_manual/DM00046982.pdf)
    * [RM0090 - STM32F405xx/07xx, STM32F415xx/17xx, STM32F42xxx and STM32F43xxx advanced ARM®-based 32-bit MCUs](http://www.st.com/web/en/resource/technical/document/reference_manual/DM00031020.pdf)
    * BSP : STM32Cube_FW_F4_V1.4.0/Drivers/BSP/STM32F4-Discovery/
```
debian@debian:/opt/STM32Cube_FW_F4_V1.4.0/Drivers/BSP/STM32F4-Discovery$ ls *.h
stm32f4_discovery_accelerometer.h  stm32f4_discovery.h
stm32f4_discovery_audio.h
```

  * Mandatory files to start a project (Copy from STM32CubeF4 to current directory)
    * **startup_stm32f407xx.s** (/opt/STM32Cube_FW_F4_V1.4.0/Projects/STM32F4-Discovery/Templates/TrueSTUDIO)
    * **system_stm32f4xx.c** (/opt/STM32Cube_FW_F4_V1.4.0/Projects/STM32F4-Discovery/Templates/Src)
    * **STM32F407VG_FLASH.ld** (/opt/STM32Cube_FW_F4_V1.4.0/Projects/STM32F4-Discovery/Templates/TrueSTUDIO/STM32F4-Discovery)
    * **stm32f4xx_hal_conf.h** (/opt/STM32Cube_FW_F4_V1.4.0/Projects/STM32F4-Discovery/Templates/Inc)
  * Source code to test the makefile (Copy into the current directory) :
    * /opt/STM32Cube_FW_F4_V1.4.0/Projects/STM32F4-Discovery/Templates/Src
    * /opt/STM32Cube_FW_F4_V1.4.0/Projects/STM32F4-Discovery/Templates/Inc
    
Change the sources, path & informations for your board into the Makefile
```
SRCS=main.c stm32f4xx_it.c stm32f4xx_hal_msp.c system_stm32f4xx.c
SRCS += startup_stm32f407xx.s

# Binaries will be generated with this name (.elf, .bin, .hex, etc)
PROJ_NAME=main

# Path
STM_COMMON=/opt/STM32Cube_FW_F4_V1.4.0

# Board/MCU
STM_SERIE=STM32F4XX
STM_MODEL=STM32F407xx
BSP_MODEL=STM32F4-Discovery
```

For some examples, the GPIO_EXTI ig, you should add specific BSP files : 
```
SRCS += stm32f4_discovery.c # LEDs, Button
SRCS += stm32f4_discovery_accelerometer.c # Accelerometer
SRCS += stm32f4_discovery_audio.c # Audio
```


Then:
```
make
```

To flash the device, use openocd, with the STM32F4-Discovery configuration (for the f4discovery board):
```
openocd -f /usr/share/openocd/scripts/board/stm32f4discovery.cfg
```

The openocd daemon is now listening. On another terminal, start a telnet session:
```
$ telnet localhost 4444
> reset halt
> flash write_image erase main.hex
> reset run
> shutdown
```


Project based on [tomvdb's work](https://github.com/tomvdb/stm32f401-nucleo-basic-template)
