### **命名规则**

![image.png](https://note.youdao.com/yws/res/565/WEBRESOURCEb7cfde4926df32a9742701afd1793e03)

### **STM32==引脚==定义**

![image.png](https://note.youdao.com/yws/res/581/WEBRESOURCEd62008a4effe203a27f9281d7008a64c)

> **red-电源**
>
> **blue-最小系统。**
>
> green-IO口、功能口。

FT-容忍5V电压;没FT-容忍3.3V电压

> 主功能和引脚名称不同的，以**主功能**为主。
>
> **默认复用功能**是IO口上同时连接的外设功能引脚。
>
> 配置的时候可以选择通用的主功能或者**复用功能**。推荐先用不需要配置的IO
>
> 两个都要用的功能复用在一个IO口上时，可以把其中一个重映射到其他端口（**重定义Remap**表中有其他端口）。

1.  **VBAT**:可接3V电池备用；为RTC，备份寄存器供电
2.  **TEMPER**:侵入检测。安全保护防拆除点清空数据
3.  PC13-15：IO
4.  OSC32: 32.768 Hz RTC晶振
5.  **OSC:** 主晶振，一般8MHz；PLL倍频后产生72MHz主时钟
6.  **N**RST：负极（Negative)复位
7.  \*\***VSSA**负极=GND；**VDDA**正极=3.3V；内部模拟电源
8.  10-19，21-22，25-33，41-43，45-46为**IO**口：PA;PB
9.  PA0-**WKUP**：唤醒处于待机模式的STM32
10. 20，44 \*\*BOOT1、0：\*\*配置启动模式. ![image.png](https://note.youdao.com/yws/res/665/WEBRESOURCEfb4f0aa154baef96e16b19a0f3adccb8)

    > **X0**: 常用；
    >
    > **01**（3.3V）这个模式用来做串口下载，系统存储器中有一段**boot loader**程序用来接收串口数据，然后刷新到主闪存。配置34-40端口实现。还有**STLINK**和**JLINK**下载程序的方式。
    >
    > \*\*11：\*\*程序调试模式。
    >
    > 在上电的瞬间是BOOT1的功能一当第4个时钟过之后为PB2功能
11. **VSS**\_1负;**VDD**\_1正;系统主电源；2、3同。分区供电，供电口多。++VSS=GND;VDD=3.3V。++
12. 34，37-40：调试端口：调试&下载；用不到JTAG的话，如果要把相关端口作为正常io口使用的话，需要在程序中配置。
13. STM32支持

    *   **==SWD==**：serial wire debug串行线调试;要2根线：**SWDIO, SWCLK**.
    *   \*\*JTAG \*\*Jointest Actiongroup调试协议。要5根线：**JTMS、 JTCK、JTDI 、JTDO、NTRST**

### **电路-最小系统**

3V3和GND间有滤波电容保证电压稳定

VBAT不用时可接3V3或者悬空![image.png](https://note.youdao.com/yws/res/694/WEBRESOURCE21729d6e0222653882e9ce16979185a0)

> 晶振\*\*起振电容：\*\*消减偕波
>
> 在许可范围内，电容C1和C2值越小越好。起振电容值偏大虽有利于振荡器的稳定，但将会增加起振时间，比较常见的是在15pF-33 pF 之间取值。具体的取值参数要依据电路板上电后，实测晶振输出频率为准，使其尽量靠近**标称频率**
>
> 要RTC的话在3、4间接32.768k（2^15）Hz晶振

![image.png](https://note.youdao.com/yws/res/696/WEBRESOURCE917a42441d4187d3e43a73701299ac7e)![image.png](https://note.youdao.com/yws/res/712/WEBRESOURCE1ef162722ee9ba03f15d87a13402518d)

NRST**复位电路**

开始时C未充电，NRST=0V，上电瞬间复位。按键手动复位。

**稳压芯片**常用：XC6204, XC6206, AMS1117; TR9193.&#x20;

> PA11、PA12为USB引脚，同时提供5V供电

### **项目开发：**

#### **开发思路：**

1.  基于**寄存器**：类似51，不推荐，结构复杂，寄存器太多；
2.  基于\*\*==库函数==\*\*==：==ST官方封装函数；
3.  基于**HAL**库：图形化界面配置。（上课）隐藏底层逻辑，方便。

#### **新建文件**

> STM32F10x\_StdPeriph\_Lib\_V3.5.0\Libraries\CMSIS\CM3\DeviceSupport\ST\STM32F10x\startup\arm**启动**文件（用汇编写的），根据芯片型号选择某一个
>
> stm32f10x.h外设寄存器描述文件：相当于**头**文件；51的是REGX52.h
>
> system\_stm32f10x.c system\_stm32f10x.h**配置时钟**72Hz。
>
> core\_cm3.c core\_cm3.h**内核寄存器**文件。

这些文件全部粘贴到项目下面新建文件夹。

每次新建工程的时候都要在软件中另外导入Start文件夹下的，大概6个文件。包括一个启动文件，两个内核文件。一个外设寄存器描述文件，两个配置时钟文件。

#### **配置**

![image.png](https://note.youdao.com/yws/res/827/WEBRESOURCEe9cc4b01439e2b6d7d34a7badedfcab3)表示文件只读。

![image.png](https://note.youdao.com/yws/res/830/WEBRESOURCEb2316a32319320f4ce30941e6ab4e9c4)打开工程选项。

![image.png](https://note.youdao.com/yws/res/834/WEBRESOURCEe67291db4c79e3bc46df4aa6de278634)

在这里添加头文件路径。

新建一个user文件夹main函数放在里面。 Keil同步新建。

![image.png](https://note.youdao.com/yws/res/842/WEBRESOURCE64a90b216a72d892089bc8a0aab5e1c6)

在main中插入头文件。

![image.png](https://note.youdao.com/yws/res/844/WEBRESOURCE04781b2ee38e3a8a9097e40c96fecad0)

mian文件最后一行被置为空行

编译及建立工程：

![image.png](https://note.youdao.com/yws/res/847/WEBRESOURCE8284082c85ccd41c8de53233f905feaf)

下载程序到STM32：

![image.png](https://note.youdao.com/yws/res/851/WEBRESOURCE27de65796a408b7cc416c7e7ac0b8eeb)

啥都没有的时候

```c
#include "stm32f10x.h"                  // Device header

int main(void){
	while(1){
	
	}
}	
```

#### **测试：点亮主板上的灯？**

*   **RCC**的寄存器,**RCC**的寄存器使能**GPIOC**的时钟。

> 参考手册：APB2 外设时钟使能寄存器(RCC\_APB2ENR)，**IOPCEN**：IO端口C时钟使能 (I/O port C clock enable)
>
> 无关项为0，二进制转16进制，下图为**00000010**
>
> Keil中为**RCC->APB2ENR = 0X00000010;**
>
> ![image.png](https://note.youdao.com/yws/res/894/WEBRESOURCE0d6ccfbcdd5648606aa2297ea8718fd4)

*   端口配置高寄存器\*\*(GPIOx\_CRH) (x=A..E) \*\*X是A-E的任意一个字母。

> CNF13，MODE13用来配置13口： 11 对应输出模式
>
> 推挽输出是指既可以输出低电平，也可以输出高电平，可以直接驱动功耗不大的数字器件。
>
> 无关项为0，二进制转16进制，下图为**00300000**
>
> Keil中为**GPIOC->CRH = 0x00300000;**

![image.png](https://note.youdao.com/yws/res/1113/WEBRESOURCE0f74335025a8f0b42d993d340fe352b2)

*   端口输出数据寄存器(GPIOx\_ODR) (x=A..E)

无关项为0，二进制转16进制，下图为**00002000，表示灯灭；00000000为亮![image.png](https://note.youdao.com/yws/res/1132/WEBRESOURCE5bb781c9c06322547790af360b1f782b)**

Keil中为**GPIOC->ODR = 0x00002000**;

![image.png](https://note.youdao.com/yws/res/1121/WEBRESOURCEb60722f9b61ef7b56f5f13f6c1069d8a)

```c
#include "stm32f10x.h"                  // Device header

int main(void){
	RCC->APB2ENR = 0X00000010;
	GPIOC->CRH = 0x00300000;
	GPIOC->ODR = 0x00002000;
	while(1){
	
	}
}	

```

这种操作会影响其他端口的原有配置，而且不断查手册会比较慢。

单独配置需要&=和|=，更麻烦

> 新建Library文件夹存放**库函数**
>
> 固件库\STM32F10x\_StdPeriph\_Lib\_V3.5.0\Libraries\STM32F10x\_StdPeriph\_Driver\src中：
>
> misc.c为**内核**库函数，其他stm32f10x\_开头的为**内核外设**库函数
>
> \STM32F10x\_StdPeriph\_Lib\_V3.5.0\Libraries\STM32F10x\_StdPeriph\_Driver\inc中为头文件
>
> 以上文件复制到Library文件夹

固件库\STM32F10x\_StdPeriph\_Lib\_V3.5.0\Project\STM32F10x\_StdPeriph\_Template中：

> stm32f10x\_conf.h文件 *configuration*用来配置库函数头文件的包含关系的，另外这里面还有个用来参数检查的函数定义，这是所有库函数都需要的
>
> stm32f10x\_it.c，stm32f10x\_it.h *interrupt*文件是用来存放中断函数的
>
> 添加到USER目录下，软件内外都要加

#### **包含标准外设库的方法：**

修改宏定义-条件编译语句：意思是如果你定义了USE STDPERIPH DRIVER使用标准外设驱动这个字符串，include conf.h语句才有效。


添加库函数后，用RCC\_APB2PeriphClockCmd外设时钟控制


找到需要的一项进行复制，最后keil中配置寄存器的代码为RCC\_APB2PeriphClockCmd(RCC\_APB2Periph\_GPIOC,ENABLE);

配置端口需要用到GPIO\_Init，使用了结构体配置参数。需要在前面先定义一个结构体。

定义后的结构体中有三个参数。还是需要转到定义中去寻找发现mode是选择枚举里面的内容。选**GPIO\_Mode\_Out\_PP**通用推挽输出。

```c
 @param  GPIOx: where x can be (A..G) to select the GPIO peripheral.
  * @param  GPIO_InitStruct: pointer to a GPIO_InitTypeDef structure that
  *         contains the configuration information for the specified GPIO peripheral.

```

```c

#include "stm32f10x.h"                  // Device header

int main(void)
{
	RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOC,ENABLE);
	GPIO_InitTypeDef GPIO_InitStruct;
	GPIO_InitStruct.GPIO_Mode = GPIO_Mode_Out_PP;
	GPIO_InitStruct.GPIO_Pin = GPIO_Pin_13;
	GPIO_InitStruct.GPIO_Speed = GPIO_Speed_50MHz;
	GPIO_Init(GPIOC, &GPIO_InitStruct);
//	GPIO_SetBits(GPIOC, GPIO_Pin_13)//H高电平灭
	GPIO_ResetBits(GPIOC, GPIO_Pin_13);//L低电平亮
	while(1)
	{
	
	}
}	//事实上单片机的循环永远不会结束，所以main函数最后一定是死循环。

```

load后没反应**手动复位**一下
