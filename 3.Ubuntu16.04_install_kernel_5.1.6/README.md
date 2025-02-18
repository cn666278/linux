<p align="center">
<img src="https://github.com/niehmanyo/linux/blob/main/3.Ubuntu16.04_install_kernel_5.1.6/linux_img.png">
</p>

# Install Linux Kernel 5.1.6 in Ubuntu 16.04

<p><b>⚠️Warming</b>: If the Ubuntu version is 20.04, then it would be a failure in installation</p>
<p>❤Thanks to this <a href="https://www.cyberciti.biz/tips/compiling-linux-kernel-26.html">How to compile and install Linux Kernel 5.16.9 from source code</a> </p>


|Ubuntu|Kernel|Course|Group|
|-------|-----|-----|-----|
|16.04|5.1.6|CST308 Operating System|<p>Nie Wenyu CST1909148</p><p>Zhu Qijin CST1909173</p><p>Chen Nuo CST1909128</p><p>Zhang Wei CST1909168</p><p>Yao Lan CST1909161</p>|

## 1. Installation
<p>Using this command to check the version of your ubuntu</p>

```bash
uname -r  ##check the version
wget https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.1.6.tar.xz 
## Get the tar.xz file,my version is 5.1.64
## Or you can download this file in the website,I put it in my /home.
unxz -v linux-5.1.6.tar.xz ## To extract the source code.
```
<p> <img src="https://github.com/niehmanyo/linux/blob/main/3.Ubuntu16.04_install_kernel_5.1.6/1.png"> </p>


```bash 
wget https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.1.6.tar.sign ## Download this file,then get the PGP signature
gpg --verify linux-5.1.6.tar.sign ## To get the key
gpg --recv-keys "your key-ID"	## Enter the key you receive, usually there is no problem
gpg --verify linux-5.1.6.tar.sign ## Verify it again							  
```

<p>Here are problems: </p>

* keyserver_receive failed: bad URI
* 

[Problems](#2.Problems)


<p>I noticed that the key is 6092693E,but when I enter</p>
<p> <img src="https://github.com/niehmanyo/linux/blob/main/3.Ubuntu16.04_install_kernel_5.1.6/2.png"> </p>
<p> <img src="https://github.com/niehmanyo/linux/blob/main/3.Ubuntu16.04_install_kernel_5.1.6/3.png"> </p>
<p> <img src="https://github.com/niehmanyo/linux/blob/main/3.Ubuntu16.04_install_kernel_5.1.6/4.png"> </p>
<p> <img src="https://github.com/niehmanyo/linux/blob/main/3.Ubuntu16.04_install_kernel_5.1.6/5.png"> </p>

<p><b>Sample output:</b></p>
<p> <img src="https://github.com/niehmanyo/linux/blob/main/3.Ubuntu16.04_install_kernel_5.1.6/6.png"> </p>

<p>Now,we get the "linux-5.1.6.tar" file. Then untar this tarball.</p>

```bash
tar xvf linux-5.1.6.tar

```
<p>Here we get this dic "linux-5.1.6"</p>
<p>Before start building the kernel,one must configure Linux kernel features.Then copy existing config file from your /boot</p>

<p> <img src="https://github.com/niehmanyo/linux/blob/main/3.Ubuntu16.04_install_kernel_5.1.6/7.png"> </p>

```bash
cp -v /boot/config-$(uname -r) .config ##copy the your configuration file to this linux dic

##my sample output
'/boot/config-4.15.0-112-generic'  ->  '.config'

```

<p> <img src="https://github.com/niehmanyo/linux/blob/main/3.Ubuntu16.04_install_kernel_5.1.6/8.png"> </p>


```bash
sudo vim .config  ## to see the .config file (optional)
sudo apt-get install build-essential libncurses-dev bison flex libssl-dev libelf-dev
## this package help to compile kernel
```
<p><a href="https://www.cyberciti.biz/tips/linux-debian-package-management-cheat-sheet.html?utm_source=Linux_Unix_Command&utm_medium=tips&utm_campaign=nixcmd">For more information about "apt-get" command </a></p>


<p> <img src="https://github.com/niehmanyo/linux/blob/main/3.Ubuntu16.04_install_kernel_5.1.6/9.png"></p>
<p> <img src="https://github.com/niehmanyo/linux/blob/main/3.Ubuntu16.04_install_kernel_5.1.6/10.png"> </p>

<p>After installing these package</p>

```bash
make menuconfig ## Start the kernel configuraion 
```
<p>Sample out after makeing, this is an menu then you can see some details about configuration. Also you can exit it, then the terminal will show '*** Execute 'make' to start the build '</p>
<p> <img src="https://github.com/niehmanyo/linux/blob/main/3.Ubuntu16.04_install_kernel_5.1.6/11.png"> </p>
<p> <img src="https://github.com/niehmanyo/linux/blob/main/3.Ubuntu16.04_install_kernel_5.1.6/make_menuc.png"> </p>


<p>Start compiling, just use 'make'; or to speed up time, use 'make -j $(nproc)'</p>
<p>It will take a lot of time</p>

```bash
## my cpu core is 4 becasue I set 4
make -j 4 ## Start to compile
```


<p> <img src="https://github.com/niehmanyo/linux/blob/main/3.Ubuntu16.04_install_kernel_5.1.6/12.png"> </p>
<p> <img src="https://github.com/niehmanyo/linux/blob/main/3.Ubuntu16.04_install_kernel_5.1.6/process1.png"> </p>
<p> <img src="https://github.com/niehmanyo/linux/blob/main/3.Ubuntu16.04_install_kernel_5.1.6/process2.png"> </p>
<p>Install the Linux kernel modules</p>

```bash
## Now using this command
sudo make modules_install
```
 <p>After installing kernel modules, you will see the version of your kernel in the last</p>
<p> <img src="https://github.com/niehmanyo/linux/blob/main/3.Ubuntu16.04_install_kernel_5.1.6/modules_install.png"> </p>

<p>Then I use 'uname -r' to see the version,luckily it is 4.15.0.😑 Because I have not compiled the kernel and the modules.</p>


```bash
sudo make install ## last part
```
<p><b>Sample output</b></p>
<p> <img src="https://github.com/niehmanyo/linux/blob/main/3.Ubuntu16.04_install_kernel_5.1.6/13.png"> </p>

```bash
ls -a /boot ## To see all files in /boot
```

<p><b>Now there have 4 kernel_5.1.6 files:</b></p>
<p><b>initrd.img-5.1.6</b></p>
<p><b>System.map-5.1.6</b></p>
<p><b>config-5.1.6</b></p>
<p><b>vmlinuz-5.1.6</b></p>

<p> <img src="https://github.com/niehmanyo/linux/blob/main/3.Ubuntu16.04_install_kernel_5.1.6/14.png"> </p>

<p>Now,everything is ready and then upgrade grub.</p>

```bash
sudo update-initramfs -c -k 5.1.6
sudo update-grub

```

<p> <img src="https://github.com/niehmanyo/linux/blob/main/3.Ubuntu16.04_install_kernel_5.1.6/15.png"> </p>


```bash
## After finishing, reboot ubuntu
reboot
## ...A few minutes later

uname -r
## you will see your version 😁
```

<p> <img src="https://github.com/niehmanyo/linux/blob/main/3.Ubuntu16.04_install_kernel_5.1.6/16.png"> </p>


## 2.Problems 