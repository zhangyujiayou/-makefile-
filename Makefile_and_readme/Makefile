
CROSS_COMPILE = 						#定义交叉编译工具
AS		= $(CROSS_COMPILE)as			#
LD		= $(CROSS_COMPILE)ld			#定义链接工具链LD
CC		= $(CROSS_COMPILE)gcc			#定义交叉编译工具工具链GCC
CPP		= $(CC) -E						#定义交叉编译工具工具链GCC 增添编译选项-E ：预处理，快速展开宏。
AR		= $(CROSS_COMPILE)ar			#
NM		= $(CROSS_COMPILE)nm			#

STRIP		= $(CROSS_COMPILE)strip		#
OBJCOPY		= $(CROSS_COMPILE)objcopy  	#
OBJDUMP		= $(CROSS_COMPILE)objdump	#

export AS LD CC CPP AR NM				#export：导出变量，使得变量在makefile存在的
export STRIP OBJCOPY OBJDUMP			#目录及其子目录中全局可见

CFLAGS := -Wall -O2 -g					#GCC编译器的编译选项：-Wall 打开告警，-O2 选择优化等级2， -g 产生gdb调试用的可执行文件
CFLAGS += -I $(shell pwd)/include		#-I 指定头文件的包含目录为：当前目录下的include目录。

LDFLAGS := 								#链接选项

export CFLAGS LDFLAGS					#导出变量，使得变量在makefile存在的目录及其子目录中全局可见
									
TOPDIR := $(shell pwd)					#定义变量为顶层目录
export TOPDIR							#导出变量，使得变量在makefile存在的目录及其子目录中全局可见

TARGET := test							#定义目标


obj-y += main.o							#将顶层目录文件中的所有需要由 *.c 文件生成的 *.o 文件添加到obj-y变量里面。
obj-y += sub.o							#将顶层目录文件中的所有需要由 *.c 文件生成的 *.o 文件添加到obj-y变量里面。
obj-y += a/								#将顶层目录里面包含的子文件夹 也添加到obj-y变量里面。


all : start_recursive_build $(TARGET)	#构建规则：需要生成all，处理第一个依赖，切换到顶层目录的makefile.build--->>>>前往Makefile.bulid中
	@echo $(TARGET) has been built!

start_recursive_build:
	make -C ./ -f $(TOPDIR)/Makefile.build

$(TARGET) : built-in.o
	$(CC) -o $(TARGET) built-in.o $(LDFLAGS)

clean:
	rm -f $(shell find -name "*.o")
	rm -f $(TARGET)

distclean:
	rm -f $(shell find -name "*.o")
	rm -f $(shell find -name "*.d")
	rm -f $(TARGET)
	