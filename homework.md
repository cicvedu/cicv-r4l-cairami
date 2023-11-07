# 作业

## ## 作业1：编译Linux内核

### 进入Linux文件夹，使用如下命令进行编译：

#### make x86_64_defconfig

![1699258178208](image/homework/1699258178208.png)

#### make LLVM=1 menuconfig

#set the following config to yes

![1699258228412](image/homework/1699258228412.png)

#### make LLVM=1 -j$(nproc)

![1699258623230](image/homework/1699258623230.png)


git@github.com:cicvedu/cicv-r4l-cairami.git

qemu 

./configure --help


./configure --target-list=x86_64-softmmu,x86_64-linux-user  --enable-sdl
