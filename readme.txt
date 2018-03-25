bootload test

===================================================================================
板级的移植：

【1】找一个和你要移植的开发板，芯片类型相似的 （以S5PV210 的三星芯片为例）

cp -apv u-boot-2017.01/board/samsung/smdkc100  ./wstar  -rf

1、修改Kconfig

修改前的：
----------------------------------------------------
if TARGET_SMDKC100

config SYS_BOARD
	default "smdkc100"

config SYS_VENDOR
	default "samsung"

config SYS_SOC
	default "s5pc1xx"

config SYS_CONFIG_NAME
	default "smdkc100"

endif
-----------------------------------------------------

修改后的：
#这个是等下make menuconfig 指定的一个宏
if TARGET_WSTAR  

#指定你的board 文件夹的名称
config SYS_BOARD
	default "wstar"

config SYS_VENDOR
	default "samsung"
	
#指定你的芯片的类型
config SYS_SOC
	default "s5pc1xx"

#指定你的 include/configs/wstar.h 为配置头文件
config SYS_CONFIG_NAME
	default "wstar"

endif
--------------------------------------------------

2、修改Makefile

修改前的：
obj-y	:= smdkc100.o
obj-$(CONFIG_SAMSUNG_ONENAND)	+= onenand.o
obj-y	+= lowlevel_init.o

-------------------------------------------------
修改后的：
obj-y	:= wstar.o
obj-$(CONFIG_SAMSUNG_ONENAND)	+= onenand.o
obj-y	+= lowlevel_init.o

-------------------------------------------------
修改完毕之后将Kconfig 添加到arch/arm/Kconfig  

source "board/Samsung/wsat/Kconfig"

这时候如果make的话会报没有dts的错误







	
