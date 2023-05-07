# SmartBatteryHack_Toshiba_Portage_T210

battery pack was dead hard after 4 years used since yesr 2011, battery cells had removed, housing of  battery pack retianed more than 10 years with reason that retained as support and base for the notebook but the battery will never service or charging again.

Today year 2023 the price to replace a T210 battery pack is about 100RMB less by Taobao/Aliexpress, so why would do a hack or try to renew the cells ?! FOR FUN and to learn to how.

### ref and fork 
https://boundarycondition.home.blog/2020/01/18/the-repairing-and-hacking-of-a-dell-j1knd-bq8050-laptop-battery/  
https://github.com/xiaolaba/SmartBatteryHack  

### the last activiy about Smart Battery  
https://github.com/xiaolaba/ATmega406-SPHDV20

### find pinout of Toshiba_T210_battery_PA3820U  
this is data sheet and the hints  

![Toshiba_T210_battery_PA3820U/Toshiba_T210_battery_pintout.PNG](Toshiba_T210_battery_PA3820U/Toshiba_T210_battery_pintout.PNG)  
![Toshiba_T210_battery_PA3820U/TOSHIBA_PA3820U.PNG](Toshiba_T210_battery_PA3820U/TOSHIBA_PA3820U.PNG)  

### download source code from the forked repo  
https://github.com/xiaolaba/SmartBatteryHack


### arduino code modification, I have Nano with Atmega168P only
add support and code altered, same pinout for 168/328 and thus the Nano hardware pinput of Nano.
```
// xiaolaba, 2023-04-30, add 168P support
// name:     SCL  SDA
// port pin: PC5  PC4
// pin#:     28   27    // DIP28/TQFP32/QFN32,  Atmega168P/328P, 
//           24   23    // QFN28
//           D19  D18   // Arduino Nano
//           A5   A4    // Arduino Nano 
#elif defined (__AVR_ATmega168P__) || defined (__AVR_ATmega168__) // Arduino Nano with 168 MCU, hardware I2C pins
    #define SDA_PORT PORTC
    #define SDA_PIN 4
    #define SCL_PORT PORTC
    #define SCL_PIN 5
```

This is SDA/SCL lines,

![Atmega168_328_datasheet/avr_sda_scl.PNG](Atmega168_328_datasheet/avr_sda_scl.PNG)  
![Atmega168_328_datasheet/nano_sda_scl.PNG](Atmega168_328_datasheet/nano_sda_scl.PNG)  


### PC software / MCU firmware, precompiled and testing, no battery connection is required  
testing the communication of PC/MCU, ok  
![Firmware_Hostware/PC_software/connected.PNG](Firmware_Hostware/PC_software/connected.PNG)

sign the C# PC software for installation and expireation date till 2027  
![Firmware_Hostware/PC_software/sign.PNG](Firmware_Hostware/PC_software/sign.PNG)

path of the software release,  
[Firmware_Hostware/PC_software](Firmware_Hostware/PC_software)  
[Firmware_Hostware/MCU_firmware](Firmware_Hostware/MCU_firmware)  



### battery pack info.  
there is another project used for gather the pack info  
see this, https://github.com/ArminJo/Smart-Battery-Module-Info_For_Arduino/  
as becasue no LCD2004 and test rig only available with LCD1602V2-P6, so other project and modified code is used.  
```
Smart-Battery-Module-Info_For_Arduino-master\SBMInfo\SBMInfo.ino
Version 4.1 from May  7 2023
Configured to stop discharge at 3300 mV
No LiPo supply detected -> fast display timing
Found I2C device at 0x0B

*** STATIC INFO ***
Battery mode                        0x6101 | 0b110000100000001
                                    - Internal Charge Controller Supported
                                    - Battery OK
                                    - Charge Controller Enabled
                                    - Disable AlarmWarning broadcast to Host and Smart Battery Charger
                                    - Disable broadcasts of ChargingVoltage and ChargingCurrent to Smart Battery Charger

Manufacturer Name                   SONY
Chemistry                           LION
Manufacturer Data                   0x6 D5 B 83 5 A 21 7 0 1 0 0 0 
Device Name                         NS2P3SZTL4WR
Serial number                       923 | 0x39B
Manufacture date (YYYY-MM-DD)       2010-12-26
Design voltage                      10.800 V
Design capacity                     0 mAh
Charging current                    0 mA
Charging voltage                    0.000 V
SBM protocol (Version / Revision)   1.1 with optional PEC support / 1
Cycle count                         488

Max error of charge calculation     0%
Remaining time alarm                0 min
Remaining capacity alarm            0 mAh

*** MANUFACTURER INFO ***
Device Type                         43274 | 0xA90A

*** RATE TEST INFO ***
Setting AT rate to                  100 mA
TimeToFull at rate                  0 min
Setting AT rate to                  -100 mA
TimeToEmpty at rate                 0 min
Can be delivered for 10 seconds at rate  0 | 0x0

*** DYNAMIC INFO ***
Relative charge                     0%
Absolute charge                     0%
Full charge capacity                0 mAh = 255%
Remaining capacity                  0 mAh
Voltage                             11.925 V
Current                             0 mA
Average current of last minute      0 mA
Temperature                         34.35 C
Minutes remaining until empty       0 min
Average minutes remaining until empty  0 min
Minutes remaining for full charge   0 min
Battery status (BIN)                0x0 | 0b0

Pack config and status              0x624 | 0b11000100100
                                    - Pack not inserted
                                    - Voltage > EDV2
                                    - Pack sealed


*** DYNAMIC NON STANDARD INFO ***
Cell 1 Voltage                      3.709 V
Cell 2 Voltage                      4.119 V
Cell 3 Voltage                      4.098 V
Cell 4 Voltage                      0x0
State of Health                     1808 | 0x710

*** CHANGED VALUES ***
Temperature                         34.15 C

```
