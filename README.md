# This is the repo of the setting up ZCU106 evaluation kit

## Operation system

### Ubuntu 18.04 LTS

## Tools
### 1. Xilinx Vivado 2019.1

### 2. Xilinx Vivado HLS 2019.1

### 3.Xilinx SDK 2019.1

### 4. Xilinx PetaLinux 2019.1

## Source code

### 1. Linux kernel: https://github.com/Xilinx/linux-xlnx

### 2. U-boot: https://github.com/Xilinx/u-boot-xlnx

### 3. Device tree: https://github.com/Xilinx/device-tree-xlnx.git

### 4. ARM Trusted Firmware: https://github.com/Xilinx/arm-trusted-firmware.git

## Prepare boot SD card from source

### 1. Build Linux kernel

#### a. Set up enviroment

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2010-15-12.png)

#### b. Initiate kernel configuration

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2010-19-29.png)

#### c. Edit kernel configuration

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2010-22-17.png)

##### i. Disable "General setup -> Initial RAM filesystem and RAM disk"

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2010-26-03.png)

##### ii. Enable CPU govenors at "CPU Power Management -> CPU Frequency scaling"

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2010-34-36.png)

##### iii. Enable DVFS at "Device Drivers -> Adaptive Voltage Scaling class support" and "Device Drivers -> Generic Dynamic Voltage and Frequency Scaling (DVFS) support"

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2010-35-34.png)

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2010-35-58.png)

##### iv. Save configuration
![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2010-42-40.png)

#### d. Build kernel

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2010-44-25.png)

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2010-46-21.png)

##### (PS: before build the kernel, modify the device tree "linux-xlnx/arch/arm64/boot/dts/xilinx/zynqmp-zcu106-revA.dts" )

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2010-49-07.png)

### 2. Build U-boot

#### a. Set up enviroment

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2010-56-44.png)

#### b. Initiate u-boot configuration

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2011-04-46.png)

#### c. Build u-boot

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2011-04-14.png)

##### (PS: before build the u-boot, modify the device tree "u-boot-xlnx/arch/arm/dts/zynqmp-zcu106-revA.dts")

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2010-49-07.png)

#### d. Set up the mkimag tool path

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2011-09-38.png)

### 3. Build device tree

#### a. Open a Vivado project by entering "source demo.tcl" in the vivado Tcl console. The block design diagram as shown:

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2011-23-22.png)

This is a simple design without any function on PL. Synthesis, implement the project and generate the bit stream. Export the hardware throught "File -> Export -> Export Hardware ..".

#### b. Generate device tree using SDK

##### i. Open the SDK by "File > Launch SDK".

##### ii. Add device tree soure to BSP repository by "Xilinx Tools > Repositories > New... (select the device tree folder) > OK"

##### iii. Create new board support package project for device tree by "File > New > Board Support Package > Board Support Package OS: device-tree > Finish".

##### iv. Modify the device tree settings by click the "system.mss" then go to "Modify this BSP's Setting". In the "value" field of "device tree -> bootargs", enter "earlycon clk_ignore_unused consoleblank=0 cma=1700M uio_pdrv_genirq.of_id=generic-uio root=/dev/mmcblk0p2 rootfstype=ext4 rw rootwait". 

##### v. Compile the device tree by going to the device tree BSP project folder in terminal and typing in "dtc -I dts -O dtb -o system.dtb system-top.dts".

##### (PS: Actually, when building both linus kernel and u-boot, the device tree is generated at "linux-xlnx/arch/arm64/boot/dts/xilinx/zynqmp-zcu106-revA.dtb" or "u-boot-xlnx/arch/arm/dts/zynqmp-zcu106-revA.dtb")

### 4. Build ARM Trasted Firmware

#### a. Set up eniroment as previous build kernl step

#### b. build the firmware

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2012-05-57.png)

##### The new binary is at "/build/zynqmp/release/bl31/bl31.elf"

### 5. Generate First Stage Boot Loader (FSBL)

### 6. Generate Platform Management Unit Firmware (PMUFW)

### 7. Generate boot binary

### 8. Prepare SD card

## Prepare boot SD card from PetaLinux 

### 1. install PetaLinux 

### 2. Generate board specific project from BSP

### 3. Configure kernel

### 4. Configure root file system (rootfs)


.......
