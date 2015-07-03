# ELF&Mach-O 目标文件
## 字节序
### 基本概念
- MSB 最重要的位或最重要的字节，通常用来表明一个bit序列或这个byte序列中对取值影响最大的那个bit/byte
- LSB 与MSB相反 对整个序列取值影响最小的bit/byte
- 大小端
	- 大端 MSB存储在低地址，传输在前；LSB存储在高地址，传输在后。
	- 小端 MSB存储在高地址，传输在后；LSB存储在低地址，传输在前
### 机型
- Intel X86系列 小端
- Mac 早期PowerPC系列处理器 大端
- TCP/IP网络和Java虚拟机的字节序均是大端的
- 举个栗子0x12345678传输，MSB 0x12，LSB 0x78  高地址->低地址
	- 大端 存储形式：0x78563412 传输形式：0x12345678
  	- 小端 存储形式：0x12345678 传输形式：0x78563412
## ELF
- magic-code 0x7f454c46
- ELF文件头前16字节
	- magic
	- class elf32/64
	- data 字节序：2大端1小端
	- version 默认为1
	- OS/ABI 系统平台版本
	- ABI Version 系统版本号
## Mach-O
