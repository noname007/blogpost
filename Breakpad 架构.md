## breakpad
 breakpad是google开发的一套跨平台的mini dump系统。其原理如下：
 ```
 SignalHandler (uses a global stack of ExceptionHandler objects to find
        |         one to handle the signal. If the first rejects it, try
        |         the second etc...)
        V
   HandleSignal ----------------------------| (clones a new process which
        |                                   |  shares an address space with
   (wait for cloned                         |  the crashed process. This
     process)                               |  allows us to ptrace the crashed
        |                                   |  process)
        V                                   V
   (set signal handler to             ThreadEntry (static function to bounce
    SIG_DFL and rethrow,                    |      back into the object)
    killing the crashed                     |
    process)                                V
                                          DoDump  (writes minidump)
                                            |
                                            V
                                         sys_exit

 ```
