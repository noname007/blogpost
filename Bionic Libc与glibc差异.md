与glibc相比，bionic libc有如下特点:
- 采用bsd license，而不是glibc的GPL license
- 大小约为200KB，为glibc的一半，且运行速度更快
- 实现了更小、更夸得pthread
- 提供了一些Android所需要的重要函数，
- 不完全支持posix标准，比如C++异常、宽字符等，
