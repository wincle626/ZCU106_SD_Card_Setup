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

##### i. Disable "General setup -> Initial RAM filesystem and RAM disk"

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2010-26-03.png)

##### ii. Enable CPU govenors at "CPU Power Management -> CPU Frequency scaling"

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2010-34-36.png)

##### iii. Enable DVFS at "Device Drivers -> Adaptive Voltage Scaling class support" and "Device Drivers -> Generic Dynamic Voltage and Frequency Scaling (DVFS) support"

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2010-35-34.png)

![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2010-35-58.png)

##### iv. Save configuration
![alt text](https://github.com/wincle626/ZCU106_Setup/blob/master/pics/Screenshot%20from%202019-09-09%2010-42-40.png)

### 4. Configure u-boot

### 4. Configure root file system (rootfs)
