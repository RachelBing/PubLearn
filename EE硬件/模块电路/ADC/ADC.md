## Why AC Source should be 2-4 bits more resolution than the ADC under test?

As an often used definition of ENOB:

𝐸𝑁𝑂𝐵=𝑆𝐼𝑁𝐴𝐷−1.766.02

So 如果 DAC（交流电源）的 ENOB 变低，SINAD 也会变低，这意味着噪声和失真会相对增加，这将影响测量精度。

另一点是，交流源的分辨率低于2-4位会引起更高的谐波失真，ADC输出端的数字信号会因DAC和ADC的谐波失真而恶化，并且可以求和二次谐波的幅度（例如）。由于具有更高分辨率的交流源会带来更低的谐波失真，测试输出结果将变得更加准确。

Refer to this article: [ADC Production Test Technique Using Low-Resolution Arbitrary Waveform Generator](https://www.hindawi.com/journals/vlsi/2008/482159/)