---
layout: post
title: Linux 的僵尸(zombie)进程
date: 2009/4/25/ 7:28:42
updated: 2009/4/25/ 7:28:42
status: publish
published: true
type: post
---

可能很少有人意识到，在一个进程调用了exit之后，该进程 并非马上就消失掉，而是留下一个称为僵尸进程（Zombie）的数据结构。在Linux进程的5种状态中，僵尸进程是非常特殊的一种，它已经放弃了几乎所 有内存空间，没有任何可执行代码，也不能被调度，仅仅在进程列表中保留一个位置，记载该进程的退出状态等信息供其他进程收集，除此之外，僵尸进程不再占有 任何内存空间。


僵尸进程的来由，要追溯到Unix，Unix的设计者们设计这个东西并非是因为闲来无事想装装酷什么的。上面说到，僵尸进程中保存着很多对程序员和系统管理员非常重要的信息，首先，这个进程是怎么死亡的？是正常退出呢，还是出现了错误，还是被其它进程强迫退出的？也就是说，这个程序的退出码是什么？其次，这个进程占用的总系统CPU时间和总用户CPU时间分别是多少？发生页错误的数目和收到信号的数目。这些信息都被存储在僵尸进程中，试想如果没有僵尸进程，进程执行多长我们并不知道，一旦其退出，所有与之相关的信息都立刻都从系统中清除，而如果此时父进程或系统管理员需要用到，就只好干瞪眼了。



所以，进程退出后，系统会把该进程的状态变成Zombie，然后给上一定的时间等着父进程来收集其退出信息，因为可能父进程正忙于别的事情来不及收集，所以，使用Zombie状态表示进程退出了，正在等待父进程收集信息中。


Zombie进程不可以用kill命令清楚，因为进程已退出，如果需要清除这样的进程，那么需要清除其父进程，或是等很长的时间后被内核清除。因为Zombie的进程还占着个进程ID号呢，这样的进程如果很多的话，不利于系统的进程调度。


下面，让我们来看看一个示例：



```

/* zombie.c */
#include <sys/types.h>
#include <unistd.h>  main()
{
    pid_t pid; 
    pid=fork();
    if(pid<0) { /* 如果出错 */ 
        printf("error occurred!\n");
    }else if(pid==0){ /* 如果是子进程 */ 
        exit(0);
    }else{  /* 如果是父进程 */ 
        sleep(60);  /* 休眠60秒 */ 
        wait(NULL); /* 收集僵尸进程 */
    }
}


```

编译这个程序：


`$ cc zombie.c -o zombie`


后台运行程序，以使我们能够执行下一条命令



```

$ ./zombie &
[1] 1217

```

列一下系统内的进程



```

$ ps -ax
... ...
1137   pts/0   S   0:00   -bash
1217   pts/0   S   0:00   ./zombie
1218   pts/0   Z   0:00   [zombie]
1578   pts/0   R   0:00   ps   -ax

```

其中的”Z”就是僵尸进程的标志，它表示1218号进程现在就是一个僵尸进程。


收集Zombie进程的信息，并终结这些僵尸进程，需要我们在父进程中使用waitpid调用和wait调用。这两者的作用都是收集僵尸进程留下的信息，同时使这个进程彻底消失。



**（转载本站文章请注明作者和出处 [酷 壳 – CoolShell](https://coolshell.cn/) ，请勿用于任何商业用途）**



### 相关文章

* [![eBPF 介绍](https://coolshell.cn/wp-content/uploads/2022/12/eBPF-150x150.jpeg)](https://coolshell.cn/articles/22320.html)[eBPF 介绍](https://coolshell.cn/articles/22320.html)
* [![打造高效的工作环境 – Shell 篇](https://coolshell.cn/wp-content/uploads/2019/03/linux.ninja_-150x150.png)](https://coolshell.cn/articles/19219.html)[打造高效的工作环境 – Shell 篇](https://coolshell.cn/articles/19219.html)
* [![记一次Kubernetes/Docker网络排障](https://coolshell.cn/wp-content/uploads/2018/12/docker-networking-1-150x150.png)](https://coolshell.cn/articles/18654.html)[记一次Kubernetes/Docker网络排障](https://coolshell.cn/articles/18654.html)
* [![程序员练级攻略（2018)  与我的专栏](https://coolshell.cn/wp-content/uploads/2018/05/300x262-150x150.jpg)](https://coolshell.cn/articles/18360.html)[程序员练级攻略（2018) 与我的专栏](https://coolshell.cn/articles/18360.html)
* [![Linux PID 1 和 Systemd](https://coolshell.cn/wp-content/uploads/2017/07/systemd-1-150x150.jpeg)](https://coolshell.cn/articles/17998.html)[Linux PID 1 和 Systemd](https://coolshell.cn/articles/17998.html)
* [![缓存更新的套路](https://coolshell.cn/wp-content/uploads/2016/07/cache-150x150.png)](https://coolshell.cn/articles/17416.html)[缓存更新的套路](https://coolshell.cn/articles/17416.html)
The post [Linux 的僵尸(zombie)进程](https://coolshell.cn/articles/656.html) first appeared on [酷 壳 - CoolShell](https://coolshell.cn).