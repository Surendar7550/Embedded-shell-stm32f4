# Embedded Shell (Command Parser) – STM32F446RE :

This project implements a **mini command-line shell** over UART for the STM32F446RE microcontroller using the onboard **PA5 LED**.

##  Project Structure :

Embedded_Shell/
├── Core/
│ ├── Inc/ 
│ ├── Src/ 
│ └── Startup/ 
├── Drivers/
│ └── STM32F4xx_HAL_Driver/ 
│ └── CMSIS/ 
├── Library/ 
│ ├── led_driver.c/h
│ ├── uart_driver.c/h
│ ├── shell.c/h 
├── Debug/ 
├── Embedded_Shell.ioc 
├── STM32F446RETX_FLASH.ld 
├── STM32F446RETX_RAM.ld 

##  Requirements :

- STM32F446RE board (e.g., Nucleo-F446RE)
- Onboard ST-LINK
- UART terminal (e.g., `minicom`, `screen`, `PuTTY`)
- Tools:
  - `st-flash` (`stlink-tools`)
  - `openocd`
  - `arm-none-eabi-gcc` (for rebuild)

##  FLASHING THE BINARY :

Option 1: Using `openocd` :

 ```bash
 cd Debug/
 openocd -f interface/stlink.cfg -f target/stm32f4x.cfg -c "program Embedded_Shell.elf verify reset exit"

Option 2: Using st-flash  (Recommended) :
 1.STMCube/properties/c/Settings/MCU,MPU Postbuild output/
 	->Enable Convert to binary file //Apply and close
 2.~/STM32CubeIDE/Emedded_Shell/Debug$ ls
    Core  Drivers  Embedded_Shell.bin  Embedded_Shell.elf  Embedded_Shell.list  Embedded_Shell.map  Library  makefile  objects.list  objects.mk  sources.mk
 3.flash the file
    st-flash write Embedded_Shell.bin 0x8000000

UART CONNECTION :

 screen /dev/ttyACM0 115200
          # OR
 minicom -b 115200 -D /dev/ttyACM0

UART Settings:

 Baud rate: 115200
 8N1 (8 data bits, no parity, 1 stop bit)
 No flow control

AVAILABLE SHELL COMMANDS
 
 > HELP
Available commands: HELP, LED ON, LED OFF

> LED ON
LED turned ON

> LED OFF
LED turned OFF

>STATUS
LED turned on

OUTPUT :
file:///home/surendar/git/Embedded-shell-stm32f4/output.png
