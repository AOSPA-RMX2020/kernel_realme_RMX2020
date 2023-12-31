#
# Copyright (C) 2015 MediaTek Inc.
#
# This program is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License version 2 as
# published by the Free Software Foundation.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
# GNU General Public License for more details.
#
#
# Makefile for misc devices that really don't fit anywhere else.
#
MTK_PLATFORM := $(subst ",,$(CONFIG_MTK_PLATFORM))
ARCH_MTK_PROJECT := $(subst ",,$(CONFIG_ARCH_MTK_PROJECT))
IMGSENSOR_DRIVER_PATH  := $(srctree)/drivers/misc/mediatek/imgsensor/src
MTK_DRIVER_PATH  := $(srctree)/drivers/misc/mediatek
COMMON_VERSION := v1_1
subdir-ccflags-y += -I$(IMGSENSOR_DRIVER_PATH)/common/$(COMMON_VERSION) \
	-I$(IMGSENSOR_DRIVER_PATH)/$(MTK_PLATFORM)/seninf/ \
	-I$(MTK_DRIVER_PATH)/mmdvfs \
	-I$(srctree)/drivers/i2c/busses/
obj-y				+= ../common/$(COMMON_VERSION)/imgsensor.o
obj-y				+= ../common/$(COMMON_VERSION)/imgsensor.o
obj-y				+= ../common/$(COMMON_VERSION)/imgsensor_hw.o
obj-y				+= ../common/$(COMMON_VERSION)/imgsensor_i2c.o
obj-y				+= ../common/$(COMMON_VERSION)/imgsensor_legacy.o
obj-y				+= ../common/$(COMMON_VERSION)/imgsensor_proc.o
obj-y				+= ../common/$(COMMON_VERSION)/imgsensor_sensor_list.o
obj-y				+= ../common/$(COMMON_VERSION)/seninf.o
#ifdef OPLUS_FEATURE_CAMERA_COMMON
#Henry.Chang@Cam.Drv, 20200725, add for oppo custom  operation
obj-y				+= ../OplusImgsensor/imgsensor_eeprom.o
obj-y				+= ../OplusImgsensor/imgsensor_hwcfg_custom.o
obj-y				+= ../OplusImgsensor/imgsensor_hwcfg_mt6771.o
#endif /* OPLUS_FEATURE_CAMERA_COMMON */
define FILTER_DRV
ifeq ($(wildcard $(IMGSENSOR_DRIVER_PATH)/$(MTK_PLATFORM)/camera_project/$(ARCH_MTK_PROJECT)/$(1)),)
ifeq ($(wildcard $(IMGSENSOR_DRIVER_PATH)/$(MTK_PLATFORM)/$(1)),)
common_drv += ../common/$(COMMON_VERSION)/$(1)/
else
platform_drv += $(1)/
endif
else
project_drv += ./camera_project/$(ARCH_MTK_PROJECT)/$(1)/
endif
endef
$(foreach drv,$(subst $\",,$(CONFIG_CUSTOM_KERNEL_IMGSENSOR)),$(eval $(call FILTER_DRV,$(drv))))
ifneq ($(common_drv),)
endif
obj-y				+= $(common_drv)
ifneq ($(platform_drv),)
endif


#secure part
ifeq ($(CONFIG_MTK_CAM_SECURITY_SUPPORT),y)
ifneq ($(CONFIG_MTK_CAM_GENIEZONE_SUPPORT),y)
#i2c
ccflags-y           += -DCONFIG_MTK_CAM_SECURE_I2C
obj-y				+= ../common/$(COMMON_VERSION)/imgsensor_ca.o
endif
endif
#end

obj-y				+= $(platform_drv)
ifeq (,$(wildcard $(IMGSENSOR_DRIVER_PATH)/$(MTK_PLATFORM)/camera_project/$(ARCH_MTK_PROJECT)/camera_hw))
subdir-ccflags-y		+= -I$(IMGSENSOR_DRIVER_PATH)/$(MTK_PLATFORM)/camera_hw
obj-y				+= camera_hw/
ifneq ($(project_drv),)
obj-y				+= camera_project/$(ARCH_MTK_PROJECT)/
endif
else
obj-y				+= camera_project/$(ARCH_MTK_PROJECT)/
subdir-ccflags-y		+= -I$(IMGSENSOR_DRIVER_PATH)/$(MTK_PLATFORM)/camera_project/$(ARCH_MTK_PROJECT)/camera_hw
endif

ifeq ($(CONFIG_MICROTRUST_TEE_SUPPORT),y)
ifneq ($(CONFIG_MTK_CAM_GENIEZONE_SUPPORT),y)
include $(srctree)/drivers/misc/mediatek/teei/Makefile.include
endif
endif

ifeq ($(CONFIG_TRUSTONIC_TEE_SUPPORT),y)
ifneq ($(CONFIG_MTK_CAM_GENIEZONE_SUPPORT),y)
include $(srctree)/drivers/misc/mediatek/gud/Makefile.include
endif
endif
subdir-ccflags-y += -DSENSOR_PLATFORM_MT6771
obj-y += seninf/
