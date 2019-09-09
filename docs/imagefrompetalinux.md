## Prepare boot image from PetaLinux 

### 1. install PetaLinux 

#### a. Download the petalinux installer 2019.1 

#### b. Execute the installer

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2017-11-57.png)

#### c. Export the petalinux setting

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2017-14-08.png)

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2017-21-36.png)

### 2. Generate board specific project from BSP

#### a. Download the zcu106 BSP 2019.1

#### b. genereate the project

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2017-24-12.png)

### 3. Configure kernel

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2017-26-09.png)

#### a. Disable "General setup -> Initial RAM filesystem and RAM disk"

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2010-26-03.png)

#### b. Enable CPU govenors at "CPU Power Management -> CPU Frequency scaling"

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2010-34-36.png)

#### c. Enable DVFS at "Device Drivers -> Adaptive Voltage Scaling class support" and "Device Drivers -> Generic Dynamic Voltage and Frequency Scaling (DVFS) support"

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2010-35-34.png)

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2010-35-58.png)

#### d. Save configuration
![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2010-42-40.png)

#### e. Import HDF and configure SD card booting

##### Using command "petalinux-config --get-hw-description=<*.hdf>" where *.hdf noramlly is in the vivado project sdk forder. Then select "Image Packaging Configuration->Root file system type->SD card".

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2017-50-54.png)

### 4. Configure u-boot

### 5. Configure root file system (rootfs)

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2017-37-47.png)

#### a. Enable ARM mali kernel library and user driver

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2017-34-58.png)

#### b. Enable HDMI kernel module

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2017-40-49.png)

