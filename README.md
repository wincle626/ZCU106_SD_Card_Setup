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

#### a. set up enviroment: 
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

### 2. Build U-boot

### 3. Build device tree

### 4. Build ARM Trasted Firmware

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
