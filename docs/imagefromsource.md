## Prepare boot image from source

### 1. Build u-boot

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

### 2. Build Linux kernel

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

#### e. Build u-boot kernel image with command "mkimage -n 'Kernel Image' -A arm64 -O linux -C none -T kernel -a 0x8000 -e 0x8000 -d Image uImage"

### 3. Build device tree

#### a. Open a Vivado project by entering "source demo.tcl" in the vivado Tcl console. The block design diagram as shown:

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2011-23-22.png)

This is a simple design without any function on PL. Synthesis, implement the project and generate the bit stream. Export the hardware throught "File -> Export -> Export Hardware ..".

#### b. Generate device tree using SDK

##### i. Open the SDK by "File > Launch SDK".

##### ii. Add device tree soure to BSP repository by "Xilinx Tools > Repositories > New... (select the device tree folder) > OK"

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2014-35-58.png)

##### iii. Create new board support package project for device tree by "File > New > Board Support Package > Board Support Package OS: device-tree > Finish".

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2014-37-53.png)

##### iv. Modify the device tree settings by click the "system.mss" then go to "Modify this BSP's Setting". In the "value" field of "device tree -> bootargs", enter "earlycon clk_ignore_unused consoleblank=0 cma=1700M uio_pdrv_genirq.of_id=generic-uio root=/dev/mmcblk0p2 rootfstype=ext4 rw rootwait". 

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2014-38-16.png)

##### v. Compile the device tree by going to the device tree BSP project folder in terminal and typing in "dtc -I dts -O dtb -o system.dtb system-top.dts".

##### (PS: Actually, when building both linus kernel and u-boot, the device tree is generated at "linux-xlnx/arch/arm64/boot/dts/xilinx/zynqmp-zcu106-revA.dtb" or "u-boot-xlnx/arch/arm/dts/zynqmp-zcu106-revA.dtb")

### 4. Build ARM Trasted Firmware

#### a. Set up eniroment as previous build kernel step

#### b. build the firmware

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2012-05-57.png)

##### The new binary is at "/build/zynqmp/release/bl31/bl31.elf"

### 5. Generate First Stage Boot Loader (FSBL)

#### a. Launch Xilinx SDK as previous mentioned through Vivado. 

#### b. Create a new project called "fsbl" by "File -> New ... Application Project (standalone) ". Click "Next" and choosing the "Zynq MP FSBL" template and click "Finish" to build the project. The fsbl.elf will be created under the compiled folder.

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2014-40-33.png)

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2014-40-46.png)

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2014-42-35.png)

### 6. Generate Platform Management Unit Firmware (PMUFW)

#### a. Launch Xilinx SDK as previous mentioned through Vivado. 

#### b. Create a new project called "pmufw" by "File -> New ... Application Project (standalone)". Choose "Target Hardware - Processor - psu_pmu_0" in the tab. Click the "Next", choose the "ZynqMP PMU Firmware" template and click "Finish" to build the project. The "pmufw.elf" will be created under the compiled folder. 

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2014-44-15.png)

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2014-44-33.png)

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2014-44-48.png)


### 7. Generate boot binary

#### a. Create "Boot.bin"

![alt text](https://github.com/wincle626/ZCU106_SD_Card_Setup/blob/master/pics/Screenshot%20from%202019-09-10%2012-01-35.png)

#### b. Create "Image.ub"

![alt text](https://github.com/wincle626/ZCU106_SD_Card_Setup/blob/master/pics/Screenshot%20from%202019-09-10%2017-49-44.png)
