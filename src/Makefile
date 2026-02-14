# SPDX-License-Identifier: GPL-2.0
#
# Makefile for the Linux PPP network device drivers.
#
MODULE=ppp_async
VERSION=6.18
KVERSION := $(shell uname -r)
KDIR := /lib/modules/${KVERSION}/build

obj-m = slhc.o ppp.o ppp_async.o
ppp-y = ppp_generic.o

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
