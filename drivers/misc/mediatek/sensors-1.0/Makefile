ccflags-y += -Wno-error
ifeq ($(CONFIG_MTK_SENSOR_SUPPORT),y)
obj-$(CONFIG_CUSTOM_KERNEL_SENSORHUB)	+= sensorHub/
obj-$(CONFIG_MTK_HWMON)	    += hwmon/
obj-$(CONFIG_CUSTOM_KERNEL_ALSPS) += alsps/
ifeq ($(CONFIG_CUSTOM_KERNEL_ACCELGYRO),y)
obj-y += accelgyro/
else
obj-$(CONFIG_CUSTOM_KERNEL_ACCELEROMETER) += accelerometer/
obj-$(CONFIG_CUSTOM_KERNEL_GYROSCOPE) += gyroscope/
endif
obj-$(CONFIG_CUSTOM_KERNEL_MAGNETOMETER) += magnetometer/
obj-$(CONFIG_CUSTOM_KERNEL_BAROMETER) += barometer/
#obj-$(CONFIG_CUSTOM_KERNEL_HUMIDITY) += humidity/
obj-$(CONFIG_CUSTOM_KERNEL_STEP_COUNTER)	+= step_counter/
obj-$(CONFIG_CUSTOM_KERNEL_SIGNIFICANT_MOTION_SENSOR)	+= step_counter/
obj-$(CONFIG_CUSTOM_KERNEL_ACTIVITY_SENSOR)	+= activity_sensor/
obj-$(CONFIG_CUSTOM_KERNEL_SITUATION) += situation/
#obj-$(CONFIG_CUSTOM_KERNEL_PEDOMETER)	+= pedometer/
obj-$(CONFIG_CUSTOM_KERNEL_SENSOR_FUSION)	+= sensorfusion/
#obj-$(CONFIG_MTK_KERNEL_GEOFENCE) += geofence/
obj-$(CONFIG_CUSTOM_KERNEL_BIOMETRIC_SENSOR) += biometric/

#ifdef OPLUS_FEATURE_SENSOR
#/*Fei.Mo@PSW.BSP.Sensor, 2017/12/13, Add for oppo sensor type to send some info to scp*/
obj-y += oppo_sensor_devinfo/
#endif //OPLUS_FEATURE_SENSOR
#ifdef OPLUS_FEATURE_SENSORR_ALGORITHM
#/*xiebaixue@PSW.BSP.Sensor, 2020/06/11, Add for oppo sensor algo*/
#ifneq ($(OPLUS_FEATURE_SENSOR_ALGORITHM),)
obj-y += oppo_virtual_sensor/
#endif
#endif //OPLUS_FEATURE_SENSOR_ALGORITHM
else
obj-y += dummy.o
endif
