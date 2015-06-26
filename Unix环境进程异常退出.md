# Unix环境进程异常退出
- 向进程发送信号导致进程异常退出
- 代码错误导致进程运行时异常退出

## 预备知识
- **core dump**
	- 是操作系统在进程收到某些信号而终止运行时，将此时进程地址空间内的内容以及进程状态的其他信息写出的一个磁盘文件
	- 它是软件发生错误无法恢复到产物，dump的生成一般是在系统进行中断处理进行的。
		- 广义的中断包含两种：中断（Interrupts）和异常(Exception),中断可在任何时候发生，与 CPU 正在执行什么指令无关，中断主要由 I/O 设备、处理器时钟（分时系统依赖时钟中断划分时间片）或定时器等硬件引发，可以被允许或取消。而异常是由于 CPU 执行了某些指令引起的，可以包括存储器存取违规、除 0 或者特定调试指令等，**内核也将系统服务视为异常**。
		- 每个中断都会唯一对应到一个中断处理程序，在该中断触发时，相应的处理程序就会被执行。例如应用进程进行系统调用时，就会触发一个软件异常，进入中断处理函数，完成从用户态到系统态的迁移并进入相应系统调用的入口点。应用进程 coredump 也是一个类似的过程。
	- _应用进程core dump_ 生成过程：在进程运行出现异常行为时，例如无效地址访问、浮点异常、指令异常等，将导致系统转入内核态进行异常处理（即中断处理），向相应的进程发出特定信号例如 SIGSEGV、SIGFPE、SIGILL 等。如果应用进程注册了相应信号的处理函数（例如可通过 sigaction 注册信号处理函数），则调用相应处理函数进行处理（应用程序可以选择记录信息后生成 core dump 并退出）；否则将采取默认动作，例如 SIGSEGV 的默认动作是生成 core dump 并退出程序。  由于进程信号处理本质上是异步的，应用进程注册的信号处理函数中使用的例程需要保证是异步信号安全的，例如不能使用诸如 pthread 开头的例程。
- **特定信号量**
	- SIGFPE FPE=floating-point exception浮点异常，一般是进程执行了错误的算术操作。一个通常的疏忽是认为除以零是SIGFPE的唯一来源。在一些架构上（包括IA-32[来源请求]），使用INT_MIN（最小的可以被表示的负整数值）除以-1的整数除法也会触发这个信号，因为商是一个无法被表示的正数。（比如8位有符号整数可以表示-128、+127和它们之间的整数。-128÷-1＝+128 ＞ +127，因此无法被表示而产生溢出并触发此信号
	- SIGINT 默认情况下进程终止
	- SIGSEGV 进程执行了一个无效内存引用或者发生段错误,SEGV=segmentation violation段违例
	- SIGKILL 立即终止进程，与SIGINT不同，这个信号量无法被捕获，所以接收此信号的进程在收到此信号时不能执行任何清理动作

## 向进程发送信号
- SIGKILL/SIGINT中断进程，通过signal注册此类信号处理函数（SIGKILL除外） ，例子如下
	signal函数原型如下``` void (*signal(int sig,void (*func)(int)))(int)```

	```
	  1 #include <signal.h>
      2 #include <stdio.h>
      3 #include <unistd.h>
      4 void cleanTask(int sig) {
      5     printf( "Got the signal, deleting the tmp file\n" );
      6     if( access( "/tmp/temp.lock", F_OK ) != -1 ) {
      7           if( remove( "/tmp/temp.lock" ) != 0 )
      8               perror( "Error deleting file" );
      9           else
     10               printf( "File successfully deleted\n" );
     11     }
     12
     13     printf( "Process existing...\n" );
     14     exit(0);
     15 }
     16
     17 int main() {
     18     (void) signal( SIGINT, cleanTask );
     19     FILE* tmp = fopen ( "/tmp/temp.lock", "w" );
     20     while(1) {
     21         printf( "Process running happily\n" );
     22         sleep(1);
     23     }
     24
     25     if( tmp )
     26         remove( "/tmp/temp.lock" );
     27 }
  	```
## 编程错误导致的运行时异常退出

1. 处理器异常有很多种，系统为每个异常分配异常号，每个异常有相对应的异常处理函数。以 x86 处理器为例，除 0 操作产生 DEE 异常 (Divide Error Exception)，异常号是 0；内存非法访问产生 GPF 异常 (General Protection Fault)，异常号是 13，而缺页 (page fault) 异常的异常号是 14。当异常出现时，处理器挂起当前进程，读取异常号，然后执行相应的异常处理函数。如果异常是可修复，比如内存缺页异常，异常处理函数会修复系统错误状态，清除异常，然后重新执行一遍被中断的指令，进程继续运行；如果异常无法修复，比如内存非法访问或者除 0 操作，异常处理函数会终止进程运行
2. 常见的错误
	- 内存非法访问 segmentation fault
	- 除0操作 DEE divide error exception
	- 缺页
3. 异常处理过程
	1. 进程执行非法指令或错误操作
	2. 非法操作导致处理器异常产生
	3. 系统挂起进程，读取异常号并跳转到对应异常处理函数
		1. 异常处理函数首先查看异常是不是可以恢复，如果无法恢复异常，异常处理函数向进程发送信号
		2. 异常处理函数调用内核函数issig()和psig()来接收处理信号，**内核函数psig()执行默认的信号处理程序**，终止进程运行
	4. 进程异常退出
