## 简介
  libunwind是一款简单易用用来栈解退的库，目前广泛应用。而且从Android5.0之后，android使用的最新的backtrace工具
便是libunwind。当然了Android最新的的回溯工具还有libbacktrace，这个也是依赖libunwind实现的栈解退库。

## 功能
- 本地解退
  通过调用unw_getcontext()获得CPU各寄存器值的快照，你可以在这快照基础上建立一个unwind_cursor,最后执行一个unw_int_local(),此时cursor指向当前栈帧。通过调用unw_step() unwind cursor是可以
  向上移动的（去指向早前的栈帧）。通过重复调用该函数，你便可以遍历整个调用链。unw_step返回0标示没有更多栈帧了，返回正值标示还有更多帧，负值标示有错误。
  - 常用的函数，用以获取/修改 某一栈帧中的寄存器的值。
    - unw_get_reg() 获取整型寄存器的数值
    - unw_get_fpreg() 获取浮点型寄存器的数值
    - unw_set_reg() 设置整形寄存器的数值
    - unw_set_fpreg() 设置浮点型寄存器数值
  - unw_resume()实现了类似goto的功能，只需要传递对应cursor的值就可以了。
- 如果你的libunwind只需要本地解退的话，你可以使用更快速的优化版本。使用方法，在`#include<libunwind>`之前
  `#define UNW_LOCAL_ONLY`就可以了。

下面展示一个最基本的backtrace方法实现：
```
#define UNW_LOCAL_ONLY
#include <libunwind.h>

void show_backtrace (void) {
  unw_cursor_t cursor; unw_context_t uc;
  unw_word_t ip, sp;

  unw_getcontext(&uc);
  unw_init_local(&cursor, &uc);
  while (unw_step(&cursor) > 0) {
    unw_get_reg(&cursor, UNW_REG_IP, &ip);
    unw_get_reg(&cursor, UNW_REG_SP, &sp);
    printf ("ip = %lx, sp = %lx\n", (long) ip, (long) sp);
  }
}

```
- 远程解退，实际上就是监视另外一个进程的调用栈栈帧中寄存器信息
