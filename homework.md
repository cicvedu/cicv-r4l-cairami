# 作业

## 实验环境搭建

### 配置BusyBox
![1699342702968](image/homework/1699342702968.png)
生成_install目录
![1699342759845](image/homework/1699342759845.png)

### 配置Linux文件夹
检查内核rust支持已经启用
![1699342863336](image/homework/1699342863336.png)

## 作业1：编译Linux内核

### 进入Linux文件夹，使用如下命令进行编译：

#### make x86_64_defconfig

![1699258178208](image/homework/1699258178208.png)

#### make LLVM=1 menuconfig

#set the following config to yes

![1699258228412](image/homework/1699258228412.png)

#### make LLVM=1 -j$(nproc)

![1699258623230](image/homework/1699258623230.png)

## 作业2：对Linux内核进行配置

### 编译src_e1000的代码成一个内核模块
![1699343388929](image/homework/1699343388929.png)

### 禁用默认的C版本e1000网卡驱动
![1699343489932](image/homework/1699343489932.png)

### 重新编译内核，运行./build_image.sh，启动Qemu

### 手动配置网卡驱动
insmod r4l_e1000_demo.ko
ip link set eth0 up
ip addr add broadcast 10.0.2.255 dev eth0
ip addr add 10.0.2.15/255.255.255.0 dev eth0 
ip route add default via 10.0.2.1
![1699343659027](image/homework/1699343659027.png)

ping 10.0.2.2
![1699343830935](image/homework/1699343830935.png)

### 问题1：编译成内核模块，是在哪个文件中以哪条语句定义的？
在Kbuild中，obj-m := r4l_e1000_demo.o

### 问题2：该模块位于独立的文件夹内，却能编译成Linux内核模块，这叫做out-of-tree module，请分析它是如何与内核代码产生联系的？
Makefile中通过-C指定linux内核位置，而M=$(PWD)指定驱动源码位置。内核顶层的Makefile检查到M非空时，会编译该模块为外部module。
ifeq ("$(origin M)", "command line")
  KBUILD_EXTMOD := $(M)
endif
