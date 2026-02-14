# SPDX-License-Identifier: GPL-2.0
#
# Makefile for the Linux PPP network device drivers.
#
MODULE=ppp_async
VERSION=5.10
KVERSION := $(shell uname -r)
KDIR := /lib/modules/${KVERSION}/build

obj-m = slhc.o ppp.o ppp_async.o
ppp-y = ppp_generic.o

#
# Point --sourcetree at the directory above this file.
# Add --dkmstree /where if you don't want to use /var/lib/dkms/
# Add --installtree if you don't want to use /lib/modules/
#
DKMS_FLAGS= -m $(MODULE) -v $(VERSION) --sourcetree "`pwd`/.." $(USER_DKMS_FLAGS)

all:
	$(MAKE) -C $(KDIR) M=$(PWD)

install: all
	$(MAKE) -C $(KDIR) M=$(PWD) modules_install
	depmod -A

clean:
	$(MAKE) -C /lib/modules/$(KVERSION)/build M=$(PWD) clean

load: install remove
	modprobe ppp_async

unload:
	rmmod ppp_async 2> /dev/null || true
	rmmod ppp 2> /dev/null || true
	rmmod slhc 2> /dev/null || true
