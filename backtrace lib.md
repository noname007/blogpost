# 常见backtrace库比较
## 总览
  根据Google的Android开发人员的说明：
  ```
  libcorkscrew was removed because it didn't support aarch64 and was also missing dwarf support. We decided to go with libunwind as the base unwinder for L and beyond, however, there is no guarantee that it will continue to exist forever.

If you need to get backtrace information, I highly recommend that you use system/core/libbacktrace. This was designed to hide the implementation details of whatever unwinder we use and will be supported in to the future. If we delete libunwind in the future, we'll continue to have libbacktrace.

For an example of ways this unwinder is used, see system/core/debuggerd for unwinding a process different from the one you are executing out of. See art/runtime/utils.cc (DumpNativeStack) for unwinding threads in the current process. This code is in aosp master.
  ```
## libunwind
## libbacktrace
## libcorkscrew
  
