## core dump

core dump又叫核心转储（内存倾倒）, 当程序运行过程中发生异常, 程序异常退出时, 由os把程序当前的内存状况存储在一个core文件中, 叫core dump. linux中如果内存越界会收到SIGSEGV信号，然后就会core dump)

 **在程序中如果出现段错误，进程崩溃可从以下几个方面考虑：**

1、越界 （数组下标错误，或者字符串结束符问题）

2、空指针

3、多线程程序中使用了线程不安全的函数。或者未加锁

4、堆栈溢出。比如限制了线程使用32K空间，而在某个函数中数组分配直接64k导致。此种错误破坏系统的栈和堆结构，导致出现莫名其妙的错误。特别不好定位。

**如何定位呢？**

1、常用的办法是先看coredump，查看当前函数调用栈信息。

- 设置让系统在信号中断造成的错误时产生core文件， ulimit -c unlimited  。查看是否成功ulimit -a
- 运行产生coredump文件，通常在当前目录下，名字为core.pid
- 加载gdb  core.pid  program_name 
- 使用bt（backtrace）直接定位到down所在的位置
- 详细的其他信息可以通过info args , info locals进行定位

2、如果以上仍不能定位到问题，或者bt定位不是很准确，那么可以通过加入调试打印、日志等手段。



**对于大部分公司所使用的平台封装等原因，会在代码中加入段错误信号触发机制，比如：**

```
void main()
{
    signal(SIGSEGV, &core_dump_fcn); 
    function (); 
    return 0;
}
void dump(int signo) 
{
	...
   strings = backtrace_symbols (array, size);//字符串数组
   output();
	...
}

```

当某个进程挂起，那么就会直接打印函数栈调用信息。
