<p align="center">
  <img src="https://i.imgur.com/hojWghs.png" alt="Giphy.com - Author: Dots" width="250"/>
</p>

A handmade Raspberry Pi OS for a custom dashboard to insert into a Golf GTI '95 dashboard.

## Running the OS
1. Download the ARM Embedded Toolchain (Rasbperry Pi uses ARM architecture) here https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads;
2. Extract your ARM directory with `tar -xf FOLDER_NAME`;
3. Install QEMU (VM) to run the kernel like an Raspberry Pi `sudo apt-get install qemu`;
4. After installing QEMU, install it's dependencies running `apt-get install zlib1g-dev build-essential zlib1g-dev pkg-config libglib2.0-dev binutils-dev libboost-all-dev autoconf libtool libssl-dev libpixman-1-dev libpython-dev python-pip python-capstone virtualenv`;
5. Test your QEMU installation with `qemu-system-arm --version`;
6. Clone this repository;
7. Create a folder called `build`;
8. Run the following commands: `./YOUR_DOWNLOADED_GCC_FOLDER/bin/arm-none-eabi-gcc -mcpu=cortex-a7 -fpic -ffreestanding -c ./src/boot.S -o ./build/boot.o && ./YOUR_DOWNLOADED_GCC_FOLDER/bin/arm-none-eabi-gcc -mcpu=cortex-a7 -fpic -ffreestanding -std=gnu99 -c ./src/kernel.c -o ./build/kernel.o -O2 -Wall -Wextra && ./YOUR_DOWNLOADED_GCC_FOLDER/bin/arm-none-eabi-gcc -T ./src/linker.ld -o ./build/myos.elf -ffreestanding -O2 -nostdlib ./build/boot.o ./build/kernel.o`;
9. Now run your VM with QEMU using `qemu-system-arm -m 256 -M raspi2 -serial stdio -kernel ./build/myos.elf`