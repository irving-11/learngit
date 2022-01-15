

写入时复制（英语：Copy-on-write，简称COW）是一种计算机程序设计领域的优化策略。其核心思想是，如果有多个调用者（callers）同时请求相同资源（如内存或磁盘上的数据存储），他们会共同获取相同的指针指向相同的资源，直到某个调用者试图修改资源的内容时，系统才会真正复制一份专用副本（private copy）给该调用者，而其他调用者所见到的最初的资源仍然保持不变。这过程对其他的调用者都是透明的（transparently）。此作法主要的优点是如果调用者没有修改该资源，就不会有副本（private copy）被建立，因此多个调用者只是读取操作时可以共享同一份资源。

参考链接：https://juejin.cn/post/6844903702373859335



fork():

- fork作为一个函数被调用。这个函数会有**两次返回**，将**子进程的PID返回给父进程，0返回给子进程**。(如果小于0，则说明创建子进程失败)。
- 再次说明：当前进程调用`fork()`，会创建一个跟当前进程完全相同的子进程(除了pid)，所以子进程同样是会执行`fork()`之后的代码。

所以说：

- 父进程在执行if代码块的时候，`fpid变量`的值是子进程的pid
- 子进程在执行if代码块的时候，`fpid变量`的值是0



也可将代码注入到空闲空间中，需要用到/proc/pid/maps文件的内容。

```c
long freespaceaddr(pid_t pid)
{
    FILE *fp;
    char filename[30];
    char line[85];
    long addr;
    char str[20];
    sprintf(filename, "/proc/%d/maps", pid);
    fp = fopen(filename, "r");
}
```

参考文章：

Playing with ptrace, Part I	https://www.linuxjournal.com/article/6100
