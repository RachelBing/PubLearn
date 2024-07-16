### **Amdahl's Law(阿姆达尔定律)**

 提升一个系统的一个部分的性能对整个系统有多大影响。这一观察被称为Amdahl's Law（阿姆达尔定律）：

(**注：这里的**系统，可指**计算机系统**或别的什么系统)

当提升系统的一部分性能时，对整个系统性能的影响取决于:

1、这一部分有多重要&#x20;

2、这一部分性能提升了多少。

假设原来在一个系统中执行一个程序需要时间 ![T\_{old}](https://www.zhihu.com/equation?tex=T_%7Bold%7D\&consumer=ZHI_MENG "T_{old}") ，其中某一个部分占的时间百分比为 ![\alpha](https://www.zhihu.com/equation?tex=%5Calpha\&consumer=ZHI_MENG "\alpha") ，然后，把这一部分的性能提升 ![k](https://www.zhihu.com/equation?tex=k\&consumer=ZHI_MENG "k") 倍。即这一部分原来需要的时间为 ![\alpha T\_{old}](https://www.zhihu.com/equation?tex=%5Calpha+T_%7Bold%7D\&consumer=ZHI_MENG "\alpha T_{old}") ，现在需要的时间变为 ![(\alpha T\_{old})/k](https://www.zhihu.com/equation?tex=%28%5Calpha+T_%7Bold%7D%29%2Fk\&consumer=ZHI_MENG "(\alpha T_{old})/k") 。则整个系统执行此程序需要的时间变为：

![T\_{new}=(1-\alpha)T\_{old} + (\alpha T\_{old})/k =T\_{old}\[(1-\alpha) + \alpha /k\]](https://www.zhihu.com/equation?tex=T_%7Bnew%7D%3D%281-%5Calpha%29T_%7Bold%7D+%2B+%28%5Calpha+T_%7Bold%7D%29%2Fk+%3DT_%7Bold%7D%5B%281-%5Calpha%29+%2B+%5Calpha+%2Fk%5D\&consumer=ZHI_MENG "T_{new}=(1-\alpha)T_{old} + (\alpha T_{old})/k =T_{old}\[(1-\alpha) + \alpha /k]")

故可得，系统性能提速的倍数为: ![S=\frac{1}{(1-\alpha)+\alpha/k}](https://www.zhihu.com/equation?tex=S%3D%5Cfrac%7B1%7D%7B%281-%5Calpha%29%2B%5Calpha%2Fk%7D\&consumer=ZHI_MENG "S=\frac{1}{(1-\alpha)+\alpha/k}") 。

### **RISC VS CISC**

**CISC**的英文全称为“Complex Instruc[TI](https://link.zhihu.com/?target=http%3A//bbs.elecfans.com/zhuti_715_1.html)on Set Computer”，即“复杂指令系统计算机”

**RISC**的英文全称为“Reduced Instruc[TI](https://link.zhihu.com/?target=http%3A//bbs.elecfans.com/zhuti_715_1.html)on Set Computer”，即“精简指令集计算机”

**内存**容量为4GB，即**内存单元的地址宽度**为32位。

**字长**为32位即要求**数据总线的宽度**为32位

### **数据总线**

（1） 是CPU与内存或其他器件之间的数据传送的通道。

（2）数据总线的宽度决定了CPU和外界的数据传送速度。

（3）每条传输线一次只能传输1位二进制数据。eg: 8根数据线一次可传送一个8位二进制数据(即一个字节)。

（4）数据总线是数据线数量之和。

### 地址总线

（1）CPU是通过地址总线来指定存储单元的。

（2）地址总线决定了cpu所能访问的最大内存空间的大小。eg: 10根地址线能访问的最大的内存为1024位二进制数据（1024个内存单元）(1B)

（3）地址总线是地址线数量之和。

### 控制总线

（1）CPU通过控制总线对外部器件进行控制。

（2）控制总线的宽度决定了CPU对外部器件的控制能力。

（3）控制总线是控制线数量之和。

最后总结如下： 地址总线的宽度决定CPU的寻址能力； 数据总线的宽度决定CPU与其他元器件一次最大传送的数据量； 控制总线决定CPU对其他元器件的控制能力。&#x20;
