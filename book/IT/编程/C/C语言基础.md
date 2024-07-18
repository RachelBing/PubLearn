[VSCode配置C/C++环境 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/87864677)

sizeof 数组长度

int arr\_len = sizeof(arr)/sizeof(arr\[0]) 数组元素个数=数组的总大小/单个数组元素的大小

```c
int table[26];
memset(table, 0, sizeof(table));
```
Unicode 一个字符可能对应多个字节的问题，不同语言对于字符串读取处理的方式是不同的。
