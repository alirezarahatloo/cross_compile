# cross_compile

/* 		CROSSTOOL-NG		*/
 //don't use mkdir with sudo user
 //don't use sudo 
 
 
git clone https://github.com/crosstool-ng/crosstool-ng

cd crosstool-ng/

sudo ./bootstrap

sudo ./configure --enable-local

make

./ct-ng list-samples

./ct-ng aarch64-rpi4-linux-gnu

./ct-ng build

export PATH=/home/alireza/x-tools/aarch64-rpi4-linux-gnu/bin/:$PATH

#if
aarch64-rpi4-linux-gnu-gcc hello.c --static

qemu-aarch64 a.out

else

aarch64-rpi4-linux-gnu-gcc hello.c

qemu-aarch64 -L $(aarch64-rpi4-linux-gnu-gcc -print-sysroot) ./a.out 

qemu-aarch64 ./a.out 




/*  U_BOOT  */

cd u-boot-v2022.10

ls configs | grep rpi

export PATH=/home/alireza/x-tools/aarch64-rpi4-linux-gnu/bin/:$PATH

export CROSS_COMPILE=aarch64-rpi4-linux-gnu-

make rpi_4_defconfig

sudo apt-get install libssl-dev

make -j4

sudo umount /media/alireza/*

sudo dd if=/dev/zero of=/dev/mmcblk0 bs=512 count=1

sudo cfdisk /dev/mmcblk0 	///partition open black page and select dos and write size for example 300M id=c type = W95 FAT32

sudo mount /dev/mmcblk0p1 /mnt

cp u-boot.bin /mnt 
