# WyresRIOT :: Documentation
Docs for the porting of Wyres boards on RIOT

## MyNewT repository
* https://mynewt.apache.org/
* https://github.com/wyres 
* https://github.com/wyres/mynewt-generic-app 
* Application pour les cages à marmotte https://github.com/wyres/mynewt_app_wproto_marmotte 

## Caractéristiques des 2 cartes

### WPROTO
https://github.com/wyres/mynewt-wproto-bsp

    Objective : support W_PROTO card on MyNewt 1.7.0 Card hardware:
    STM32L151CC MCU
    256kb flash / 32kb RAM / 8kb PROM : MCU based
    UART(1) : MCU based : external grove connector
    SPI(2) : MCU based : 1 dedicated for radio, 1 on header
    I2C(1) : MCU based : external grove connector
    Accelero : XX via I2C → MMA7660 https://www.nxp.com/docs/en/data-sheet/MMA7660FC.pdf
    Altimeter : XX via I2C → MPL3115A2 → Driver RIOT 
    MEMS microphone on I2S bus (     http://www.jhearing.com/web2/docs/SPH0641LM4H-1%20latest%20edits%20Rev%2012.pdf )
    Semtech Lora radio SX1272 on SPI bus
    2 LEDs via GPIO on-board and via header
    1 'power' PWM GPIO (mosfet switched) on header (Speaker AST-01708MR-R https://www.puiaudio.com/media/SpecSheet/AST-01708MR-R.pdf )
    2 GPIO on header
    Functionality configurable/initialised in BSP
    UART :
    UART0 : 1 -> creates 'uart0' device : 'real' UART1 of STM32 connected to grove header
    UARTDBG : 1 -> creates 'uartdbg' s/w bitbang uart on any gpio for debug log output only (19200 baud only)
    recommended pin : button input header (PB3)
    Periphs
    TIMER1 : 1 -> used as os timer @1MHz frequency
    I2C1 : 1 -> enables I2C1 in STM32, creates HAL device for 'i2c0', creates devices for accelero and altimeter
    SPI_0_MASTER : 1 -> creates SPI1 in STM32, creates 'spi0' device for SX1272
    Flash layout
    16Kb : bootloader (mcuboot recommended)
    100Kb x 2 : 2 image slots



### WBASE_V2
    https://github.com/wyres/mynewt-wbasev2-bsp 
    BSP for Wyres "W_BASE" card
    Objective : support Wyres W_BASE cards on MyNewt 1.7.0
    v2 revB (SX1272, RF switch old)
    v2 revC/D (SX1272, RF switch Skynet new))
    v3 revA/B (SX1261/2)
    Card hardware:
    STM32L151CC MCU → https://github.com/RIOT-OS/RIOT/blob/73ccd1e2e721bee38f958f8906ac32e5e1fceb0c/cpu/stm32/kconfigs/l1/Kconfig.models#L65 
    256kb flash / 32kb RAM / 8kb EEPROM : MCU based
    UART(1) : MCU based : external grove connector
    SPI(2) : MCU based : 1 dedicated for radio, 1 on header
    I2C(1) : MCU based : external grove connector
    Accelero : ST LIS2DE12 via I2C → Driver RIOT 
    Altimeter : ST LPS22HB via I2C https://github.com/RIOT-OS/RIOT/tree/master/drivers/lpsxxx 
    light sensitive trans. on GPIO KPS-3227SP1C https://www.tme.eu/Document/e553ef252ee57f18cff7eba7ee94fbeb/KPS-3227SP1C%28Ver.9%29.pdf 
    MEMS microphone on I2S bus (SPH0641LM4H-1 http://www.jhearing.com/web2/docs/SPH0641LM4H-1%20latest%20edits%20Rev%2012.pdf )
    Semtech Lora radio SX1272 on SPI bus
    2 LEDs via GPIO on-board and via header
    1 'power' PWM GPIO (mosfet switched) on header
    1 'button' GPIO input with limiter resistance on header
    1 GPIO on header
    Functionality configurable/initialised in BSP
    UART :
    UART0 : 1 -> creates 'uart0' device : 'real' UART1 of STM32 connected to grove header
    UARTDBG : 1 -> creates 'uartdbg' s/w bitbang uart on any gpio for debug log output only (19200 baud only)
    recommended pin : button input header (PB3)
    Periphs
    TIMER1 : 1 -> used as os timer @1MHz frequency
    I2C_0 : 1 -> enables I2C1 in STM32, creates HAL device for 'i2c0', creates devices for accelero and altimeter
    SPI_0_MASTER : 1 -> creates SPI1 in STM32, creates 'spi0' device for SX1272
    Flash principal blocks
    16Kb : bootloader (mcuboot recommended)
    160Kb x 1 : main application image slot
    32Kb x 1 : FOTA application slot

## RIOT Drivers

* https://github.com/RIOT-OS/RIOT/tree/master/drivers/mpl3115a2
* https://github.com/RIOT-OS/RIOT/tree/master/drivers/mma7660 
* Accelerometer : ST LIS2DE12 https://github.com/RIOT-OS/RIOT/tree/master/drivers/lis2dh12 
* Altimeter : ST LPS22HB https://github.com/RIOT-OS/RIOT/tree/master/drivers/lpsxxx 

## Portage des cartes
Lire Portage de la board (et surtout Boards outside of RIOTBASE)
https://doc.riot-os.org/porting-boards.html 

## WPROTO

[Repository](https://github.com/WyresRIOT/wyres_proto_rev1a)

## WBASE_V2

[Repository](https://github.com/WyresRIOT/wyres_wbase_v2)

