ifeq ($(KERNELRELEASE),)  

#########################################
# To support cross-compiling for the ARM:
# For ARM, invoke make as:
# make ARCH=arm CROSS_COMPILE=arm-none-linux-gnueabi- 
# (or whatever CROSS_COMPILE should be...)
ifeq ($(ARCH),arm)
   # *UPDATE* 'KDIR' below to point to the ARM Linux kernel source tree
   KDIR ?= ~/3.18.22-arm-tags
   #KDIR ?= ~/DG-L3/RPi/kernel_RPi/linux-3.6.11-rpi
   #KDIR ?= ~/DG-L3/pandaboard/custom/kernel/linux-3.1.5
else
   KDIR ?= /lib/modules/$(shell uname -r)/build 
endif
#########################################

PWD := $(shell pwd)  

.PHONY: build clean  

build:
	$(MAKE) -Wall -C $(KDIR) M=$(PWD) modules
install:
	$(MAKE) -C $(KDIR) M=$(PWD) modules_install
clean:
	$(MAKE) -C $(KDIR) M=$(PWD) clean

else

$(info Building with ARCH=${ARCH} and KERNELRELEASE=${KERNELRELEASE})

# Uncomment the -DDEBUG_PRINT directive to actiavte the 'MSG' macro...
EXTRA_CFLAGS += -g -ggdb -DDEBUG_PRINT #-DUSE_FTRACE_PRINT

obj-m := devmem_rw.o
devmem_rw-objs := rwmem.o debugfs_hooks.o

endif
