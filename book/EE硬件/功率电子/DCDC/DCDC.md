buck

boost

buck-boost
劣化电源实验
供电端出现瞬时跌落
	之前电路作为降压，跌落瞬间作为升压

手机电池供电
	升降压延长待机时间
#### 开关电源的同步与非同步
[开关电源的同步与非同步的区别 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/480955483)
### 手册

 同步与非同步  
 输入电压，输入电流，输出电压，输出电流  
 输入输出电容选择  
 MOSFET选型  
	开关mos:Rds越小越好：导通损耗
	寄生C越小越好：导通速度
	电流足够大
 电感选型  
 功耗  
 纹波和噪声  
 上电时序
	在12V-5V的应用中，假设12V上电慢，5V快，那可能出现理论上输出比输入大的那一段实际中出现跌落
	所以在输入输出中加一个压差，大于6V再开，会比之前慢一点

### 设计要点
**欠压锁定**：上电、掉电到多少V导通/关断
缓启动电容不能太大/小

**输入电容**：
耐压，ESR
 
**输出电压**
通过VSENSE分压设计

**电感**最小值
![](Pasted%20image%2020240117224629.png)
KIND 0.1---0.4
电感最大电流：额定+纹波
ESR小

**输出电容**
剪切频率：1/10* 开关频率
	[转折频率，剪切频率，截止频率，极点，零点的概念总结 - 电源技术 - 电子工程世界-论坛 (eeworld.com.cn)](http://bbs.eeworld.com.cn/thread-649003-1-1.html)
	根据剪切频率设计Co-min
I根据电感算为1.116A
![](Pasted%20image%2020240118114900.png)
电压 纹波最大：
![](Pasted%20image%2020240118114747.png)

**续流二极管**
肖特基
	反向电压> 0.5（芯片内钳位二极管）+Vin
	损耗功率小：正向电压小
	正向电流> 开关电流正向峰值 ，工作+1/2纹波
	开关速度快

**自举电容**：芯片要求
耐压高12V->25V

**环路**设计COMP
剪切频率设计为开关频率的1/10~1/20，不能低于10k 
相位裕量≥45° ，增益裕量≤-10dB
清楚调节环路中R或C能让环路曲线怎么移动