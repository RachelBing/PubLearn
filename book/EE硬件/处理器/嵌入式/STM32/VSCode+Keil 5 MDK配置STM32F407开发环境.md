# VSCode+Keil 5 MDK+ST-LINK配置STM32F407寄存器程序开发环境

> keil μvision实在是太难用了，在代码间跳来跳去十分不便，于是就想用惯用的vscode来开发。因为其实就是C语言程序代码，所以把项目文件夹拖进去之后Linker啥的都有好好的工作，注释和代码跳转都能正常使用，但是不能编译、下载和调试，在插件中心发现了keil assistant这个插件，但是装了又不太会用，百度到的有关配置教程质量良莠不齐，磕磕绊绊了很久才弄好，故此整理一篇调教日记，以方便后来者。

## Keil 5 MDK项目配置

### 安装Keil 5 MDK

1.  安装mdk511a.exe

2.  安装ARM.CMSIS.4.1.1.pack

3.  安装Keil.STM32F4xx\_DFP.1.0.8.pack

4.  安装mdkcm511a.exe以兼容旧版项目格式

5.  激活以支持大项目编译

### 配置项目

1.  新建项目文件夹，在项目文件夹里新建USER、OBJ、SYSTEM等常规Keil MDK项目常用的文件夹

2.  在USER文件中新建项目文件

3.  在弹出的期间选择对话框中依次选择使用的开发板芯片型号

4.  添加启动文件和项目用到的源代码、头文件到对应文件夹中

5.  在μvision左侧目录树上右键Manage Project Items添加代码文件到项目中

    ![2021-07-02-22-18-35-image.png](https://raw.githubusercontent.com/CrystalRays/CDN/main/2021/07/05-08-17-00-2021-07-02-22-18-35-image.png)

6.  在options的output选项夹按下Select Folder for Objects按钮选择OBJ为输出文件夹，并勾选create Hex file选项

    ![2021-07-02-22-17-12-image.png](https://raw.githubusercontent.com/CrystalRays/CDN/main/2021/07/05-08-18-10-2021-07-02-22-17-12-image.png)

7.  在options的C/C++选项夹下Include设置项包含需要的头文件

    ![2021-07-02-22-16-48-image.png](https://raw.githubusercontent.com/CrystalRays/CDN/main/2021/07/05-08-18-29-2021-07-02-22-16-48-image.png)

8.  安装CH340驱动实现使用FlyMCU通过USB刷写ROM

9.  安装ST-Link驱动，并在options的Debug选项夹下use选择ST-Link Debugger

    ![2021-07-02-22-19-11-image.png](https://raw.githubusercontent.com/CrystalRays/CDN/main/2021/07/05-08-18-44-2021-07-02-22-19-11-image.png)

10. 点击use ST-Link Debugger右侧的settings按钮，在弹出的设置界面，选择Port为SW，确认右侧SW device列表中识别出设备

    ![2021-07-02-22-16-29-image.png](https://raw.githubusercontent.com/CrystalRays/CDN/main/2021/07/05-08-19-04-2021-07-02-22-16-29-image.png)

11. 保存设置退出项目

## VSCode安装配置keil assistant实现编译和下载

1.  安装keil assistant

    ![2021-07-02-22-24-23-image.png](https://raw.githubusercontent.com/CrystalRays/CDN/main/2021/07/05-08-19-30-2021-07-02-22-24-23-image.png)

2.  在插件设置中设置C51路径为null，MDK路径为C:\Keil\_v5\UV4\UV4.exe

    ![2021-07-02-22-24-36-image.png](https://raw.githubusercontent.com/CrystalRays/CDN/main/2021/07/05-08-19-43-2021-07-02-22-24-36-image.png)

3.  修改项目后缀名uvproj为uvprojx（没有x识别为C51项目，有x的识别为MDK项目）

4.  点KEIL UVISION PEOJECT面板右侧的按钮打开uvprojx文件

    ![2021-07-02-22-28-03-image.png](https://raw.githubusercontent.com/CrystalRays/CDN/main/2021/07/05-08-19-54-2021-07-02-22-28-03-image.png)

5.  点击Target 右侧的按钮进行编译和下载

    ![2021-07-05-08-20-14-image.png](https://raw.githubusercontent.com/CrystalRays/CDN/main/2021/07/05-08-20-46-2021-07-05-08-20-14-image.png)

    ![2021-07-02-22-31-28-image.png](https://raw.githubusercontent.com/CrystalRays/CDN/main/2021/07/05-08-21-02-2021-07-02-22-31-28-image.png)

## VSCode配置ST-Link调试环境

### 安装插件

1.  Cortex-Debug

2.  ARM

3.  C/C++

### 安装调试组件

3/4/5任选其一

1.  ARM版GBD调试器——arm-none-eabi-gdb:[GNU Toolchain | GNU Arm Embedded Toolchain Downloads – Arm Developer](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads)

2.  开源版STLINK——st-util:[stlink-org/stlink: Open source STM32 MCU programming toolset (github.com)](https://github.com/stlink-org/stlink)

3.  STMCubeMX提供的ST-LINK gdbServer和STM32CubeProgrammer：[TrueSTUDIO - A powerful eclipse-based C/C++ integrated development tool for your STM32 projects - STMicroelectronics](https://www.st.com/content/st_com/en/products/development-tools/software-development-tools/stm32-software-development-tools/stm32-ides/truestudio.html)

4.  OpenOCD：[Download OpenOCD for Windows (gnutoolchains.com)](https://gnutoolchains.com/arm-eabi/openocd/)

### 配置调试环境

#### st-util

1.  安装arm-none-eabi-gdb

2.  解压st-util

3.  配置系统环境变量，或配置vscode插件

    ![2021-07-03-14-18-56-image.png](https://raw.githubusercontent.com/CrystalRays/CDN/main/2021/07/05-08-32-34-2021-07-03-14-18-56-image.png)

4.  配置launch.json

    ```json
           {
                "cwd": "${workspaceRoot}",
                "executable": "../OBJ/TEST.axf",
                "name": "Debug STUTIL",
                "request": "attach", //launch+axf在启用FPU时会出现hardfault循环
                "type": "cortex-debug",
                "servertype": "stutil",
                "svdFile": "C:\\Keil_v5\\ARM\\Pack\\Keil\\STM32F4xx_DFP\\1.0.8\\SVD\\STM32F40x.svd",
                "device": "STM32F407ZGT6",
                "v1":false,

            },
    ```

5.  调试的时候先用keil assistant下载程序，启动板子后再attach上去调试

#### ST-LINK\_gdbserver

1.  安装arm-none-eabi-gdb

2.  从trueStudio中解包获得ST-LINK gdbServer和STM32CubeProgrammer

3.  配置系统环境变量，或配置vscode插件

    ![2021-07-03-14-21-32-image.png](https://raw.githubusercontent.com/CrystalRays/CDN/main/2021/07/05-08-32-52-2021-07-03-14-21-32-image.png)

4.  配置launch.json

    ```json
            {
                "cwd": "${workspaceRoot}",
                "executable": "../OBJ/TEST.hex",//axf在启用FPU时会出现hardfault循环,hex没有符号表没法下断点
                "name": "Debug STLINK",
                "request": "launch",//launch+axf在启用FPU时会出现hardfault循环，attach无法工作，原因未知
                "type": "cortex-debug",
                "servertype": "stlink",
                "svdFile": "C:\\Keil_v5\\ARM\\Pack\\Keil\\STM32F4xx_DFP\\1.0.8\\SVD\\STM32F40x.svd",
                "device": "STM32F407ZGT6",
                "v1":false,

            },
    ```

5.  hex没有符号表没法下断点，但是可以正常运行不会hardfault循环。正常运行后在调试窗口使用`file xxx.axf`切换到axf就能正常调试了

    ![2021-07-03-15-27-33-image.png](https://raw.githubusercontent.com/CrystalRays/CDN/main/2021/07/05-08-33-03-2021-07-03-15-27-33-image.png)

#### openOCD

*   装arm-none-eabi-gdb

*   解压openOCD

*   配置系统环境变量，或配置vscode插件

*   配置launch.json

    ```json
            {
                "cwd": "${workspaceRoot}",
                "executable": "../OBJ/TEST.hex",
                "name": "Debug openocd",
                "request": "launch",
                "type": "cortex-debug",
                "servertype": "openocd",
                "configFiles": ["C:/Program Files/OpenOCD-20210625-0.11.0/share/openocd/scripts/interface/stlink.cfg","C:/Program Files/OpenOCD-20210625-0.11.0/share/openocd/scripts/target/stm32f4x.cfg"]
            },
    ```

*   hex没有符号表没法下断点，但是可以正常运行不会hardfault循环。正常运行后在调试窗口使用`file xxx.axf`切换到axf就能正常调试了

