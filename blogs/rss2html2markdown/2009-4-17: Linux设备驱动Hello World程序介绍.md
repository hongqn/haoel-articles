---
layout: post
title: Linux设备驱动Hello World程序介绍
date: 2009/4/17/ 17:19:52
updated: 2009/4/17/ 17:19:52
status: publish
published: true
type: post
---

by Valerie Henson  

07/05/2007


(**译者注：本文的例子是只能在linux的2.6内核下使用的，2.6以上的内核，译者没有做过实验，2.4是要修改make文件才能运行**。)


本文的出处：[这里](http://www.linuxdevcenter.com/pub/a/linux/2007/07/05/devhelloworld-a-simple-introduction-to-device-drivers-under-linux.html?page=1)


自古以来，学习一门新编程语言的第一步就是写一个打印“hello world”的程序（可以看[《hello world 集中营》](https://coolshell.cn/articles/169.html)这个帖子供罗列了300个“hello world”程序例子）在本文中，我们将用同样的方式学习如何编写一个简单的linux内核模块和设备驱动程序。我将学习到如何在内核模式下以三种不同的方式来打印hello world，这三种方式分别是： printk()，/proc文件，/dev下的设备文件。


#### 准备：安装内核模块的编译环境


一个内核模块kernel module是一段能被内核动态加载和卸载的内核代码，因为内核模块程序是内核的一个部分，并且和内核紧密的交互，所以内核模块不可能脱离内核编译环境，至少，它需要内核的头文件和用于加载的配置信息。编译内核模块同样需要相关的开发工具，比如说编译器。为了简化，本文只简要讨论如何在Debian、Fedora和其他以.tar.gz形式提供的原版linux内核下进行核模块的编译。在这种情况下，你必须根据你正在运行内核相对应的内核源代码来编译你的内核模块kernel module(当你的内核模块一旦被装载到你内核中时，内核就将执行该模块的代码)



必须要注意内核源代码的位置，权限：内核程序通常在/usr/src/linux目录下，并且属主是root。如今，推荐的方式是将内核程序放在一个非root用户的home目录下。本文中所有命令都运行在非root的用户下，只有在必要的时候，才使用sudo来获得临时的root权限。配置和使用sudo可以man sudo(8) visudo(8) 和sudoers(5)。或者切换到root用户下执行相关的命令。不管什么方式，你都需要root权限才能执行本文中的一些命令。


在Debian下编译内核模块的准备


使用如下的命令安装和配置用于在Debian编译内核模块的module-assitant包



```

$ sudo apt-get install module-assistant

```

以此你就可以开始编译内核模块，你可以在[《Debian Linux Kernel Handbook》](http://kernel-handbook.alioth.debian.org/)这本书中找到对Debian内核相关任务的更深度的讨论。


Fedora的kernel-devel包包含了你编译Fedora内核模块的所有必要内核头文件和工具。你可以通过如下命令得到这个包。


`$ sudo yum install kernel-devel`


有了这个包，你就可以编译你的内核模块kernel modules。关于Fedora编译内核模块的相关文档你可以从[Fedora release notes](http://docs.fedoraproject.org/release-notes/fc6/en_US/sn-Kernel.html#id2950723)中找到。


一般Linux 内核源代码和配置


(译者注，下面的编译很复杂，如果你的Linux不是上面的系统，你可以使用REHL AS4系统，这个系统的内核就是2.6的内核，并且可以通过安装直接安装内核编译支持环境，从而就省下了如下的步骤。而且下面的步骤比较复杂，建议在虚拟机安装Linux进行实验。)


如果你选择使用一般的Linux内核源代吗，你必须，配置，编译，安装和重启的你编译内核。这个过程非常复杂，并且本文只会讨论使用一般内核源代码的基本概念。


linux的著名的内核源代码在http://kernel.org上都可以找到。最近新发布的稳定版本的代码在首页上。下载全版本的源代码，不要下载补丁代码。例如，当前发布稳定版本在url: http://kernel.org/pub/linux/kernel/v2.6/linux-2.6.21.5.tar.bz2上。如果需要更快速的下载，从htpp://kernel.org/mirrors上找到最近的镜像进行下载。最简单获得源代码的方式是以断点续传的方式使用wget。如今的http很少发生中断，但是如果你在下载过程中发生了中断，这个命令将帮助你继续下载剩下的部分。


`$ wget -c http://kernel.org/pub/linux/kernel/v2.6/linux-2.6.21.5.tar.bz2` 


解包内核源代码


`$ tar xjvf linux-<version>.tar.bz2`


现在你的内核源代码位于linux-/目录下。转到这个目录下，并配置它：



```

$ cd linux-<version>
$ make menuconfig
```

一些非常易用的编译目标make targets提供了多种编译安装内核的形式：Debian 包，RPM包，gzip后的tar文件 等等，使用如下命令查看所有可以编译的目标形式


`$ make help`


一个可以工作在任何linux的目标是：(译者注：REHL AS4上没有tar-pkg这个目标，你可以任选一个rpm编译，编译完后再上层目录可以看到有一个linux-.tar.gz可以使用)


`$ make tar-pkg`


当编译完成后，可以调用如下命令安装你的内核


`$ sudo tar -C / -xvf linux-<version>.tar`


在标准位置建立的到内核源代码的链接


`$ sudo ln -s <location of top-level source directory> /lib/modules/'uname -r'/build`


现在已经内核源代码已经可以用于编译内核模块了，重启你的机器以使得你根据新内核程序编译的内核可以被装载。


#### 使用printk()函数打印”Hello World”


我们的第一个内核模块，我们将以一个在内核中使用函数printk()打印”Hello world”的内核模块为开始。printk是内核中的printf函数。printk的输出打印在内核的消息缓存kernel message buffer并拷贝到/var/log/messages(关于拷贝的变化依赖于如何配置syslogd)


下载[hello\_printk](http://www.linuxdevcenter.com/linux/2007/07/05/examples/hello_printk.tar.gz) 模块的tar包 并解包：


`$ tar xzvf hello_printk.tar.gz`


这个包中包含两个文件:Makefile，里面包含如何创建内核模块的指令和一个包含内核模块源代码的hello\_printk.c文件。首先，我们将简要的过一下这个Makefile 文件。


`obj-m := hello_printk.o`


obj-m指出将要编译成的内核模块列表。.o格式文件会自动地有相应的.c文件生成(不需要显示的罗列所有源代码文件)



```

KDIR  := /lib/modules/$(shell uname -r)/build

```

KDIR表示是内核源代码的位置。在当前标准情况是链接到包含着正在使用内核对应源代码的目录树位置。



```

PWD := $(shell pwd)

```

PWD指示了当前工作目录并且是我们自己内核模块的源代码位置



```

default:
     $(MAKE) -C $(KDIR) M=$(PWD) modules

```

default是默认的编译连接目标；即，make将默认执行本条规则编译目标，除非程序员显示的指明编译其他目标。这里的的编译规则的意思是，在包含内核源代码位置的地方进行make,然后之编译$(PWD)(当前)目录下的modules。这里允许我们使用所有定义在内核源代码树下的所有规则来编译我们的内核模块。


现在我们来看看hello\_printk.c这个文件



```

#include
	<linux/init.h>
#include
	<linux/module.h>

```

这里包含了内核提供的所有内核模块都需要的头文件。这个文件中包含了类似module\_init()宏的定义，这个宏稍后我们将用到



```

static int __init
hello_init(void){
    printk("Hello, world!n");
    return 0;
}

```

这是内核模块的初始化函数，这个函数在内核模块初始化被装载的时候调用。\_\_init关键字告诉内核这个代码只会被运行一次，而且是在内核装载的时候。printk()函数这一行将打印一个”Hello, world”到内核消息缓存。printk参数的形式在大多数情况和printf(3)一模一样。



```

module_init(hello_init); 
module_init()

```

宏告诉内核当内核模块第一次运行时哪一个函数将被运行。任何在内核模块中其他部分都会受到内核模块初始化函数的影响。



```

static void __exit
hello_exit(void){
    printk("Goodbye, world!n");
}
module_exit(hello_exit);

```

同样地，退出函数也只在内核模块被卸载的时候会运行一次，module\_exit()宏标示了退出函数。\_\_exit关键字告诉内核这段代码只在内核模块被卸载的时候运行一次。



```

MODULE_LICENSE("GPL");
MODULE_AUTHOR("Valerie Henson val@nmt.edu");
MODULE_DESCRIPTION("Hello, world!" minimal module");
MODULE_VERSION("printk");
MODULE_LICENSE()

```

宏告诉内核，内核模块代码在什么样的license之下，这将影响主那些符号(函数和变量，等等)可以访问主内核。GPLv2 下的模块(如同本例子中)能访问所有的符号。某些内核模块license将会损害内核开源的特性，这些license指示内核将装载一些非公开或不受信的代码。如果内核模块不使用MODULE\_LICENSE()宏，就被假定为非GPLv2的，这会损害内核的开源特性，并且大部分Linux内核开发人员都会忽略来自受损内核的bug报告，因为他们无法访问所有的源代码，这使得调试变得更加困难。剩下的MODULE\_\*()这些宏以标准格式提供有用的标示该内核模块的信息(译者注：这里意思是，你必须使用GPLv2的license，否则你的驱动程序很有可能得不到Linux社区的开发者的支持 ：）)


现在，开始编译和运行代码。转到相应的目录下，编译内核模块



```

$ cd hello_printk  
$ make

```

接着，装载内核模块，使用insmod指令，并且通过dmesg来检查打印出的信息，dmesg是打印内核消息缓存的程序。



```

$ sudo insmod ./hello_printk.ko  
$ dmesg | tail

```

你将从dmesg的屏幕输出中看见”Hello world!”信息。现在卸载使用rmmod卸载内核模块，并检查退出信息。



```

$ sudo rmmod hello_printk  
$ dmesg | tail

```

到此，你就成功地完成了对内核模块的编译和安装！


#### 使用/proc的Hello, World!


一种用户程序和内核通讯最简单和流行的方式是通过使用/proc下文件系统进行通讯。/proc是一个伪文件系统，从这里的文件读取的数据是由内核返回的数据，并且写入到这里面的数据将会被内核读取和处理。在使用/proc方式之前，所用用户和内核之间的通讯都不得不使用系统调用来完成。使用系统调用意味着你将在要在查找已经具有你需要的行为方式的系统调用(一般不会出现这种情况)，或者创建一种新的系统调用来满足你的需求(这样就要求对内核全局做修改，并增加系统调用的数量，这是通常是非常不好的做法)，或者使用ioctl这个万能系统调用，这就要求要创建一个新文件类型供ioctl操作(这也是非常复杂而且bug比较多的方式，同样是非常繁琐的)。/proc提供了一个简单的，无需定义的方式在用户空间和内核之间传递数据，这种方式不仅可以满足内核使用，同样也提供足够的自由度给内核模块做他们需要做的事情。


为了满足我们的要求，我们需要当我们读在/proc下的某一个文件时将会返回一个“Hello world!”。我们将使用/proc/hello\_world这个文件。下载并解开[hello proc](http://www.linuxdevcenter.com/linux/2007/07/05/examples/hello_proc.tar.gz)这个gzip的tar包后，我们将首先来看一下[hello\_proc.c](http://www.linuxdevcenter.com/linux/2007/07/05/examples/hello_proc.c)这个文件



```

#include <linux/init.h>
#include <linux/module.h>
#include <linux/proc_fs.h>

```

这次，我们将增加一个proc\_fs头文件，这个头文件包括驱动注册到/proc文件系统的支持。当另外一个进程调用read()时，下一个函数将会被调用。这个函数的实现比一个完整的普通内核驱动的read系统调用实现要简单的多，因为我们仅做了让”Hello world”这个字符串缓存被一次读完。



```

static int
hello_read_proc(char *buffer, char **start,off_t offset,
                int size, int *eof, void *data)
{

```

这个函数的参数值得明确的解释一下。buffer是指向内核缓存的指针，我们将把read输出的内容写到这个buffer中。start参数多用更复杂的/proc文件；我们在这里将忽略这个参数；并且我只明确的允许offset这个的值为0。size是指buffer中包含多字节数；我们必须检查这个参数已避免出现内存越界的情况，eof参数一个EOF的简写，用于返回文件是否已经读到结束，而不需要通过调用read返回0来判断文件是否结束。这里我们不讨论依靠更复杂的/proc文件传输数据的方法。这个函数方法体罗列如下：



```

    char *hello_str = "Hello, world!\n";
    int len = strlen(hello_str); /* Don't include the null byte. */
    /*     * We only support reading the whole string at once.     */
    if (size < len)
        return< -EINVAL;
    /*     * If file position is non-zero, then assume the string has
    * been read and indicate there is no more data to be read.
    */
    if (offset != 0)
        return 0;
    /*     * We know the buffer is big enough to hold the string.     */
    strcpy(buffer, hello_str);
    /*     * Signal EOF.     */
    *eof = 1;
    return len;
}

```

下面，我们需将内核模块在初始化函数注册在/proc 子系统中。



```

static int __init
hello_init(void){
    /*
    * Create an entry in /proc named "hello_world" that calls
    * hello_read_proc() when the file is read.
    */
    if (create_proc_read_entry("hello_world", 0, 
                        NULL, hello_read_proc, NULL) == 0) {
        printk(KERN_ERR
        "Unable to register "Hello, world!" proc filen");
        return -ENOMEM;
    }
    return 0;
}
module_init(hello_init);

```

当内核模块卸载时，需要在/proc移出注册的信息(如果我们不这样做的，当一个进程试图去访问/proc/hello\_world，/proc文件系统将会试着执行一个已经不存在的功能，这样将会导致内核崩溃)



```

static void __exit
hello_exit(void){
    remove_proc_entry("hello_world", NULL);
}
module_exit(hello_exit);
MODULE_LICENSE("GPL");
MODULE_AUTHOR("Valerie Henson val@nmt.edu");
MODULE_DESCRIPTION(""Hello, world!" minimal module");
MODULE_VERSION("proc");

```

下面我们将准备编译和装载模组



```

$ cd hello_proc  
$ make  
$ sudo insmod ./hello_proc.ko

```

现在，将会有一个称为/proc/hello\_world的文件，并且读这个文件的，将会返回一个”Hello world”字符串。



```

$ cat /proc/hello_world
Hello, world!

```

你可以为为同一个驱动程序创建多个/proc文件，并增加相应写/proc文件的函数，创建包含多个/proc文件的目录，或者更多的其他操作。如果要写比这个更复杂的驱动程序，可以使用seq\_file函数集来编写是更安全和容易的。关于这些更多的信息可以看[《Driver porting: The seq\_file interface》](http://lwn.net/Articles/22355/)


#### Hello, World! 使用 /dev/hello\_world


现在我们将使用在/dev目录下的一个设备文件/dev/hello\_world实现”Hello,world!” 。追述以前的日子，设备文件是通过MAKEDEV脚本调用mknod命令在/dev目录下产生的一个特定的文件，这个文件和设备是否运行在改机器上无关。到后来设备文件使用了devfs，devfs在设备第一被访问的时候创建/dev文件，这样将会导致很多有趣的加锁问题和多次打开设备文件的检查设备是否存在的重试问题。当前的/dev版本支持被称为udev，因为他将在用户程序空间创建到/dev的符号连接。当内核模块注册设备时，他们将出现在sysfs文件系统中，并mount在/sys下。一个用户空间的程序，udev,注意到/sys下的改变将会根据在/etc/udev/下的一些规则在/dev下创建相关的文件项。


下载[hello world](http://www.linuxdevcenter.com/linux/2007/07/05/examples/hello_dev.tar.gz)内核模块的gzip的tar包，我们将开始先看一下hello\_dev.c这个源文件。



```

#include <linux/fs.h>
#include <linux/init.h>
#include <linux/miscdevice.h>
#include <linux/module.h>
#include <asm/uaccess.h>

```

正如我们看到的必须的头文件外，创建一个新设备还需要更多的内核头文件支持。fs.sh包含所有文件操作的结构，这些结构将由设备驱动程序来填值，并关联到我们相关的/dev文件。miscdevice.h头文件包含了对通用miscellaneous设备文件注册的支持。 asm/uaccess.h包含了测试我们是否违背访问权限读写用户内存空间的函数。hello\_read将在其他进程在/dev/hello调用read()函数被调用的是一个函数。他将输出”Hello world!”到由read()传入的缓存。



```

static ssize_t hello_read(struct file * file, char * buf, size_t count, loff_t *ppos)
{
    char *hello_str = "Hello, world!n";
    int len = strlen(hello_str); /* Don't include the null byte. */
    /*     * We only support reading the whole string at once.     */
    if (count < len)
        return -EINVAL;
    /*
    * If file position is non-zero, then assume the string has
    * been read and indicate there is no more data to be read.
    */
    if (*ppos != 0)
        return 0;
    /*
    * Besides copying the string to the user provided buffer,
    * this function also checks that the user has permission to
    * write to the buffer, that it is mapped, etc.
    */
    if (copy_to_user(buf, hello_str, len))
        return -EINVAL;
    /*
    * Tell the user how much data we wrote.
    */
    *ppos = len;
    return len;
}

```

下一步，我们创建一个文件操作结构file operations struct，并用这个结构来定义当文件被访问时执行什么动作。在我们的例子中我们唯一关注的文件操作就是read。



```

static const struct file_operations hello_fops = {
    .owner        = THIS_MODULE,
    .read        = hello_read,
};

```

现在，我们将创建一个结构，这个结构包含有用于在内核注册一个通用miscellaneous驱动程序的信息。



```

static struct miscdevice hello_dev = {
    /*
    * We don't care what minor number we end up with, so tell the
    * kernel to just pick one.
    */
    MISC_DYNAMIC_MINOR,
    /*     
    * Name ourselves /dev/hello.     
    */
    "hello",
    /*     
    * What functions to call when a program performs file
    * operations on the device.
    */
    &hello_fops
};

```

在通常情况下，我们在init中注册设备



```

static int __init
hello_init(void){
    int ret;
    /*
    * Create the "hello" device in the /sys/class/misc directory.
    * Udev will automatically create the /dev/hello device using
    * the default rules.
    */
    ret = misc_register(&hello_dev);
    if (ret)
        printk(KERN_ERR
            "Unable to register "Hello, world!" misc devicen");
    return ret;
}
module_init(hello_init);

```

接下是在卸载时的退出函数



```

static void __exit
hello_exit(void){
    misc_deregister(&hello_dev);
}
module_exit(hello_exit);
MODULE_LICENSE("GPL");
MODULE_AUTHOR("Valerie Henson val@nmt.edu>");
MODULE_DESCRIPTION(""Hello, world!" minimal module");
MODULE_VERSION("dev");

```

编译并加载模块:



```

$ cd hello_dev  
$ make  
$ sudo insmod ./hello_dev.ko

```

现在我们将有一个称为/dev/hello的设备文件，并且这个设备文件被root访问时将会产生一个”Hello, world!”



```

$ sudo cat /dev/hello
 Hello, world!
 
```

但是我们不能使用普通用户访问他:



```

$ cat /dev/hello 
cat:/dev/hello: Permission denied  

$ ls -l 
/dev/hello crw-rw---- 1 root root 10, 61 2007-06-20 14:31 /dev/hello


```

这是有默认的udev规则导致的，这个条规将标明当一个普通设备出现时，他的名字将会是/dev/，并且默认的访问权限是0660(用户和组读写访问，其他用户无法访问)。我们在真实情况中可能会希望创建一个被普通用户访问的设备驱动程序，并且给这个设备起一个相应的连接名。为达到这个目的，我们将编写一条udev规则。


udev规则必须做两件事情：第一创建一个符号连接，第二修改设备的访问权限。


下面这条规则可以达到这个目的：


`KERNEL=="hello", SYMLINK+="hello_world", MODE="0444"`


我们将详细的分解这条规则，并解释每一个部分。KERNEL==”hello” 标示下面的的规则将作用于/sys中设备名字”hello”的设备(==是比较符)。hello 设备是我们通过调用misc\_register()并传递了一个包含设备名为”hello”的文件操作结构file\_operations为参数而达到的。你可以自己通过如下的命令在/sys下查看



```

$ ls -d /sys/class/misc/hello//sys/class/misc/hello/

```

SYMLINK+=”hello\_world” 的意思是在符号链接列表中增加 (+= 符号的意思着追加)一个hello\_world ，这个符号连接在设备出现时创建。在我们场景下，我们知道我们的列表的中的只有这个符号连接，但是其他设备驱动程序可能会存在多个不同的符号连接，因此使用将设备追加入到符号列表中，而不是覆盖列表将会是更好的实践中的做法。


MODE=”0444″的意思是原始的设备的访问权限是0444,这个权限允许用户，组，和其他用户可以访问。


通常，使用正确的操作符号(==, +=, or =)是非常重要的，否则将会出现不可预知的情况。


现在我们理解这个规则是怎么工作的，让我们将其安装在/etc/udev目录下。udev规则文件以和System V初始脚本目录命名的同种方式的目录下，/etc/udeve/rules.d这个目录，并以字母/数字的顺序。和System V的初始化脚本一样，/etc/udev/rules.d下的目录通常符号连接到真正的文件，通过使用符号连接名，将使得规则文件已正确的次序得到执行。  

使用如下的命令，拷贝hello.rules文件从/hello\_dev目录到/etc/udev目录下，并创建一一个最先被执行的规则文件链接在/etc/udev/rules.d目录下。



```

$ sudo cp hello.rules /etc/udev/  
$ sudo ln -s ../hello.rules /etc/udev/rules.d/010_hello.rules

```

现在我们重新装载驱动程序，并观察新的驱动程序项



```

$ sudo rmmod hello_dev  
$ sudo insmod ./hello_dev.ko  
$ ls -l /dev/hello*  
cr--r--r-- 1 root root 10, 61 2007-06-19 21:21 /dev/hello  
lrwxrwxrwx 1 root root      5 2007-06-19 21:21 /dev/hello_world -> hello

```

最后，检查你可以使用普通用户访问/dev/hello\_world设备.



```

$ cat /dev/hello_world
Hello, world!  

$ cat /dev/hello
Hello, world!

```

更多编写udev规则的信息可以在Daniel Drake的文章[Writing udev rules](http://www.reactivated.net/writing_udev_rules.html)中找到。



**（转载本站文章请注明作者和出处 [酷 壳 – CoolShell](https://coolshell.cn/) ，请勿用于任何商业用途）**



### 相关文章

* [![eBPF 介绍](https://coolshell.cn/wp-content/uploads/2022/12/eBPF-150x150.jpeg)](https://coolshell.cn/articles/22320.html)[eBPF 介绍](https://coolshell.cn/articles/22320.html)
* [![打造高效的工作环境 – Shell 篇](https://coolshell.cn/wp-content/uploads/2019/03/linux.ninja_-150x150.png)](https://coolshell.cn/articles/19219.html)[打造高效的工作环境 – Shell 篇](https://coolshell.cn/articles/19219.html)
* [![记一次Kubernetes/Docker网络排障](https://coolshell.cn/wp-content/uploads/2018/12/docker-networking-1-150x150.png)](https://coolshell.cn/articles/18654.html)[记一次Kubernetes/Docker网络排障](https://coolshell.cn/articles/18654.html)
* [![程序员练级攻略（2018)  与我的专栏](https://coolshell.cn/wp-content/uploads/2018/05/300x262-150x150.jpg)](https://coolshell.cn/articles/18360.html)[程序员练级攻略（2018) 与我的专栏](https://coolshell.cn/articles/18360.html)
* [![Linux PID 1 和 Systemd](https://coolshell.cn/wp-content/uploads/2017/07/systemd-1-150x150.jpeg)](https://coolshell.cn/articles/17998.html)[Linux PID 1 和 Systemd](https://coolshell.cn/articles/17998.html)
* [![缓存更新的套路](https://coolshell.cn/wp-content/uploads/2016/07/cache-150x150.png)](https://coolshell.cn/articles/17416.html)[缓存更新的套路](https://coolshell.cn/articles/17416.html)
The post [Linux设备驱动Hello World程序介绍](https://coolshell.cn/articles/566.html) first appeared on [酷 壳 - CoolShell](https://coolshell.cn).