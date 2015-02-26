# STM32CubeF4 Makefile template #

STM32F4-DISCOVERY Makefile template for linux.

## Install Debian/ubuntu ##
```
sudo add-apt-repository -y ppa:terry.guo/gcc-arm-embedded
sudo apt-get update
sudo apt-get -y install gcc-arm-none-eabi gdb-arm-none-eabi binutils-arm-none-eabi
```

## STM32CubeMX ##

You need java to run it.
Download STM32CubeMX from [STM website](http://www.st.com/web/catalog/tools/FM147/CL1794/SC961/SS1533/PF259242?sc=stm32cube#)

```
unzip stm32cubemx.zip
java -jar SetupSTM32CubeMX-4.6.0.exe
java -jar /usr/local/STMicroelectronics/STM32Cube/STM32CubeMX/STM32CubeMX.exe
```

## Using STM32CubeF4 ##

  * [Get the sources](http://www.st.com/web/catalog/tools/FM147/CL1794/SC961/SS1743/PF259243#). Download it and copy where you want (eg. /opt/).
  * Documentation
    * [UM1730 - Getting started with STM32CubeF4 firmware package for STM32F4xx series](http://www.st.com/st-web-ui/static/active/en/resource/technical/document/user_manual/DM00107720.pdf)
    * [UM1472 - Discovery kit for STM32F407/417 lines](http://www.st.com/st-web-ui/static/active/en/resource/technical/document/user_manual/DM00039084.pdf)
    * [UM1725 - Description of STM32F4xx HAL drivers](http://www.st.com/st-web-ui/static/active/en/resource/technical/document/user_manual/DM00105879.pdf)
    * [PM0214 - STM32F3 and STM32F4 Series Cortex®-M4 programming manual](http://www.st.com/web/en/resource/technical/document/programming_manual/DM00046982.pdf)
    * BSP : STM32Cube_FW_F4_V1.4.0/Drivers/BSP/STM32F4-Discovery/
```
debian@debian:/opt/STM32Cube_FW_F4_V1.4.0/Drivers/BSP/STM32F4-Discovery$ ls *.h
stm32f4_discovery_accelerometer.h  stm32f4_discovery.h
stm32f4_discovery_audio.h
```

  * Mandatory files to start a project (To copy from STM32CubeF4)
    * **startup_stm32f407xx.s** (/opt/STM32Cube_FW_F4_V1.4.0/Projects/STM32F4-Discovery/Templates/TrueSTUDIO)
    * **system_stm32f4xx.c** (/opt/STM32Cube_FW_F4_V1.4.0/Projects/STM32F4-Discovery/Templates/Src)
    * **STM32F407VG_FLASH.ld** (/opt/STM32Cube_FW_F4_V1.4.0/Projects/STM32F4-Discovery/Templates/TrueSTUDIO/STM32F4-Discovery)
    * **stm32f4xx_hal_conf.h** (/opt/STM32Cube_FW_F4_V1.4.0/Projects/STM32F4-Discovery/Templates/Inc)
  * Source code to test the makefile (copy into the current directory) :
    * /opt/STM32Cube_FW_F4_V1.4.0/Projects/STM32F4-Discovery/Templates/Src
    * /opt/STM32Cube_FW_F4_V1.4.0/Projects/STM32F4-Discovery/Templates/Inc
    
Change the path & information for your board into the Makefile
```
STM_COMMON=/opt/STM32Cube_FW_F4_V1.4.0
STM_SERIE=STM32F4XX
STM_MODEL=STM32F407xx
```

Then:
```
make
```


