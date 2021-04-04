ccflags-y += -Wall -Wextra -Wno-unused-parameter

PWD := $(shell pwd)
ifeq ($(LINUX_DIR),)
	KERNEL_VERSION := $(shell uname -r)
	LINUX_DIR := /lib/modules/$(KERNEL_VERSION)/build
endif

ifeq ($(BIN_DIR),)
	BIN_DIR := /bin
endif

beagle-logic-y := beaglelogic.o

obj-m := beagle-logic.o

all:
	$(MAKE) -C '$(LINUX_DIR)' M='$(PWD)' modules C=1
clean:
	$(MAKE) -C '$(LINUX_DIR)' M='$(PWD)' clean

# Compile and install device tree
overlay: beaglelogic-00A0.dtbo

beaglelogic-00A0.dtbo: beaglelogic-00A0.dts
	$(BIN_DIR)/dtc -O dtb -o beaglelogic-00A0.dtbo -b 0 -@ beaglelogic-00A0.dts
