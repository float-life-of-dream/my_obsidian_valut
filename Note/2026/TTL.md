[![](http://www.linusakesson.net/img/linus1.png)](http://www.linusakesson.net/index.php)

[linusakesson.net](http://www.linusakesson.net/index.php)

[(show navigation)](http://www.linusakesson.net/programming/tty/#)

## The TTY demystified TTY 揭秘

![Teletypes](http://www.linusakesson.net/programming/tty/oldschool.jpg)

Real teletypes in the 1940s.  
20 世纪 40 年代的真实电传打字机。

The TTY subsystem is central to the design of Linux, and UNIX in general. Unfortunately, its importance is often overlooked, and it is difficult to find good introductory articles about it. I believe that a basic understanding of TTYs in Linux is essential for the developer and the advanced user.  
TTY 子系统是 Linux 乃至整个 UNIX 系统设计的核心。然而，它的重要性常常被忽视，而且很难找到优秀的入门文章。我认为，对于开发者和高级用户来说，对 Linux 中的 TTY 有一个基本的了解至关重要。

Beware, though: What you are about to see is not particularly elegant. In fact, the TTY subsystem — while quite functional from a user's point of view — is a twisty little mess of special cases. To understand how this came to be, we have to go back in time.  
不过，请注意：您即将看到的内容并不十分优雅。事实上，TTY 子系统虽然从用户角度来看功能齐全，但却是由各种特殊情况组成的复杂系统。要了解其由来，我们必须追溯到过去。

## History 历史

In 1869, the *stock ticker* was invented. It was an electro-mechanical machine consisting of a typewriter, a long pair of wires and a ticker tape printer, and its purpose was to distribute stock prices over long distances in realtime. This concept gradually evolved into the faster, ASCII-based *teletype*. Teletypes were once connected across the world in a large network, called *Telex*, which was used for transferring commercial telegrams, but the teletypes weren't connected to any computers yet.  
1869 年， *股票行情显示屏* 被发明出来。它是一种机电式设备。 机器由一台打字机、一对长长的电线和一条电报带组成。 打印机，其目的是远距离分发股票价格。 实时。这一概念逐渐演变为速度更快、基于 ASCII 的编码方式。 *电传打字机* 。电传打字机曾经通过一个名为 *Telex* 的大型网络连接在世界各地，用于传输商业电报，但当时的电传打字机还没有连接到任何计算机。

Meanwhile, however, the computers — still quite large and primitive, but able to multitask — were becoming powerful enough to be able to interact with users in realtime. When the command line eventually replaced the old batch processing model, teletypes were used as input and output devices, because they were readily available on the market.  
然而，与此同时，计算机——尽管体积仍然相当庞大且结构原始，但已具备多任务处理能力——其性能已足以与用户进行实时交互。当命令行最终取代旧的批处理模式时，由于电传打字机在市场上随处可见，因此被用作输入输出设备。

There was a plethora of teletype models around, all slightly different, so some kind of software compatibility layer was called for. In the UNIX world, the approach was to let the operating system kernel handle all the low-level details, such as word length, baud rate, flow control, parity, control codes for rudimentary line editing and so on. Fancy cursor movements, colour output and other advanced features made possible in the late 1970s by solid state *video terminals* such as the VT-100, were left to the applications.  
当时市面上有很多种电传打字机型号，每一种都略有不同，所以 需要某种软件兼容层。在 UNIX 世界中， 这种方法是让操作系统内核处理所有底层操作。 详细信息，例如字长、波特率、流量控制、奇偶校验、控制码 用于基本的行编辑等功能。花哨的光标移动、彩色输出 以及20世纪70年代后期固态技术带来的其他先进功能 VT-100 等 *视频终端* 则留给了应用开发者自行决定。

In present time, we find ourselves in a world where physical teletypes and video terminals are practically extinct. Unless you visit a museum or a hardware enthusiast, all the TTYs you're likely to see will be emulated video terminals — software simulations of the real thing. But as we shall see, the legacy from the old cast-iron beasts is still lurking beneath the surface.  
如今，实体电传打字机和视频终端几乎绝迹。除非你去博物馆或拜访硬件爱好者，否则你看到的电传打字机很可能都是模拟视频终端——用软件模拟真实设备。但正如我们将看到的，这些老式铁制设备的遗迹仍然潜藏在表面之下。

## The use cases 用例

![Diagram](http://www.linusakesson.net/programming/tty/case1.png)

A user types at a terminal (a physical teletype). This terminal is connected through a pair of wires to a *UART* (Universal Asynchronous Receiver and Transmitter) on the computer. The operating system contains a *UART driver* which manages the physical transmission of bytes, including parity checks and flow control. In a naïve system, the UART driver would then deliver the incoming bytes directly to some application process. But such an approach would lack the following essential features:  
用户在终端（物理电传打字机）上输入内容。该终端通过一对导线连接到计算机上的 *UART* （通用异步收发器）。操作系统包含一个 *UART 驱动程序* ，用于管理字节的物理传输，包括奇偶校验和流量控制。在一个简单的系统中，UART 驱动程序会将接收到的字节直接传递给某个应用程序进程。但这种方法会缺少以下几个关键特性：

**Line editing.** Most users make mistakes while typing, so a backspace key is often useful. This could of course be implemented by the applications themselves, but in accordance with the UNIX design philosophy, applications should be kept as simple as possible. So as a convenience, the operating system provides an editing buffer and some rudimentary editing commands (backspace, erase word, clear line, reprint), which are enabled by default inside the *line discipline*. Advanced applications may disable these features by putting the line discipline in *raw* mode instead of the default *cooked* (or *canonical*) mode. Most interactive applications (editors, mail user agents, shells, all programs relying on curses or readline) run in raw mode, and handle all the line editing commands themselves. The line discipline also contains options for character echoing and automatic conversion between carriage returns and linefeeds. Think of it as a primitive kernel-level sed(1), if you like.  
**行编辑。** 大多数用户在打字时都会出错，所以需要一个退格键。 密钥通常很有用。当然，这可以通过应用程序来实现。 它们本身，但根据 UNIX 设计理念，应用程序 应该尽可能保持简单。因此，为了方便起见，操作系统 提供编辑缓冲区和一些基本的编辑命令（退格键、 擦除单词、清除行、重印），这些功能在默认情况下是启用的。 *线条规整* 。高级应用程序可以通过将线条规整设置为 *原始* 模式（而非默认模式）来禁用这些功能。 *已烹饪* （或 *规范* ）模式。大多数交互式应用程序（编辑器、邮件用户代理、shell、所有依赖于 curses 或 readline ) 以原始模式运行，并自行处理所有行编辑命令。该行规则还包含字符回显和回车符与换行符之间自动转换的选项。您可以将其视为一个原始的内核级 sed(1) 。

Incidentally, the kernel provides several different line disciplines. Only one of them is attached to a given serial device at a time. The default discipline, which provides line editing, is called N\_TTY (drivers/char/n\_tty.c, if you're feeling adventurous). Other disciplines are used for other purposes, such as managing packet switched data (ppp, IrDA, serial mice), but that is outside the scope of this article.  
顺便一提，内核提供了几种不同的行规则。每次只有一个规则可以连接到给定的串行设备。默认规则（提供行编辑功能）称为 N\_TTY 。 （ drivers/char/n\_tty.c ，如果您有兴趣尝试一下）。其他学科则用于其他目的，例如管理分组交换数据（ppp、IrDA、串行鼠标），但这超出了本文的讨论范围。

**Session management.** The user probably wants to run several programs simultaneously, and interact with them one at a time. If a program goes into an endless loop, the user may want to kill it or suspend it. Programs that are started in the background should be able to execute until they try to write to the terminal, at which point they should be suspended. Likewise, user input should be directed to the foreground program only. The operating system implements these features in the *TTY driver* (drivers/char/tty\_io.c).  
**会话管理。** 用户可能希望同时运行多个程序，并逐个与之交互。如果某个程序陷入无限循环，用户可能希望将其终止或挂起。在后台启动的程序应该能够一直执行，直到它们尝试向终端写入数据，此时应将其挂起。同样，用户输入也应该只被定向到前台程序。操作系统在 *TTY 驱动程序* 中实现了这些功能。 ( drivers/char/tty\_io.c ).

An operating system process is "alive" (has an *execution context*), which means that it can perform actions. The TTY driver is not alive; in object oriented terminology, the TTY driver is a passive object. It has some data fields and some methods, but the only way it can actually do something is when one of its methods gets called from the context of a process or a kernel interrupt handler. The line discipline is likewise a passive entity.  
操作系统进程是“存活的”（拥有 *执行上下文* ），这意味着它可以执行操作。TTY 驱动程序并非存活的；用面向对象术语来说，TTY 驱动程序是一个被动对象。它有一些数据字段和方法，但只有当它的方法被进程或内核中断处理程序调用时，它才能真正执行操作。线路规程同样是一个被动实体。

Together, a particular triplet of UART driver, line discipline instance and TTY driver may be referred to as a *TTY device*, or sometimes just TTY. A user process can affect the behaviour of any TTY device by manipulating the corresponding device file under /dev. Write permissions to the device file are required, so when a user logs in on a particular TTY, that user must become the owner of the device file. This is traditionally done by the login(1) program, which runs with root privileges.  
UART 驱动程序、线路规程实例和 TTY 驱动程序这三个组件组合在一起，可以称为 *TTY 设备* ，有时也简称为 TTY。用户进程可以通过操作 /dev 下的相应设备文件来影响任何 TTY 设备的行为。需要对设备拥有写入权限。 文件是必需的，因此当用户登录到特定的 TTY 时，该用户必须 成为设备文件的所有者。传统上，这是由……完成的。 login(1) 程序，以 root 权限运行。

The physical line in the previous diagram could of course be a long-distance phone line:  
前图中所示的物理线路当然也可能是长途电话线：

![Diagram](http://www.linusakesson.net/programming/tty/case2.png)

This does not change much, except that the system now has to handle a modem hangup situation as well.  
这并没有太大变化，只是系统现在还需要处理调制解调器挂断的情况。

Let's move on to a typical desktop system. This is how the Linux console works:  
接下来我们来看一个典型的桌面系统。Linux 控制台的工作方式如下：

![Diagram](http://www.linusakesson.net/programming/tty/case3.png)

The TTY driver and line discipline behave just like in the previous examples, but there is no UART or physical terminal involved anymore. Instead, a video terminal (a complex state machine including a *frame buffer* of characters and graphical character attributes) is emulated in software, and rendered to a VGA display.  
TTY 驱动程序和线路规程的行为与之前的示例相同，但不再涉及 UART 或物理终端。取而代之的是，软件会模拟一个视频终端（一个复杂的状态机，包括字符 *帧缓冲区* 和图形字符属性），并将其渲染到 VGA 显示器上。

The console subsystem is somewhat rigid. Things get more flexible (and abstract) if we move the terminal emulation into userland. This is how xterm(1) and its clones work:  
控制台子系统比较僵化。但随着系统的发展，灵活性会越来越强（而且）。 摘要）如果我们把终端模拟移到用户空间。这就是方法 xterm(1) 及其克隆版本均可正常工作：

![Diagram](http://www.linusakesson.net/programming/tty/case4.png)

To facilitate moving the terminal emulation into userland, while still keeping the TTY subsystem (session management and line discipline) intact, the *pseudo terminal* or *pty* was invented. And as you may have guessed, things get even more complicated when you start running pseudo terminals inside pseudo terminals, à la screen(1) or ssh(1).  
为了便于将终端仿真移至用户空间，同时仍然 在保持 TTY 子系统（会话管理和线路纪律）完整的情况下， *伪终端* （ *pty）* 被发明了出来。正如你可能已经猜到的那样，当你在伪终端内部运行伪终端时，比如像 screen(1) 或 ssh(1) 那样，事情会变得更加复杂。

Now let's take a step back and see how all of this fits into the process model.  
现在让我们退后一步，看看这一切是如何融入流程模型的。

## Processes 流程

A Linux process can be in one of the following states:  
Linux 进程可以处于以下几种状态之一：

![Process states](http://www.linusakesson.net/programming/tty/linuxprocess.png)

| R | Running or runnable (on run queue)   正在运行或可运行（在运行队列中） |
| --- | --- |
| D | Uninterruptible sleep (waiting for some event)   不间断睡眠（等待某个事件发生） |
| S | Interruptible sleep (waiting for some event or signal)   可中断睡眠（等待某些事件或信号） |
| T | Stopped, either by a job control signal or because it is being traced by a debugger.   停止运行，可能是由于作业控制信号，也可能是因为正在被调试器跟踪。 |
| Z | Zombie process, terminated but not yet reaped by its parent.   僵尸进程，已终止但尚未被其父进程回收。 |

By running ps l, you can see which processes are running, and which are sleeping. If a process is sleeping, the WCHAN column ("wait channel", the name of the wait queue) will tell you what kernel event the process is waiting for.  
运行 ps l 命令，您可以查看哪些进程正在运行，哪些进程处于睡眠状态。如果某个进程处于睡眠状态， WCHAN 列（“等待通道”，即等待队列的名称）将显示该进程正在等待哪个内核事件。

```
$ ps l
F   UID   PID  PPID PRI  NI    VSZ   RSS WCHAN  STAT TTY        TIME COMMAND
0   500  5942  5928  15   0  12916  1460 wait   Ss   pts/14     0:00 -/bin/bash
0   500 12235  5942  15   0  21004  3572 wait   S+   pts/14     0:01 vim index.php
0   500 12580 12235  15   0   8080  1440 wait   S+   pts/14     0:00 /bin/bash -c (ps l) >/tmp/v727757/1 2>&1
0   500 12581 12580  15   0   4412   824 -      R+   pts/14     0:00 ps l
```

The " wait " wait queue corresponds to the wait(2) syscall, so these processes will be moved to the running state whenever there's a state change in one of their child processes. There are two sleeping states: Interruptible sleep and uninterruptible sleep. Interruptible sleep (the most common case) means that while the process is part of a wait queue, it may actually also be moved to the running state when a signal is sent to it. If you look inside the kernel source code, you will find that any kernel code which is waiting for an event must check if a signal is pending after schedule() returns, and abort the syscall in that case.  
“ wait ”等待队列对应于“ wait(2) ”系统调用，因此，当其子进程的状态发生变化时，这些进程将被移至运行状态。睡眠状态有两种：可中断睡眠和不可中断睡眠。可中断睡眠（最常见的情况）意味着，当进程处于等待队列中时，如果收到信号，它也可能会被移至运行状态。如果您查看内核源代码，您会发现任何等待事件的内核代码都必须在 schedule() 返回后检查是否有待处理的信号，如果有，则中止系统调用。

In the ps listing above, the STAT column displays the current state of each process. The same column may also contain one or more attributes, or flags:  
在上面的 ps 列表中， STAT 列显示每个进程的当前状态。同一列还可以包含一个或多个属性或标志：

| s | This process is a session leader. |
| --- | --- |
| + | This process is part of a foreground process group. |

These attributes are used for job control.

## Jobs and sessions

Job control is what happens when you press ^Z to suspend a program, or when you start a program in the background using &. A job is the same as a process group. Internal shell commands like jobs,fg and bg can be used to manipulate the existing jobs within a *session*. Each session is managed by a *session leader*, the shell, which is cooperating tightly with the kernel using a complex protocol of signals and system calls.

The following example illustrates the relationship between processes, jobs and sessions:

### The following shell interactions...以下壳层相互作用……

![Screenshot](http://www.linusakesson.net/programming/tty/exampleterm.png)

### ...correspond to these processes...……与这些过程相对应……

![Table](http://www.linusakesson.net/programming/tty/examplediagram.png)

### ...and these kernel structures.以及这些内核结构。

- TTY Driver (/dev/pts/0).TTY 驱动程序（ /dev/pts/0 ）。
	```
	Size: 45x13
	Controlling process group: (101)
	Foreground process group: (103)
	UART configuration (ignored, since this is an xterm):
	  Baud rate, parity, word length and much more.
	Line discipline configuration:
	  cooked/raw mode, linefeed correction,
	  meaning of interrupt characters etc.
	Line discipline state:
	  edit buffer (currently empty),
	  cursor position within buffer etc.
	```
- pipe0
	```
	Readable end (connected to PID 104 as file descriptor 0)
	Writable end (connected to PID 103 as file descriptor 1)
	Buffer
	```

The basic idea is that every pipeline is a job, because every process in a pipeline should be manipulated (stopped, resumed, killed) simultaneously. That's why kill(2) allows you to send signals to entire process groups. By default, fork(2) places a newly created child process in the same process group as its parent, so that e.g. a ^C from the keyboard will affect both parent and child. But the shell, as part of its session leader duties, creates a new process group every time it launches a pipeline.  
基本思路是，每个管道都是一个作业，因为管道中的每个进程都应该同时被操作（停止、恢复、终止）。这就是为什么 kill(2) 允许你向整个进程组发送信号。默认情况下， fork(2) 会将新创建的子进程与其父进程放在同一个进程组中，因此例如，键盘上的 ^C 会同时影响父进程和子进程。但是，作为会话领导者职责的一部分，shell 每次启动管道时都会创建一个新的进程组。

The TTY driver keeps track of the foreground process group id, but only in a passive way. The session leader has to update this information explicitly when necessary. Similarly, the TTY driver keeps track of the size of the connected terminal, but this information has to be updated explicitly, by the terminal emulator or even by the user.  
TTY 驱动程序会跟踪前台进程组 ID，但只是被动地跟踪。会话领导者必须在必要时显式更新此信息。同样，TTY 驱动程序也会跟踪已连接终端的大小，但此信息必须由终端模拟器甚至用户显式更新。

As you can see in the diagram above, several processes have /dev/pts/0 attached to their standard input. But only the foreground job (the ls | sort pipeline) will receive input from the TTY. Likewise, only the foreground job will be allowed to write to the TTY device (in the default configuration). If the cat process were to attempt to write to the TTY, the kernel would suspend it using a signal.  
如上图所示，有多个流程 /dev/pts/0 连接到它们的标准输入。但只有前台作业（ ls | sort 流水线）才能从 TTY 接收输入。同样，只有前台作业才能写入 TTY 设备（在默认配置下）。如果 cat 进程尝试写入 TTY，内核会使用信号将其挂起。

## Signal madness 信号疯狂

Now let's take a closer look at how the TTY drivers, the line disciplines and the UART drivers in the kernel communicate with the userland processes.  
现在让我们仔细看看内核中的 TTY 驱动程序、线路规程和 UART 驱动程序是如何与用户空间进程通信的。

UNIX files, including the TTY device file, can of course be read from and written to, and further manipulated by means of the magic ioctl(2) call (the Swiss army-knife of UNIX) for which lots of TTY related operations have been defined. Still, ioctl requests have to be initiated from processes, so they can't be used when the kernel needs to communicate *asynchronously* with an application.  
当然，UNIX 文件（包括 TTY 设备文件）可以通过 ioctl(2) 调用（UNIX 的瑞士军刀）进行读写和进一步操作，该调用定义了许多与 TTY 相关的操作。但是， ioctl 请求必须由进程发起，因此当内核需要与应用程序进行 *异步* 通信时，不能使用 ioctl 请求。

In *The Hitchhiker's Guide to the Galaxy*, Douglas Adams mentions an extremely dull planet, inhabited by a bunch of depressed humans and a certain breed of animals with sharp teeth which communicate with the humans by biting them very hard in the thighs. This is strikingly similar to UNIX, in which the kernel communicates with processes by sending paralyzing or deadly signals to them. Processes may intercept some of the signals, and try to adapt to the situation, but most of them don't.  
在 *《银河系漫游指南》* 中，道格拉斯·亚当斯提到了一个极其沉闷的星球，那里居住着一群抑郁的人类和一种长着锋利牙齿的动物。这种动物通过狠狠咬人类的大腿来与人类交流。这与 UNIX 系统惊人地相似，在 UNIX 系统中，内核通过向进程发送瘫痪或致命信号来与之通信。进程可能会截获一些信号并试图适应情况，但大多数进程都无法做到。

So a signal is a crude mechanism that allows the kernel to communicate asynchronously with a process. Signals in UNIX aren't clean or general; rather, each signal is unique, and must be studied individually.  
因此，信号是一种粗略的机制，它允许内核与进程进行异步通信。UNIX 中的信号并不清晰或通用；相反，每个信号都是独一无二的，必须单独研究。

You can use the command kill -l to see which signals your system implements. This is what it may look like:  
您可以使用命令 kill -l 来查看您的系统实现了哪些信号。它看起来可能像这样：

```
$ kill -l
 1) SIGHUP     2) SIGINT     3) SIGQUIT     4) SIGILL
 2) SIGTRAP     6) SIGABRT     7) SIGBUS     8) SIGFPE
 3) SIGKILL    10) SIGUSR1    11) SIGSEGV    12) SIGUSR2
4) SIGPIPE    14) SIGALRM    15) SIGTERM    16) SIGSTKFLT
5) SIGCHLD    18) SIGCONT    19) SIGSTOP    20) SIGTSTP
6) SIGTTIN    22) SIGTTOU    23) SIGURG    24) SIGXCPU
7) SIGXFSZ    26) SIGVTALRM    27) SIGPROF    28) SIGWINCH
8) SIGIO    30) SIGPWR    31) SIGSYS    34) SIGRTMIN
9) SIGRTMIN+1    36) SIGRTMIN+2    37) SIGRTMIN+3    38) SIGRTMIN+4
10) SIGRTMIN+5    40) SIGRTMIN+6    41) SIGRTMIN+7    42) SIGRTMIN+8
11) SIGRTMIN+9    44) SIGRTMIN+10    45) SIGRTMIN+11    46) SIGRTMIN+12
12) SIGRTMIN+13    48) SIGRTMIN+14    49) SIGRTMIN+15    50) SIGRTMAX-14
13) SIGRTMAX-13    52) SIGRTMAX-12    53) SIGRTMAX-11    54) SIGRTMAX-10
14) SIGRTMAX-9    56) SIGRTMAX-8    57) SIGRTMAX-7    58) SIGRTMAX-6
15) SIGRTMAX-5    60) SIGRTMAX-4    61) SIGRTMAX-3    62) SIGRTMAX-2
16) SIGRTMAX-1    64) SIGRTMAX
```

As you can see, signals are numbered starting with 1. However, when they are used in bitmasks (e.g. in the output of ps s), the least significant bit corresponds to signal 1.  
如您所见，信号从 1 开始编号。但是，当它们用于位掩码时（例如在 ps s 的输出中），最低有效位对应于信号 1。

This article will focus on the following signals: SIGHUP,SIGINT, SIGQUIT, SIGPIPE, SIGCHLD,SIGSTOP, SIGCONT, SIGTSTP, SIGTTIN,SIGTTOU and SIGWINCH.  
本文将重点关注以下信号： SIGHUP ， SIGINT, SIGQUIT, SIGPIPE, SIGCHLD, SIGSTOP, SIGCONT, SIGTSTP, SIGTTIN, SIGTTOU 和 SIGWINCH 。

### SIGHUP

- Default action: **Terminate**  
	默认操作： **终止**
- Possible actions: Terminate, Ignore, Function call  
	可执行的操作：终止、忽略、函数调用

SIGHUP is sent by the UART driver to the entire session when a hangup condition has been detected. Normally, this will kill all the processes. Some programs, such as nohup(1) and screen(1), detach from their session (and TTY), so that their child processes won't notice a hangup.  
当检测到挂断情况时，UART 驱动程序会向整个会话发送 SIGHUP 。通常情况下，这将终止所有进程。某些程序，例如 nohup(1) 和 screen(1) ，会从其会话（和 TTY）中分离，这样它们的子进程就不会注意到挂断。

### SIGINT 信号情报

- Default action: **Terminate**  
	默认操作： **终止**
- Possible actions: Terminate, Ignore, Function call  
	可执行的操作：终止、忽略、函数调用

SIGINT is sent by the TTY driver to the current foreground job when the *interactive attention* character (typically ^C, which has ASCII code 3) appears in the input stream, unless this behaviour has been turned off. Anybody with access permissions to the TTY device can change the interactive attention character and toggle this feature; additionally, the session manager keeps track of the TTY configuration of each job, and updates the TTY whenever there is a job switch.  
当 TTY 驱动程序向当前前台作业发送 SIGINT 时， *交互式注意* 字符（通常为 ^C ，ASCII 码为 3）会出现在输入流中，除非此功能已被关闭。任何拥有 TTY 设备访问权限的用户都可以更改交互式注意字符并切换此功能；此外，会话管理器会跟踪每个作业的 TTY 配置，并在作业切换时更新 TTY。

### SIGQUIT 退出信号

- Default action: **Core dump**  
	默认操作： **核心转储**
- Possible actions: Core dump, Ignore, Function call  
	可能的操作：核心转储、忽略、函数调用

SIGQUIT works just like SIGINT, but the quit character is typically ^\\ and the default action is different.  
SIGQUIT 的功能与 SIGINT 相同，但退出字符通常是 ^\\ 并且默认操作有所不同。

### SIGPIPE 信号管

- Default action: **Terminate**  
	默认操作： **终止**
- Possible actions: Terminate, Ignore, Function call  
	可执行的操作：终止、忽略、函数调用

The kernel sends SIGPIPE to any process which tries to write to a pipe with no readers. This is useful, because otherwise jobs like yes | head would never terminate.  
内核会向任何试图向管道写入数据的进程发送 SIGPIPE 。 没有读者。这很有用，因为否则像这样的工作就无法开展。 yes | head 永远不会终止。

### SIGCHLD 信号

- Default action: **Ignore**  
	默认操作： **忽略**
- Possible actions: Ignore, Function call  
	可执行的操作：忽略、函数调用

When a process dies or changes state (stop/continue), the kernel sends a SIGCHLD to its parent process. The SIGCHLD signal carries additional information, namely the process id, the user id, the exit status (or termination signal) of the terminated process and some execution time statistics. The session leader (shell) keeps track of its jobs using this signal.  
当一个进程终止或改变状态（停止/继续）时，内核会发送一个 SIGCHLD 信号会传递给其父进程。 SIGCHLD 信号携带额外信息，包括进程 ID、用户 ID、已终止进程的退出状态（或终止信号）以及一些执行时间统计信息。会话领导者（shell）使用此信号来跟踪其任务。

### SIGSTOP 信号停止

- Default action: **Suspend**  
	默认操作： **暂停**
- Possible actions: Suspend  
	可采取的措施：暂停

This signal will unconditionally suspend the recipient, i.e. its signal action can't be reconfigured. Please note, however, that SIGSTOP isn't sent by the kernel during job control. Instead, ^Z typically triggers a SIGTSTP, which can be intercepted by the application. The application may then e.g. move the cursor to the bottom of the screen or otherwise put the terminal in a known state, and subsequently put itself to sleep using SIGSTOP.  
此信号将无条件暂停接收者，即其信号操作无法重新配置。但请注意， SIGSTOP 在作业控制期间，内核不会发送此消息。相反， ^Z 通常会触发 SIGTSTP ，应用程序可以拦截该消息。然后，应用程序可以将光标移动到屏幕底部，或将终端置于某种已知状态，随后使用 SIGSTOP 使自身进入睡眠状态。

### SIGCONT 信号控制

- Default action: **Wake up**  
	默认操作： **唤醒**
- Possible actions: Wake up, Wake up + Function call  
	可能的操作：唤醒、唤醒 + 函数调用

SIGCONT will un-suspend a stopped process. It is sent explicitly by the shell when the user invokes the fg command. Since SIGSTOP can't be intercepted by an application, an unexpected SIGCONT signal might indicate that the process was suspended some time ago, and then un-suspended.  
SIGCONT 信号会恢复已停止的进程。当用户调用 fg 命令时，shell 会显式发送此信号。由于应用程序无法拦截 SIGSTOP 信号，因此意外的 SIGCONT 信号可能表明该进程之前曾被挂起，后来又被恢复。

### SIGTSTP

- Default action: **Suspend**  
	默认操作： **暂停**
- Possible actions: Suspend, Ignore, Function call  
	可执行的操作：暂停、忽略、函数调用

SIGTSTP works just like SIGINT and SIGQUIT, but the magic character is typically ^Z and the default action is to suspend the process.  
SIGTSTP 的作用与 SIGINT 和 SIGQUIT 相同，但神奇的字符通常是 ^Z ，默认操作是暂停进程。

### SIGTTIN 信号转导

- Default action: **Suspend**  
	默认操作： **暂停**
- Possible actions: Suspend, Ignore, Function call  
	可执行的操作：暂停、忽略、函数调用

If a process within a background job tries to read from a TTY device, the TTY sends a SIGTTIN signal to the entire job. This will normally suspend the job.  
如果后台作业中的某个进程尝试从 TTY 设备读取数据，TTY 会向整个作业发送 SIGTTIN 信号。这通常会导致作业暂停。

### SIGTTOU 信号灯

- Default action: **Suspend**  
	默认操作： **暂停**
- Possible actions: Suspend, Ignore, Function call  
	可执行的操作：暂停、忽略、函数调用

If a process within a background job tries to write to a TTY device, the TTY sends a SIGTTOU signal to the entire job. This will normally suspend the job. It is possible to turn off this feature on a per-TTY basis.  
如果后台作业中的某个进程尝试向 TTY 设备写入数据，TTY 会向整个作业发送 SIGTTOU 信号。这通常会导致作业暂停。可以针对每个 TTY 单独关闭此功能。

### SIGWINCH 西格温奇

- Default action: **Ignore**  
	默认操作： **忽略**
- Possible actions: Ignore, Function call  
	可执行的操作：忽略、函数调用

As mentioned, the TTY device keeps track of the terminal size, but this information needs to be updated manually. Whenever that happens, the TTY device sends SIGWINCH to the foreground job. Well-behaving interactive applications, such as editors, react upon this, fetch the new terminal size from the TTY device and redraw themselves accordingly.  
如前所述，TTY 设备会跟踪终端尺寸，但此信息需要手动更新。每当需要更新时，TTY 设备都会向前台作业发送 SIGWINCH 。行为良好的交互式应用程序（例如编辑器）会对此做出响应，从 TTY 设备获取新的终端尺寸并相应地重新绘制自身。

## An example 一个例子

Suppose that you are editing a file in your (terminal based) editor of choice. The cursor is somewhere in the middle of the screen, and the editor is busy executing some processor intensive task, such as a search and replace operation on a large file. Now you press ^Z. Since the line discipline has been configured to intercept this character (^Z is a single byte, with ASCII code 26), you don't have to wait for the editor to complete its task and start reading from the TTY device. Instead, the line discipline subsystem instantly sends SIGTSTP to the foreground process group. This process group contains the editor, as well as any child processes created by it.  
假设您正在使用您选择的（基于终端的）编辑器编辑文件。光标位于屏幕中央，编辑器正忙于执行一些占用大量处理器资源的任务，例如对一个大文件进行查找和替换操作。现在您按下 ^Z 。由于行规程已配置为拦截此字符（ ^Z 是一个字节，ASCII 码为 26），您无需等待编辑器完成其任务并开始从 TTY 设备读取数据。相反，行规程子系统会立即将 SIGTSTP 发送到前台进程组。该进程组包含编辑器及其创建的任何子进程。

The editor has installed a signal handler for SIGTSTP, so the kernel diverts the process into executing the signal handler code. This code moves the cursor to the last line on the screen, by writing the corresponding control sequences to the TTY device. Since the editor is still in the foreground, the control sequences are transmitted as requested. But then the editor sends a SIGSTOP to its own process group.  
编辑器已为 SIGTSTP 信号安装了处理程序，因此内核会将进程重定向到执行该信号处理程序代码。该代码通过向 TTY 设备写入相应的控制序列，将光标移动到屏幕上的最后一行。由于编辑器仍在前台运行，因此控制序列会按请求发送。但随后，编辑器会向其自身的进程组发送 SIGSTOP 信号。

The editor has now been stopped. This fact is reported to the session leader using a SIGCHLD signal, which includes the id of the suspended process. When all processes in the foreground job have been suspended, the session leader reads the current configuration from the TTY device, and stores it for later retrieval. The session leader goes on to install itself as the current foreground process group for the TTY using an ioctl call. Then, it prints something like "\[1\]+ Stopped" to inform the user that a job was just suspended.  
编辑器现已停止。此信息通过 SIGCHLD 信号报告给会话领导者，该信号包含已暂停进程的 ID。当前台作业中的所有进程都已暂停后，会话领导者会从 TTY 设备读取当前配置，并将其存储以便稍后检索。然后，会话领导者会使用 ioctl 调用将自身设置为 TTY 的当前前台进程组。最后，它会打印类似“\[1\]+ 已停止”的信息，以通知用户某个作业刚刚被暂停。

At this point, ps(1) will tell you that the editor process is in the stopped state (" T "). If we try to wake it up, either by using the bg built-in shell command, or by using kill(1) to send SIGCONT to the process(es), the editor will start executing its SIGCONT signal handler. This signal handler will probably attempt to redraw the editor GUI by writing to the TTY device. But since the editor is now a background job, the TTY device will not allow it. Instead, the TTY will send SIGTTOU to the editor, stopping it again. This fact will be communicated to the session leader using SIGCHLD, and the shell will once again write "\[1\]+ Stopped" to the terminal.  
此时， ps(1) 会告诉你编辑器进程处于停止状态（“ T ”）。如果我们尝试唤醒它，无论是使用 bg 使用内置 shell 命令，或者通过 kill(1) 向进程发送 SIGCONT ，编辑器将开始执行其 SIGCONT 信号处理程序。该信号处理程序可能会尝试通过写入 TTY 设备来重绘编辑器 GUI。但由于编辑器现在是后台任务，TTY 设备将不允许这样做。因此，TTY 将向编辑器发送 SIGTTOU ，使其再次停止。此信息将通过 SIGCHLD 传递给会话领导者，shell 将再次向终端写入“"\[1\]+ 已停止”。

When we type fg, however, the shell first restores the line discipline configuration that was saved earlier. It informs the TTY driver that the editor job should be treated as the foreground job from now on. And finally, it sends a SIGCONT signal to the process group. The editor process attempts to redraw its GUI, and this time it will not be interrupted by SIGTTOU since it is now a part of the foreground job.  
然而，当我们输入 fg 时，shell 首先会恢复之前保存的行规程配置。它会通知 TTY 驱动程序，从现在开始将编辑器作业视为前台作业。最后，它会向进程组发送 SIGCONT 信号。编辑器进程会尝试重新绘制其 GUI，这次不会再被 SIGTTOU 中断。 因为它现在是前台工作的一部分。

## Flow control and blocking I/O流量控制和阻塞 I/O

[![](http://www.linusakesson.net/pix/data/061001-1/300/300/dsc00043.jpg)](http://www.linusakesson.net/pix/data/061001-1/dsc00043.jpg)

Run yes in an xterm, and you will see a lot of " y " lines swooshing past your eyes. Naturally, the yes process is able to generate " y " lines much faster than the xterm application is able to parse them, update its frame buffer, communicate with the X server in order to scroll the window and so on. How is it possible for these programs to cooperate?  
在 xterm 中运行 yes ，你会看到很多“ y ”线条在你眼前飞驰而过。当然， yes 该过程能够比其他过程更快地生成“ y ”行 xterm 应用程序能够解析这些文件，更新其帧缓冲区，与 X 服务器通信以滚动窗口等等。这些程序是如何协同工作的？

The answer lies in *blocking I/O*. The pseudo terminal can only keep a certain amount of data inside its kernel buffer, and when that buffer is full and yes tries to call write(2), then write(2) will *block*, moving the yes process into the interruptible sleep state where it remains until the xterm process has had a chance to read off some of the buffered bytes.  
答案在于 *阻塞式 I/O* 。伪终端的内核缓冲区只能保存一定量的数据，当缓冲区满时，如果 yes 尝试调用 write(2) ，那么 write(2) 将会被阻塞。 *阻塞* ，将 yes 进程移入可中断睡眠状态，该状态将保持到 xterm 进程有机会读取一些缓冲字节为止。

The same thing happens if the TTY is connected to a serial port.yes would be able to transmit data at a much higher rate than, say, 9600 baud, but if the serial port is limited to that speed, the kernel buffer soon fills up and any subsequent write(2) calls block the process (or fail with the error code EAGAIN if the process has requested non-blocking I/O).  
如果 TTY 连接到串口，也会发生同样的情况。 yes 可以以比 9600 波特更高的速率传输数据，但如果串行端口的速度限制为该速率，内核缓冲区很快就会填满，任何后续的 write(2) 调用都会阻塞进程（如果进程请求非阻塞 I/O，则会失败并返回错误代码 EAGAIN ）。

What if I told you, that it is possible to explicitly put the TTY in a blocking state even though there is space left in the kernel buffer? That until further notice, every process trying to write(2) to the TTY automatically blocks. What would be the use of such a feature?  
如果我告诉你，即使内核缓冲区还有空间，也可以显式地将 TTY 置于阻塞状态呢？也就是说，在另行通知之前，所有尝试向 TTY 发送 write(2) 的进程都会自动阻塞。这样的功能有什么用呢？

Suppose we're talking to some old VT-100 hardware at 9600 baud. We just sent a complex control sequence asking the terminal to scroll the display. At this point, the terminal gets so bogged down with the scrolling operation, that it's unable to receive new data at the full rate of 9600 baud. Well, physically, the terminal UART still runs at 9600 baud, but there won't be enough buffer space in the terminal to keep a backlog of received characters. This is when it would be a good time to put the TTY in a blocking state. But how do we do that from the terminal?  
假设我们正在以 9600 波特率与一台老旧的 VT-100 硬件通信。我们刚刚发送了一个复杂的控制序列，要求终端滚动显示。此时，终端由于滚动操作而变得非常吃力，无法以 9600 波特率接收新数据。实际上，终端的 UART 端口仍然以 9600 波特率运行，但终端的缓冲区空间不足以容纳接收到的字符。这时，将 TTY 置于阻塞状态就显得尤为重要。但是，我们如何在终端上实现这一点呢？

We have already seen that a TTY device may be configured to give certain data bytes a special treatment. In the default configuration, for instance, a received ^C byte won't be handed off to the application through read(2), but will instead cause a SIGINT to be delivered to the foreground job. In a similar way, it is possible to configure the TTY to react on a *stop flow* byte and a *start flow* byte. These are typically ^S (ASCII code 19) and ^Q (ASCII code 17) respectively. Old hardware terminals transmit these bytes automatically, and expect the operating system to regulate its flow of data accordingly. This is called flow control, and it's the reason why your xterm sometimes appears to lock up when you accidentally press ^S.  
我们已经看到，TTY 设备可以配置为对某些数据字节进行特殊处理。例如，在默认配置中，接收到的 ^C 字节不会通过 TTY 传递给应用程序。 read(2) ，但会改为向前台作业发送 SIGINT 。类似地，也可以配置 TTY 以响应 *停止流* 字节和 *开始流* 字节。这些字节通常是 ^S （ASCII 码 19）和 ^Q （ASCII 码 17）。 旧式硬件终端分别传输这些字节 自动地，并期望操作系统来调节其数据流。 因此，这叫做流量控制，这也是为什么你的 xterm 有时在您意外按下时似乎会卡住 ^S.

There's an important difference here: Writing to a TTY which is stopped due to flow control, or due to lack of kernel buffer space, will *block* your process, whereas writing to a TTY from a background job will cause a SIGTTOU to suspend the entire process group. I don't know why the designers of UNIX had to go all the way to invent SIGTTOU and SIGTTIN instead of relying on blocking I/O, but my best guess is that the TTY driver, being in charge of job control, was designed to monitor and manipulate whole jobs; never the individual processes within them.  
这里有一个重要的区别：向因流量控制或内核缓冲区空间不足而停止的 TTY 写入数据将会 *阻塞* 你的操作。 进程，而从后台作业写入 TTY 则会导致 SIGTTOU 用于暂停整个进程组。我不明白 UNIX 的设计者为什么非要发明 SIGTTOU 呢？ SIGTTIN 而不是依赖阻塞式 I/O，但我最好的猜测是，TTY 驱动程序负责作业控制，其设计目的是监视和操作整个作业；而不是其中的单个进程。

## Configuring the TTY device配置 TTY 设备

![Control panel](http://www.linusakesson.net/programming/tty/cockpit.jpg)

To find out what the controlling TTY for your shell is called, you could refer to the ps l listing as described earlier, or you could simply run the tty(1) command.  
要找出控制 shell 的 TTY 的名称，您可以参考前面描述的 ps l 列表，或者您可以直接运行 tty(1) 命令。

A process may read or modify the configuration of an open TTY device using ioctl(2). The API is described in tty\_ioctl(4). Since it's part of the binary interface between Linux applications and the kernel, it will remain stable across Linux versions. However, the interface is non-portable, and applications should rather use the POSIX wrappers described in the termios(3) man page.  
进程可以使用 ioctl(2) 读取或修改已打开的 TTY 设备的配置。该 API 的描述见 tty\_ioctl(4) 。由于它是 Linux 应用程序和内核之间二进制接口的一部分，因此在不同的 Linux 版本中都能保持稳定。但是，该接口不具备可移植性，应用程序应该使用 termios(3) 手册页中描述的 POSIX 封装器。

I won't go into the details of the termios(3) interface, but if you're writing a C program and would like to intercept ^C before it becomes a SIGINT, disable line editing or character echoing, change the baud rate of a serial port, turn off flow control etc. then you will find what you need in the aforementioned man page.  
我不会详细介绍 termios(3) 接口，但是如果您正在编写 C 程序，并且想要在 ^C 变成 SIGINT 之前拦截它，禁用行编辑或字符回显，更改串口的波特率，关闭流控制等等，那么您可以在上述手册页中找到您需要的内容。

There is also a command line tool, called stty(1), to manipulate TTY devices. It uses the termios(3) API.  
此外，还有一个名为 stty(1) 的命令行工具，用于操作 TTY 设备。它使用 termios(3) API。

Let's try it!我们来试试吧！

$ stty -a  
speed 38400 baud; rows 73; columns 238; line = 0;  
intr = ^C; quit = ^\\; erase = ^?; kill = ^U; eof = ^D; eol = <undef>; eol2 = <undef>; swtch = <undef>; start = ^Q; stop = ^S; susp = ^Z; rprnt = ^R; werase = ^W; lnext = ^V; flush = ^O; min = 1; time = 0;  
\-parenb -parodd cs8 -hupcl -cstopb cread -clocal -crtscts  
\-ignbrk brkint ignpar -parmrk -inpck -istrip -inlcr -igncr icrnl ixon -ixoff -iuclc -ixany imaxbel -iutf8  
opost -olcuc -ocrnl onlcr -onocr -onlret -ofill -ofdel nl0 cr0 tab0 bs0 vt0 ff0  
isig icanon iexten echo echoe echok -echonl -noflsh -xcase -tostop -echoprt echoctl echoke  

The \-a flag tells stty to display **all** settings. By default, it will look at the TTY device attached to your shell, but you can specify another device with \-F.  
\-a 标志告诉 stty 显示 **所有** 设置。默认情况下，它会查找连接到 shell 的 TTY 设备，但您可以使用 \-F 指定其他设备。

Some of these settings refer to UART parameters, some affect the line discipline and some are for job control. *All mixed up in a bucket for monsieur.* Let's have a look at the first line:  
这些设置有些与 UART 参数有关，有些影响生产线规程，有些用于作业控制。 *全都混在一起，等着瞧吧。* 我们来看第一行：

| speed 速度 | UART | The baud rate. Ignored for pseudo terminals.   波特率。伪终端忽略此参数。 |
| --- | --- | --- |
| rows, columns 行、列 | TTY driver TTY 驱动程序 | Somebody's idea of the size, in characters, of the terminal attached to this TTY device. Basically, it's just a pair of variables within kernel space, that you may freely set and get. Setting them will cause the TTY driver to dispatch a SIGWINCH to the foreground job.   这是某人对连接到此 TTY 设备的终端大小（以字符为单位）的估计。本质上，它只是内核空间中的一对变量，您可以自由设置和获取它们。设置它们将导致 TTY 驱动程序向前台作业分派 SIGWINCH 。 |
| line 线 | Line discipline 直线纪律 | The line discipline attached to the TTY device. 0 is N\_TTY. All valid numbers are listed in /proc/tty/ldiscs. Unlisted numbers appear to be aliases for N\_TTY, but don't rely on it.   连接到 TTY 设备的线路规程。0 代表 N\_TTY 。所有有效号码都列在 /proc/tty/ldiscs 中。未列出的号码似乎是 N\_TTY 的别名，但不要依赖它。 |

Try the following: Start an xterm. Make a note of its TTY device (as reported by tty) and its size (as reported by stty -a). Start vim (or some other full-screen terminal application) in the xterm. The editor queries the TTY device for the current terminal size in order to fill the entire window. Now, from a different shell window, type:  
尝试以下步骤：启动 xterm 。记下它的 TTY 设备（由 tty 报告）及其大小（由 stty -a 报告）。在 vim （或其他全屏终端应用程序）中启动它。 xterm 编辑器会向 TTY 设备查询当前终端大小，以便填充整个窗口。现在，在另一个 shell 窗口中，输入：

```
stty -F X rows Y
```

where *X* is the TTY device, and *Y* is half the terminal height. This will update the TTY data structure in kernel memory, and send a SIGWINCH to the editor, which will promptly redraw itself using only the upper half of the available window area.  
其中 *X* 是 TTY 设备， *Y* 是终端高度的一半。这将更新内核内存中的 TTY 数据结构，并向编辑器发送 SIGWINCH ，编辑器会立即重新绘制自身，仅使用可用窗口区域的上半部分。

The second line of stty -a output lists all the special characters. Start a new xterm and try this:  
stty -a 输出的第二行列出了所有特殊字符。新建一个 xterm 并尝试以下操作：

```
stty intr o
```

Now " o ", rather than ^C, will send a SIGINT to the foreground job. Try starting something, such as cat, and verify that you can't kill it using ^C. Then, try typing " hello " into it.  
现在，输入“ o ”而不是“ ^C ”会将“ SIGINT ”发送到前台作业。尝试启动一些作业，例如“ cat ”，并验证是否无法使用“ ^C ”将其终止。然后，尝试在其中输入“ hello ”。

Occasionally, you may come across a UNIX system where the backspace key doesn't work. This happens when the terminal emulator transmits a backspace code (either ASCII 8 or ASCII 127) which doesn't match the erase setting in the TTY device. To remedy the problem, one usually types stty erase ^H (for ASCII 8) or stty erase ^? (for ASCII 127). But please remember that many terminal applications use readline, which puts the line discipline in raw mode. Those applications aren't affected.  
有时，您可能会遇到 UNIX 系统中退格键不起作用的情况。这是因为终端模拟器发送的退格代码（ASCII 8 或 ASCII 127）与 erase 不匹配。 在 TTY 设备中进行设置。要解决此问题，通常输入 stty erase ^H （ASCII 码 8）或 stty erase ^? （ASCII 码 127）。但请记住，许多终端应用程序使用 readline ，这会将行规程设置为原始模式。这些应用程序不受影响。

Finally, stty -a lists a bunch of switches. As expected, they are listed in no particular order. Some of them are UART-related, some affect the line discipline behaviour, some are for flow control and some are for job control. A dash (\-) indicates that the switch is off; otherwise it is on. All of the switches are explained in the stty(1) man page, so I'll just briefly mention a few:  
最后， stty -a 列出了一系列开关。不出所料，它们的排列顺序并不固定。其中一些与 UART 相关，一些影响线路规程行为，一些用于流量控制，还有一些用于作业控制。短横线 ( \- ) 表示开关关闭；否则表示开启。所有开关都在 stty(1) 手册页中有详细说明，因此我只简要介绍几个：

**icanon** toggles the canonical (line-based) mode. Try this in a new xterm:  
**icanon** 切换规范（基于行）模式。请在新的 xterm 中尝试以下操作：

```
stty -icanon; cat
```

Note how all the line editing characters, such as backspace and ^U, have stopped working. Also note that cat is receiving (and consequently outputting) one character at a time, rather than one line at a time.  
请注意，所有行编辑字符（例如退格键和 ^U ）都已停止工作。另请注意， cat 每次接收（并因此输出）一个字符，而不是一次一行。

**echo** enables character echoing, and is on by default. Re-enable canonical mode (stty icanon), and then try:  
**echo** 启用字符回显，默认开启。重新启用规范模式 ( stty icanon )，然后重试：

```
stty -echo; cat
```

As you type, your terminal emulator transmits information to the kernel. Usually, the kernel echoes the same information back to the terminal emulator, allowing you to see what you type. Without character echoing, you can't see what you type, but we're in cooked mode so the line editing facilities are still working. Once you press enter, the line discipline will transmit the edit buffer to cat, which will reveal what your wrote.  
当你输入时，终端模拟器会将信息发送到内核。通常情况下，内核会将相同的信息回显到终端模拟器，让你看到自己输入的内容。如果没有字符回显，你就看不到自己输入的内容，但我们目前处于“已完成”模式，所以行编辑功能仍然有效。按下回车键后，行规则会将编辑缓冲区的内容发送到 cat ，从而显示你输入的内容。

**tostop** controls whether background jobs are allowed to write to the terminal. First try this:  
**tostop** 控制后台作业是否允许写入终端。首先尝试以下操作：

```
stty tostop; (sleep 5; echo hello, world) &
```

The & causes the command to run as a background job. After five seconds, the job will attempt to write to the TTY. The TTY driver will suspend it using SIGTTOU, and your shell will probably report this fact, either immediately, or when it's about to issue a new prompt to you. Now kill the background job, and try the following instead:  
& 会使命令作为后台任务运行。五秒后，该任务会尝试写入 TTY。TTY 驱动程序会使用 SIGTTOU 将其挂起，你的 shell 可能会立即报告此情况，或者在即将向你发出新提示符时报告。现在终止后台任务，然后尝试以下命令：

```
stty -tostop; (sleep 5; echo hello, world) &
```

You will get your prompt back, but after five seconds, the background job transmits hello, world to the terminal, in the middle of whatever you were typing.  
你会收到提示符，但五秒钟后，后台作业会向终端发送 hello, world ，而此时你正在输入任何内容。

Finally, stty sane will restore your TTY device configuration to something reasonable.  
最后， stty sane 会将您的 TTY 设备配置恢复到合理的状态。

## Conclusion 结论

I hope this article has provided you with enough information to get to terms with TTY drivers and line disciplines, and how they are related to terminals, line editing and job control. Further details can be found in the various man pages I've mentioned, as well as in the glibc manual (info libc, "Job Control").  
我希望本文能为您提供足够的信息，帮助您理解 TTY 驱动程序和线路规则，以及它们与终端、线路编辑和作业控制之间的关系。更多详细信息，请参阅我提到的各个手册页以及 glibc 手册（ info libc ，“作业控制”）。

Finally, while I don't have enough time to answer all the questions I get, I do welcome feedback on this and other pages on the site. Thanks for reading!  
最后，虽然我没有足够的时间回答所有问题，但我非常欢迎大家对本页面以及网站上的其他页面提出反馈意见。感谢阅读！

Posted Friday 25-Jul-2008 17:46  
发布于 2008 年 7 月 25 日星期五 17:46

### Discuss this page 讨论此页面

Anonymous 匿名的  
Sun 24-Aug-2008 21:36

Very good and informative article for a complex topic  
2008年8月24日星期日 21:36 这是一篇非常好的文章，内容翔实，主题也很复杂。  
\- the tty system really gets demystified here.  
\- 在这里，tty 系统得到了真正的揭秘。  
  
Only a small correction:只需稍作更正：  
Your statement "icanon switches between raw and cooked mode" is not completely true.  
你所说的“icanon 会在生熟模式之间切换”并不完全正确。  
  
'stty -icanon' still interprets control characters such as Ctrl-C whereas 'stty raw' disables even this and is the real raw mode.  
'stty -icanon' 仍然会解释 Ctrl-C 等控制字符，而 'stty raw' 甚至禁用了此功能，是真正的原始模式。  
  
Greetings,问候，  
\-Andreas.\-安德烈亚斯。

Anonymous 匿名的  
Thu 10-Jul-2025 13:26 2025年7月10日星期四 下午1:26

**marky** wrote:**marky** 写道：

Sadly, this nice property seems to break over SSH, as I recently lamented about at stack overflow, here:  
遗憾的是，这个不错的特性似乎在 SSH 连接下会失效，正如我最近在 Stack Overflow 上抱怨的那样，链接如下：  
  
https://stackoverflow.com/questions/78843587/how-to-run-ssh-in-the-background-without-writing-my-own-os-kernel-and-ssh-server  

  
Sadly, the internet is so broken there's no good place for you to post things that doesn't get deleted. Even eternal-september is removing knowledge at an astonishing rate.  
令人遗憾的是，互联网如今已千疮百孔，你找不到一个可以放心发布内容而不被删除的地方。就连“永恒九月”（Eternal September）这样的网站也在以惊人的速度删除知识。

Anonymous 匿名的  
Thu 10-Jul-2025 13:55 2025年7月10日星期四 13:55

**marky** wrote:**marky** 写道：

Sadly, this nice property seems to break over SSH, as I recently lamented about at stack overflow, here:  
遗憾的是，这个不错的特性似乎在 SSH 连接下会失效，正如我最近在 Stack Overflow 上抱怨的那样，链接如下：  
  
\[ https://web.archive.org/web/20250126093803/https://stackoverflow.com/questions/78843587/how-to-run-ssh-in-the-background-without-writing-my-own-os-kernel-and-ssh-server \]  
  
To fix this issue, I think we'd need new kernel APIs and a change to the SSH protocol  
要解决这个问题，我认为我们需要新的内核 API 和对 SSH 协议的修改。

  
What's the problem? That ssh doesn't pass on job control responsibilities to the other end? You need to run something of this structure in lieu of something more transparent?  
问题是什么？是 SSH 没有将作业控制职责传递给另一端吗？你需要运行类似这样的架构来代替更透明的方案吗？  
  
myend -- ssh args... 'yourend -- cmd args...'  
我的终端 -- ssh 参数... '你的终端 -- cmd 参数...'  
  
tty muxing and relaying looks impossible to do exactly right without a new line discipline or two so terminal state changes can be relayed and data that varies with state can be conditionally delayed until states ar esynchronised.  
如果没有一两个新的线路规则，tty 复用和中继似乎不可能完全正确，这样终端状态的变化就可以中继，并且随着状态变化的数据可以有条件地延迟，直到状态同步。  
  
It kinda looks like new line discipline(s) are the place to do it.  
看起来，新的生产线学科是开展这项工作的最佳场所。  
It looks like, despite comments around the internet of a mythical RAW line discipline, Linux offers only N\_TTY and N\_NONE, neither of which looks suitable as a basis for tty relaying.  
尽管互联网上流传着关于神话般的 RAW 线路规则的评论，但 Linux 似乎只提供了 N\_TTY 和 N\_NONE，而这两者都不太适合作为 tty 中继的基础。  
  
I can't bear to imagine the hurdles tmux must go through to do the right thing. I can only imagine they give up on terminals that show the termios flags to the user.  
我简直无法想象 tmux 为了做正确的事情要克服多少困难。我只能猜测他们最终放弃了向用户显示 termios 标志的终端。  
  
The real tty needs to be given the flags of the pty and vice-versa, whenever those change at either end, but features of the line discipline need to be "secretly" off via the pty master rather than being switched off for relaying in the slave pty or real tty termios, or by trying to convert streams in between. terminal types need to be generalised to intersections of types and applications need to advise what types from the terminfo database they support for inclusion in the intersection so applications can adjust themselves to suit the relay pipeline even when its just one real and one pseudo.  
当任何一端的标志发生变化时，真实终端（tty）需要获得伪终端（pty）的标志，反之亦然。但是，线路规程的某些特性需要通过伪终端主控端“秘密”关闭，而不是在从属伪终端或真实终端终端（termios）中进行中继时关闭，或者尝试在两者之间转换数据流。终端类型需要泛化为类型的交集，应用程序需要告知其支持 terminfo 数据库中哪些类型可以包含在交集内，以便应用程序能够调整自身以适应中继管道，即使只有一个真实终端和一个伪终端。

Anonymous 匿名的  
Fri 11-Jul-2025 00:48 2025年7月11日星期五 00:48

  
I had relied on the list in /proc/tty/ldiscs which I found referenced as a list of available line disciplines. I now think that's populated from loaded kernel modules (and built in ones if nonmodular kernels still exist) but no N\_RAW that I can see in /usr/include/linux/tty.h  
我之前依赖于 /proc/tty/ldiscs 中的列表，该列表被引用为可用线路规程的列表。我现在认为该列表是由已加载的内核模块（以及如果仍然存在非模块化内核，则包括内置模块）填充的，但我没有在 /usr/include/linux/tty.h 中找到 N\_RAW。  
  

0-1999:linux# cat /proc/tty/ldiscs  
n\_tty 0  
n\_null 27  
0-2000:linux# modprobe slip  
0-2001:linux# cat /proc/tty/ldiscs  
n\_tty 0  
slip 1 滑倒 1  
n\_null 27  
0-2002:linux# rmmod slip  
0-2003:linux# cat /proc/tty/ldiscs  
n\_tty 0  
n\_null 27

Anonymous 匿名的  
Fri 11-Jul-2025 01:30

There are various ioctls for ttys in several layers, at least:  
2025 年 7 月 11 日星期五 01:30 至少在多个层级中，tty 有多种 ioctl 指令：  
  
tty layer tty 层  
tty devices low-level driver  
tty 设备底层驱动程序  
line discipline 直线纪律  
  
man tty\_ioctl has some information about some of them.  
man tty\_ioctl 包含一些关于它们的信息。  
  
There seem to be some synchronisation, buffered char counts and fake input methods that might make an approximation of transparent relaying practical, including even synchronisation of streams with termios changes, perhaps tmux, screen and sudo use them.  
似乎有一些同步、缓冲字符计数和伪输入方法，可以实现透明中继的近似值，甚至包括流与 termios 更改的同步，也许 tmux、screen 和 sudo 会使用它们。  
  
For your ssh solution see how well sudo does it using its 'monitor'. see man sudo for an outline.  
对于你的 SSH 解决方案，可以参考 sudo 的“monitor”功能，看看它的表现如何。详情请参阅 sudo 的手册页。