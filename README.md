# hit-oslab
基于Ubuntu 20.04/18.04配置实现 哈工大-李志军老师《操作系统》课程实验环境

- 导入安装包
    
    *安装包已放在sources文件夹下*

    解压安装包至文件夹
    ```
    tar -zvxf hit-oslab-linux-20110823.tar.gz  -C /root/
    ```
- 进入 linux-0.11，尝试编译
    ```
    cd /root/oslab/linux-0.11
    make all
    ```
    报错 
    ```
    as86 -0 -a -o boot/bootsect.o boot/bootsect.s
    make: as86: Command not found
    make: *** [Makefile:101: boot/bootsect] Error 127
    ```
- 安装 as86
    ```
    sudo apt-get install bin86
    ```
    安装完成后，尝试执行`make all`

    报错
    ```
    gcc-3.4 -m32 -g -I./include -traditional -c boot/head.s
    make: gcc-3.4: Command not found
    make: *** [Makefile:62: boot/head.o] Error 127
    ```

- 安装 gcc-3.4

    参考文档：[Ubuntu 20.04（64位）如何配置gcc-3.4用于编译linux-0.11](https://www.bilibili.com/read/cv6353911/)
    
    执行

    ```
    wget http://old-releases.ubuntu.com/ubuntu/pool/main/g/gcc-3.4/cpp-3.4_3.4.6-6ubuntu2_amd64.deb 

    wget http://old-releases.ubuntu.com/ubuntu/pool/main/g/gcc-3.4/gcc-3.4-base_3.4.6-6ubuntu2_amd64.deb

    wget http://old-releases.ubuntu.com/ubuntu/pool/main/g/gcc-3.4/gcc-3.4_3.4.6-6ubuntu2_amd64.deb

    sudo dpkg -i cpp-3.4_3.4.6-6ubuntu2_amd64.deb gcc-3.4-base_3.4.6-6ubuntu2_amd64.deb gcc-3.4_3.4.6-6ubuntu2_amd64.deb

    sudo apt install gcc-multilib
    ```

    此时运行 make all可通过

- 回上一级目录，运行 `./run` 
    报错
    ```
    ./bochs/bochs-gdb: error while loading shared libraries: libSM.so.6: cannot open shared object file: No such file or directory
    ```
    执行
    ```
    sudo apt install lib32z1 libsm-dev:i386 libx11-6:i386 libxpm4:i386 libstdc++6:i386
    ```
- 运行`./run`

    成功执行，截图如下

    [结果截图](./sources/result.png)