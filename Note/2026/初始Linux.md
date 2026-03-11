[跳转至](https://101.lug.ustc.edu.cn/Ch01/#linux)

## 初识 Linux

本文已完稿并通过审阅，是正式版本。

导言

21 世纪是计算机科学的世纪。在信息化程度日增月益的现代社会，与计算机和各类电子产品打交道已经成为我们，尤其是年轻人的日常生活中几乎不可避免的事情了。据统计，截至 2025 年 6 月，中国的网民规模达 11.23 亿人 [^1] ，即比例已经超过七成，而其中以中青年为主。在你的生活中，你认为计算机又占据了多大的席位呢？事实上，计算机在你生活中的比重可能远超出你的想象：不仅包括我们熟悉的在日常生活中频繁使用的个人计算机（俗称“电脑”），诸如智能手机操作系统、车载定位导航系统、校内一卡通服务系统以及如今风靡中国的电子支付网络等等都十分倚重各式各样的计算机。这些隐藏在各类用途迥异的设备中、甚至是无形的网络后面的计算机又会是什么模样？

在本书的第一章，我们将带领你简单了解现代计算机和计算机系统的发展，并正式引入本书的核心介绍对象，即在个人计算机系统中虽然不甚流行，你可能也少有耳闻，但在科学研究、工业生产、计算机网络等各种专业场合中占据绝对主导的 Linux 操作系统。本章还会进一步引领你一步步了解我们身边的 Linux 系统，认识到其实它并不遥远缥缈也绝非高不可攀。最后，我们还会把它带到你的眼前，让你亲自上手感受它的魅力。

## 计算机与操作系统

### 计算机的更新换代

自 1946 年第一台通用计算机埃尼阿克（全称“电子数值积分计算机”，英文简称 ENIAC）问世以来，人类文明就朝向信息化大步迈进。在接下来的几十年，计算机经历了真空管时代（第一代，ENIAC 就是真空管计算机）、晶体管时代（第二代，如贝尔实验室的世界上第一台全晶体管计算机 TRADIC）、集成电路时代（第三代，如 IBM System/360 系列）和如今的大规模集成电路时代（第四代，如世界上第一款微处理器 Intel 4004）。在更新换代中，计算机的性能和集成度都有着飞跃般的提升，在过去几十年的表现呈指数级增长，因而就有了计算机行业内耳熟能详的“摩尔定律”（Moore's Law），即 **集成电路上可容纳的晶体管数目每两年就会翻一倍** ，这条定律描述了近几十年来计算机性能爆发增长的现象。

摩尔定律

对于摩尔定律或许你会更熟悉这种说法： **计算机的性能每 18 个月提高一倍** ，但事实上这句话来自英特尔首席执行官大卫·豪斯（David House）而不是摩尔。不过有一点可以肯定的是，这两句话都预测计算机的性能将随着时间产生指数爆炸级别的增长，而这在过去几十年间确实实现了。

不过，由于晶体管的密度会受到量子物理理论上的限制，以及 CPU 会受到功耗和散热的限制，事实上这个定律已经开始失效了，计算机性能的提升开始放缓。为了不受制于这些限制，人们从最初追求单个 CPU 性能的提升逐渐转向了多个 CPU 之间的联合协作，因而基于多核的开发成为了未来计算机领域开发人员的一个不可绕过的话题。

### 计算机操作系统

如果现在提起计算机操作系统，可能多数人的第一反应就是大名鼎鼎的 Windows，此外有些人可能也接触过 macOS 或者 Linux 的各类发行版（如：Ubuntu, Fedora, Manjaro, CentOS 等），它们都是计算机操作系统。然而计算机最初并没有操作系统。在当时，许多计算机不是通用计算机，它们造出来就是为了某个特定目的而服务的，因此其架构只需要为这个目的而设计即可，无需包括完整的操作系统。另外一个原因是在晶体管时代之前，计算机体积庞大，而性能又十分有限，因此也没有能力承载通用的操作系统。随着计算机性能的提升，人们更加依赖计算机的能力，对计算机的功能要求也日渐复杂。为了能尽可能利用计算机的自动化这一特性，一些操作系统开始成型。在成型的初期，计算机操作系统的目的是为了帮助用户进行批处理操作，不过之后它们也慢慢有了新的功能：进程管理、任务调度、控制输入输出设备等。这样的操作系统逐渐形成了庞大的体系，成为了联络一般用户和计算机底层设备的中介，让用户无需关心绝大多数的底层设备，大大降低了用户的使用学习成本。

### 现代操作系统的功能 \*

现代的计算机操作系统的功能已经十分复杂，远非当初所能比，且不同的操作系统可能在各方面都有着差异。但总体来说，其一直是用户与底层硬件交流的桥梁。用户可以通过操作系统的用户界面向计算机发出命令，操作系统则对输入的命令进行解释并驱动相关的设备来实现用户的要求。

现代个人计算机操作系统典型功能

通常来说，一个现代个人计算机操作系统会包含以下的功能 [^2] ：

- 进程管理：操作系统之上运行的各类程序都以进程的形式存在（有关进程的内容将在本书 [第四章](https://101.lug.ustc.edu.cn/Ch04/) 中展开），而通常计算机的中央处理器只有几个。为了能让许多进程并发执行，需要操作系统进行调度。
- 内存管理：内存是操作系统和进程用来临时存储数据的介质。计算机的内存是有限的，而且通常还是多层次的，因此操作系统需要合理分配和回收内存。
- 文件系统：为了管理计算机上的文件和数据，操作系统需要建立一个合适的数据结构来存储它们，即文件系统。
- 网络通信：为了能和互联网上的其它计算机进行有效的联络，一个公认的通信协议（如当今互联网主流的 TCP/IP）是必要的。操作系统需要有能力实现各种必需的网络通信方式。
- 安全机制：很多个人计算机和商业服务器上的数据都很敏感，因此操作系统必须配备一个安全机制用于保护数据不被未授权的人士获取，以及保护计算机免于各类计算机病毒的攻击。
- 用户界面：现代的个人计算机操作系统通常都会包含一个图形化的用户界面，从而方便用户与计算机打交道，并且提升用户体验。
- 驱动程序：驱动程序是直接与硬件交互的软件，使用驱动程序才能利用好计算机的硬件，因此操作系统要有能力与驱动程序对接以发挥硬件的功能。

不同的操作系统通常会基于不同设计思路，面向不同的用户群体，因此从用户的使用感受来说往往大相径庭。然而由于现代个人计算机操作系统的功能高度相似，因此它们在不同的外表下存在着诸多共通的属性。只要进行一些调研，我们就能发现它们实际上殊途同归。

## 什么是 Linux？

### Linux 的起源

1969 年，美国 AT&T 公司的贝尔实验室开发了 UNIX 操作系统，并在此后的 10 年里在学术机构和大型企业中得到了广泛的应用。在这段时间，许多计算机从业者开发了很多基于 UNIX 的变种，统称为“类 UNIX 操作系统”。最初 AT&T 公司将 UNIX 的源码以低价甚至免费的许可授权给学术机构做研究和教学之用，然而后来它开始意识到了其商业价值，改变了之前的策略，取消了授权并对代码进行闭源，并对之前在 UNIX 之上研究出来的各类衍生组件和变种系统全部声明了著作权，随后开始了一场旷日持久的诉讼。虽然 UNIX 在此前 10 年在学界和业界起着十分重要的作用，但 AT&T 公司的这种行为对诸多使用 UNIX 和其变种的学术机构和商业厂家造成了巨大的负面影响，许多曾经的用户对 AT&T 公司的行径十分不满。

1983 年 9 月 27 日，理查德·斯托曼（Richard Stallman）在麻省理工学院发起了 GNU 计划，它的目标是创建一套类似 UNIX 但完全自由的操作系统，因此这套系统不会包括任何 UNIX 的代码。在这个计划中诞生了之后十分有名的“GNU 通用公共许可证”（英文简称 GPL），这份许可证把使用该许可的软件的所有权利授予任何使用它的人。这种授权方式与通常的版权授权方式相左，它十分慷概地让出了几乎所有权利，让基于它的软件成为了自由且开源的软件，因此这种权利又被称为著作传（相对于通常的“著作权”）。

1991 年，正在大学内进修的林纳斯·托瓦兹（Linus Torvalds）对他使用的一个类 UNIX 操作系统 MINIX 十分不满，因为当时 MINIX 仅可用于教育但不允许任何商业用途。于是他在他的大学时期编写并发布了自己的操作系统，也就是后来所谓的 “Linux 内核”，成为了如今各类 Linux 发行版的基础。

Linux 内核并不是一个完整的操作系统，因为它过于精简，单单从它的功能上来说就已经不符合通常的现代的操作系统的定义了。为了能让这个内核拥有更多功能、完善的用户界面和更佳的使用体验，许多自由软件社区的开发人员和一些计算机商业公司便开始把各种组件添加到这个内核之上，这才构建成了一个完整的 Linux 操作系统。因为 Linux 内核是一个开源软件，所以通过这种方式组合出来的 Linux 操作系统会有许许多多的形式，不像 Windows 或者 macOS 这种受到公司统一规定的商业操作系统。正是因为开源社区的诸多成员以及许多商业公司的去中心化的贡献，让 Linux 充满了多样性。因为这种独特的属性，或许我们可以说 Linux 操作系统从来都不是指哪一种操作系统。取而代之地，为了指代某一个基于 Linux 内核构造出来的操作系统，我们通常都将其称之为“Linux 发行版”。

GNU/Linux

GNU 计划最初是为了对抗 UNIX 而建立的，这可以从 GNU 的全称 “GNU's Not UNIX”（GNU 不是 UNIX）中十分直观地看出来。GNU 计划的创始人理查德·斯托曼希望通过这个计划开发一个自由的操作系统 GNU，他将 GNU 操作系统视作“达成社会目的的技术方法”。

虽然 GNU 计划产生出了许多自由开源的组件和软件，但其核心的 GNU 操作系统却至今没有开发完成。在实际操作中，GNU 计划的组件通常都会依赖 Linux 内核作为系统核心来承载它们，它们在一起合称 GNU/Linux。在这里，Linux 内核是功能核心，而 GNU 组件则是这块核心的外设，也是用户操作和使用 Linux 内核的工具。众多当今通用计算机和服务器上主流的 Linux 发行版都属于 GNU/Linux。

如今智能手机上一个常见的系统是谷歌公司开发的 Android，它其实也是一个基于 Linux 内核开发的操作系统。不过它没有采用 GNU 组件作为工具，而是谷歌自行研发的另一套体系。基于这套体系构成的组合则被称为 Android/Linux，它和我们接下来讨论的 GNU/Linux 大相径庭，感兴趣的读者可以参考本章的拓展阅读： [Android/Linux](https://101.lug.ustc.edu.cn/Ch01/supplement/#android-linux) 。

GNU 自由软件

进入 GNU/Linux 世界，便意味着与 GNU 自由软件打交道。先看看一堆字母 g 开头的应用程序：

- GCC: GNU 的 C 和 C++ 编译器
- GDB: GNU 程序调试器
- Gzip: gz 格式压缩与解压缩工具
- GIMP: GNU 图像编辑工具

它们的首字母 g 都是 GNU 的缩写（当然不是所有以 g 开头的都是 GNU 软件）。许多 Linux 上的系统管理命令虽然未必以 g 开头，但都属于自由软件；还有 [更多优秀的软件](https://www.gnu.org/software/) ，被自由软件爱好者维护、分享……选择 Linux，很大程度上是一种对极客精神与开源文化的认同。

### Linux 发行版

一个典型的 Linux 发行版除了 Linux 内核以外，通常还会包括一系列 GNU 工具和库、一些附带的软件、说明文档、一个桌面系统、一个窗口管理器和一个桌面环境。不同的发行版之间除了 Linux 内核以外的其它部分都有可能不一样，因此有的时候我们对比某两种发行版的时候会觉得它们看起来像是完全不一样的操作系统，然而实质上它们却拥有着相同的核心，即 Linux 内核。

这里给读者介绍若干桌面和服务器环境中主流的发行版分支：

#### Debian 分支

Debian 是一个完全由自由软件构成的类 UNIX 操作系统，第一个版本发布于 1993 年 9 月 15 日，迄今仍在维护，是最早的发行版之一。其以坚持自由软件精神和生态环境优良而出名，拥有庞大的用户群体，甚至自己也成为了一个主流的子框架，称为“Debian GNU/Linux”。

![Debian](https://101.lug.ustc.edu.cn/Ch01/images/Debian-Logo.png)

Debian 图标

Debian GNU/Linux 也派生了很多发行版，其中最为著名的便是 Ubuntu（官方译名“友邦拓”）。Ubuntu 由英国的 Canonical 公司主导创立，是一个主打桌面应用的操作系统。其为一般用户提供了一个时新且稳定的由自由软件构成的操作系统，且拥有庞大的社群力量和资源，十分适合普通用户使用。

![Ubuntu](https://101.lug.ustc.edu.cn/Ch01/images/Ubuntu-Logo.png)

Ubuntu 图标

#### Red Hat 分支

Red Hat Linux 是美国的 Red Hat 公司发行的一个发行版，第一个版本发布于 1994 年 11 月 3 日，也是一个历史悠久的发行版。它曾经也广为使用，但在 2003 年 Red Hat 公司停止了对它的维护，转而将精力都投身于其企业版 Red Hat Enterprise Linux（简称 RHEL）上，Red Hat Linux 自此完结，而商业市场导向的 RHEL 维护至今。

![Red Hat](https://101.lug.ustc.edu.cn/Ch01/images/Red-Hat-Logo.png)

Red Hat 公司商标，RHEL 是其旗下产品

在 Red Hat Linux 在停止官方更新后，由社群启动的 Fedora 项目接管了其源代码并构筑了自己的更新，演变成了如今的 Fedora 发行版。Fedora 是一套功能完备且更新迅速的系统，且本身计划也受到了 Red Hat 公司的赞助，成为了公司测试新技术的平台。

![Fedora](https://101.lug.ustc.edu.cn/Ch01/images/Fedora-Logo.png)

Fedora 图标

虽然 RHEL 是一个收费的、商业化的系统，但是其遵循 GNU 通用公共许可证，因此会开放源代码。编译这些源代码可以重新得到一个可以使用的操作系统，即一个新的发行版：CentOS（Community Enterprise Operating System，社区版企业操作系统）。因为 CentOS 几乎完全编译自 RHEL 的代码，所以其也像 RHEL 一样具有企业级别的稳定性，适合在要求高度稳定的服务器上运行。

2020 年 12 月，CentOS 社区在其博客中 [宣布未来的重点转向 CentOS Stream](https://www.redhat.com/en/blog/centos-stream-building-innovative-future-enterprise-linux) ，这是一个全新的滚动发行版。在此之前，RHEL 的上游为 Fedora，而 CentOS 的上游为 RHEL；在推出 CentOS Stream 之后，它就成为了 RHEL 的上游发行版。与此同时，CentOS 8 的支持期限被缩短至 2021 年底，且不再推出新的非 Stream 的 CentOS 版本。不满于该决定的人们也组织了新的社区，推出了诸如 [AlmaLinux](https://almalinux.org/) 、 [Rocky Linux](https://rockylinux.org/) 等发行版。

![CentOS](https://101.lug.ustc.edu.cn/Ch01/images/CentOS-Logo.png)

CentOS 图标

#### Arch Linux 分支

Arch Linux 是一个基于 x86-64 架构的 Linux 发行版，不过因为其内核默认就包含了部分非自由的模块，所以其未受到 GNU 计划的官方支持。即便如此，Arch Linux 也因其“简单、现代、实在、人本、万能”的宗旨赢得了 Linux 中坚用户的广泛青睐。不过，Arch Linux 对这个宗旨的定义和其它发行版有所区别。通常的操作系统为了方便用户快速上手，都是尽可能隐藏底层细节，从而避免用户了解操作系统的运行知识即可直接使用。但是 Arch Linux 则是重在构建优雅、极简的代码结构，这方便了使用者去理解系统，但不可避免地要求使用者自身愿意去了解操作系统的运作方式。某种程度上说，它的“简单”和“人本”注重的是方便用户通过了解而去最大化地利用它，而不是采取屏蔽工作原理的方式来降低使用门槛。因此，本书不建议初学者直接上手 Arch Linux，但十分推荐在读者对 Linux 有进一步了解之后去探索它。

![Arch Linux](https://101.lug.ustc.edu.cn/Ch01/images/Arch-Linux-Logo.png)

Arch Linux 图标

Arch Linux 拥有强大的功能，但因其特殊的理念使得用户不易使用。为了能让一般用户也能用上 Arch Linux 的强大功能，它的变种 Manjaro 发行版于 2011 年问世。Manjaro 发行版基于 Arch Linux，但更注重易用，因而更适合一般用户。

![Manjaro](https://101.lug.ustc.edu.cn/Ch01/images/Manjaro-Logo.png)

Manjaro 图标

以上是若干个常见的 Linux 发行版系列，其他的常用发行版有 openSUSE、Gentoo 等，相关介绍可参考 [附录中对应的资料](https://101.lug.ustc.edu.cn/Appendix/distribution/) 。

由上文可见，Linux 的发行版非常丰富，不同的发行版有其各自的特性，因而可以面向不同的用户满足独特的需求。对于新手来说，一个拥有丰富的图形界面的发行版更加适合初步探索和后续使用。 **本书推荐初次接触 Linux 的读者优先采用 Ubuntu 发行版或者它的子发行版（Lubuntu, Xubuntu 等）** 作为自己接触和探索 Linux 的平台，在以后可以自行上手其它发行版。

Linux 总结

这一章或许对于一些读者来说不太容易一次读懂，因为不同于 Windows 或者 macOS 这种受到一家商业公司完全控制和规划的系统那样有着比较单一和线性的发展轨迹，Linux 其独特的自由、开源的特性注定了它的发展进程必定是一个去中心化的、非线性的形式。因此，Linux 的历史虽然只有短短三十年，却充满着复杂的脉络和丰富的细节。但是正是因为 Linux 在如此繁茂的分枝之上结出诸多硕果，我们才能从某种角度感受到开源社区文化的强大活力，反过来也正是这种活力才能让 Linux 有着与其它闭源商业操作系统不一样的叙事。

回到本章的标题：什么是 Linux？这个问题在不同的语境下有不同的答案：它可以指代 Linux 内核，也可能指代一个或者多个 Linux 发行版。在日常领域或是作为新手接触到的情境来看，这个词通常都是指代后者，而且往往指的是 GNU/Linux 的发行版。

## 我们身边的 Linux

虽然在个人电脑上不太常见，但 Linux 的各类发行版其实早已深入我们的日常生活。下面是几个例子：

### 智能手机

智能手机目前有两个主流的操作系统：苹果公司研发的 iOS 操作系统和谷歌公司研发的 Android 操作系统，而 Android 正是 Linux 的一个知名的发行版。与通常安装在通用计算机上的 GNU/Linux 分支不同，Android 属于 Android/Linux 分支，这个分支通常活跃在智能手机和嵌入式设备的舞台上。

由谷歌公司推出的 Android 叫做 Android 原生系统，而基于该原生系统诞生出来的各类独特的操作系统就是 Android/Linux 系下的子发行版。Android/Linux 下的子发行版很多，如华为公司的 EMUI 操作系统和小米公司的 MIUI 操作系统等。

![Android](https://101.lug.ustc.edu.cn/Ch01/images/Android-10-Native.png)

Android 10 原生界面

### 服务器

现代人的生活已经很难离开互联网了，在互联网上，我们可以访问各式各样的网站、利用在线社交平台分享自己的生活、或者是使用联机办公工具和同事协同工作。通常来说这些网站和软件的提供商都需要设立他们自己的计算机来完成计算、存储和通信的功能，这种计算机就被称为服务器。和个人计算机不同，服务器通常都不会使用 Windows 或者 macOS 这种个人计算机操作系统，事实上绝大部分的服务器维护人员都愿意选择一些 Linux 发行版作为它们的操作系统，因为许多 Linux 发行版界面简洁，功能强大，而且某些发行版也是受到专业计算机企业的服务支持的（如前文提到的 RHEL）。

同时，受惠于互联网上丰富的教程，Debian 和 Ubuntu Server 也成为越来越多个人和团体用作服务器操作系统的 Linux 发行版，如下文提到的中科大开源社群 LUG@USTC 使用 Debian 发行版及其衍生产品 Proxmox VE 作为其所有服务器的操作系统。

另一类有名的服务器操作系统是微软公司的 Windows Server 系列，不过其流行程度比不上各类 Linux 发行版。

![Windows Server](https://101.lug.ustc.edu.cn/Ch01/images/Windows-Server.png)

Windows Server 图标

### 电视机顶盒

比起十几年前采用传统线路的电视，现在国内很多家庭里的电视都换成了智能数字电视，这些电视通常会配备一个机顶盒来控制电视播放的内容。实际上，电视机顶盒就是一个嵌入式设备，而 Android/Linux 分支下的各类发行版正是主流的嵌入式操作系统，如谷歌公司为数字电视专门推出的 Android TV 操作系统。

![Android TV](https://101.lug.ustc.edu.cn/Ch01/images/Android-TV.png)

Android TV 图标

## 让自己的计算机用上 Linux

有很多尚未接触过 Linux 的读者看到这里可能已经在期待或者计划让自己尽快开始使用 Linux 了。事实上，如果把 Linux 看作一个领域，那它的确是一个重视实践的领域。而且出于学习目的，在阅读本书未来的章节时在手头准备一个随时可用的 Linux 发行版是十分关键和有益的。因此，本书 **强烈建议各位读者在本机安装一个属于自己的 Linux 发行版** ，以供随时实践。

在本机上安装一个 Linux 发行版有很多种选择，如：安装方法可以选择实机安装或虚拟机安装；发行版则可以在诸多选项中任意抉择。然而，对于新手来说，本书 **不建议直接采用实机安装 Linux** ，因为这样做会面临以下问题：

- 在安装过程中不理解关键的选项（如：磁盘分区、挂载、交换空间分配等）的意义，很容易做出错误的决定；
- 错误的配置可能导致自己原先本机上的操作系统和数据遭到不可逆转的损坏；
- 部分硬件可能对安装的发行版缺少兼容，从而导致意外安装失败。
- 如果安装的过程中选择下载附加工具，可能会因为默认镜像在国外而导致下载十分缓慢，从而让安装流程变得很漫长。

鉴于以上问题对于新手来说十分常见，本书的编写组为各位读者专门提供了另外一种更为安全高效的方法：在虚拟机上运行 Linux 发行版镜像。虚拟机简单来说可以视作一个安全可靠的沙盒，它受到虚拟机管理软件的管理，而管理软件是直接安装在自己目前常用的操作系统上的。本书 **推荐使用虚拟机运行安装完毕的 Linux 镜像** ，因为这样会有如下优点：

- 读者仍然可以安心地使用自己当前的操作系统，因为虚拟机不干涉当前电脑操作系统的配置。
- 无需考虑底层硬件的兼容性问题，稳定性大幅提升。
- 系统已经安装完毕，使用虚拟机打开时相当于直接开机，无需经历安装流程。
- 如果在虚拟机中发生任何错误，可以通过重置、回溯虚拟机镜像的方法无痛修复，而不会伤害到读者计算机上的操作系统和数据。

因此，本书将主要讲解如何为自己搭建一个安全高效的 Linux 虚拟机。如果你有一台远程的 Linux 服务器，可以参考 [拓展阅读](https://101.lug.ustc.edu.cn/Ch01/supplement/#ssh) 的内容配置 SSH 连接。

WSL

如今，对于 Windows 用户来说，使用 WSL 安装 Linux 或许会是更加便捷的方法，详情可以参考 [附录](https://101.lug.ustc.edu.cn/Appendix/wsl/) 。

### 获取虚拟机管理软件

现在在 Windows / macOS 上主流的虚拟机管理软件有：

- [VMware Workstation Pro](https://support.broadcom.com/group/ecx/productdownloads?subfamily=VMware+Workstation+Pro) 是 VMware 公司（现已被博通收购）推出的一款 Windows 上的虚拟机管理软件，现已免费。
- [VMware Fusion Pro](https://support.broadcom.com/group/ecx/productdownloads?subfamily=VMware+Fusion) 是 VMware 公司为 macOS 平台推出的虚拟机管理软件，现已免费。
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads) 是甲骨文公司发行的通用虚拟机管理系统，支持 Windows 和 macOS，且遵循 GPLv2 开源。

以上软件都是免费的，且支持中文。点击上面对应的链接进入官方下载页面获取安装包，获取完毕后，直接双击打开安装程序，根据安装步骤完成安装即可。

### 获取 Xubuntu 虚拟机镜像

Xubuntu 是 Ubuntu 的一个子发行版，它与 Ubuntu 非常类似，但其体积更小，性能需求更少，因此十分适合各种不同性能的电脑安装使用。本书的编写组已经制作了 Xubuntu 的虚拟机镜像，供读者按需求下载使用。

- （推荐）Xubuntu 24.04 64 位（ [VMware](https://ftp.lug.ustc.edu.cn/101/vm/VMware-Xubuntu-24.04-amd64.ova) ， [VirtualBox](https://ftp.lug.ustc.edu.cn/101/vm/VirtualBox-Xubuntu-24.04-amd64.ova) ）
- Xubuntu 22.04 64 位（ [VMware](https://ftp.lug.ustc.edu.cn/101/vm/VMware-Xubuntu-22.04-amd64.ova) ， [VirtualBox](https://ftp.lug.ustc.edu.cn/101/vm/VirtualBox-Xubuntu-22.04-amd64.ova) ）

目前 Ubuntu 已经不再提供 32 位字长的镜像支持，64 位的镜像可以在绝大部分计算机上运行，并且仍然支持运行 32 位的应用。

虚拟机镜像常见问题

我们在拓展阅读中添加了 [虚拟机镜像常见问题](https://101.lug.ustc.edu.cn/Ch01/supplement/#vm-faq) ，供读者参考。

有关虚拟机构建的信息

自 Xubuntu 22.04 开始，我们提供的虚拟机镜像由程序自动构建，相关代码可参见 [101strap](https://github.com/ustclug/101strap) 。在构建镜像时，我们对 Xubuntu 进行了一些定制与精简，以期在一般的硬件环境下也可流畅使用。

如果在使用自动构建的虚拟机镜像时遇到问题，欢迎在 [101strap 仓库的 issues](https://github.com/ustclug/101strap/issues) 中反馈。

Xubuntu

Xubuntu 的设计理念是创造一个易用且更轻量的 Ubuntu。与 Ubuntu 不同的是，它采用的是更轻量和兼容性更强的 Xfce 桌面系统，并基于 GTK 运行。Xubuntu 和 Ubuntu 使用完全一致的软件源，因此 Xubuntu 能运行绝大部分 Ubuntu 下的软件。

![](https://101.lug.ustc.edu.cn/Ch01/images/Xubuntu-Logo.png)

Xubuntu 图标

Ubuntu 的支持周期

不管从经济上还是技术上考虑，为一个固定版本的软件提供无限长时间的技术支持都是不现实的，对操作系统来说更是如此。因此，用户需要选择合适的操作系统版本，并且在支持周期结束前迁移或更新至新版本。在停止支持（End of Life，EOL）后，操作系统仍然可以继续运行，但是不再能够得到安全更新和功能更新。

对 Ubuntu 来说，其发行的版本主要分为两类：长期支持版本（Long Term Support，LTS）和中间版本（Interim releases）。Ubuntu 一般在每年四月和十月各发布一次新版本。其中 LTS 版本于每隔两年的四月份发布一次新版本，诸如 22.04、20.04、18.04；在其他时间发布的则是中间版本。

中间版本的支持周期为 9 个月，一般被需要使用最新特性的开发者使用；而 LTS 有五年 [^3] 的标准支持周期。根据 Ubuntu 官方的估算 [^4] ，在所有 Ubuntu 系统中有 95% 安装的都是 LTS 版本。

如果读者想要自己安装 Ubuntu 操作系统的话，以下两篇博客也可以参考：

- [在 Windows 下使用 VMware Workstation 安装 Ubuntu](https://ibug.io/p/15-cn) （另有 [英文版](https://ibug.io/p/15) ）
- [在 macOS 下使用 VMware Fusion 和 VirtualBox 安装 Ubuntu](https://blog.taoky.moe/2019-02-23/installing-os-on-vm.html)
Windows 下使用 VirtualBox

安装过程基本与 macOS 下安装 VirtualBox 一致，也可以参考 Windows 安装 VMware，两者大致相当；共享文件夹等功能可参考 [macOS 下 VirtualBox 安装 Ubuntu](https://blog.taoky.moe/2019-02-23/installing-os-on-vm.html#%E6%96%87%E4%BB%B6%E5%85%B1%E4%BA%AB-1) 。

![](https://101.lug.ustc.edu.cn/Ch01/images/VirtualBox-Create-VM.jpg)

VirtualBox 新建界面

对于日常惯用 Windows 10 及以上版本的用户来说，还有另一种更为便捷的安装 Linux 的方法。自 1607 版本起，Windows 10 支持适用于 Linux 的 Windows 子系统，可以在该子系统下安装若干主流的 Linux 发行版。详情可以参考拓展阅读： [适用于 Linux 的 Windows 子系统](https://101.lug.ustc.edu.cn/Ch01/supplement/#wsl) 。

Warning

请注意，本节中在 macOS 下安装虚拟机的步骤只适用于使用 Intel 处理器的 Mac。如果你使用的是基于 Apple Silicon 的 Mac，请参见 [在使用 Apple Silicon 处理器的机型上配置 Linux 虚拟机](https://101.lug.ustc.edu.cn/Ch01/supplement/#configure-vm-in-apple-silicon) 。

### 启动虚拟机

若已经安装了上述虚拟机管理软件，则可以直接双击打开虚拟机镜像，管理软件会打开并导入该镜像，导入完毕后可直接点击开始按钮启动。

![VirtualBox 导入镜像](https://101.lug.ustc.edu.cn/Ch01/images/VirtualBox-import.jpg)

VirtualBox 导入设置（需要手动选择镜像）

![VMware Workstation](https://101.lug.ustc.edu.cn/Ch01/images/VWP-Xubuntu-32bit-Login.png)

VMware Workstation 启动 Xubuntu 18.04 虚拟机

如果读者采用了上面列出的虚拟机之一，其默认登录用户名和密码均为 `ustc` ，输入密码即可登录虚拟机系统桌面。

![VMware Xubuntu Desktop](https://101.lug.ustc.edu.cn/Ch01/images/VWP-Xubuntu-32bit-Desktop.png)

Xubuntu 18.04 虚拟机桌面

## 中科大开源社群：LUG@USTC

LUG@USTC 是中国科学技术大学主流的开源社群，也是校内最大的学术科技类社团。其现今拥有数百名热爱开源文化的成员，并受益于他们而正在蓬勃发展。LUG@USTC 维护了中国最大的开源镜像站之一 [USTC Mirrors](https://mirrors.ustc.edu.cn/) ，其作为本土的软件源为国内许多开源软件用户提供了镜像服务，是本社群对社会作出的一项重要贡献。

![LUG@USTC](https://101.lug.ustc.edu.cn/Ch01/images/LUG%40USTC-Logo.png)

LUG@USTC 图标

### 了解与加入 LUG@USTC

你可以从 [LUG@USTC 官方网站](https://lug.ustc.edu.cn/wiki/) 中了解我们。官方网站中包括了我们在校内开展的各类流行活动和面向校内外提供的诸多网络服务。

LUG@USTC 欢迎校内外的朋友加入社群交流。如果你是中国科学技术大学在读学生，你可以通过致邮 附上姓名与学号申请加入本社群；如果你是校外人士，也可以致邮获取进一步的沟通交流方式。

## 思考题

计算机性能的增长

计算机的性能在过去几十年内一直呈现指数级增长，而如今其增速却已经放缓，转而开始偏向多核。在指数增长时代，计算机实际上经历过了几个不同的阶段，每个阶段都是通过不同的因素让计算机的性能快速增长。自行动手在线查阅资料，思考如下问题：

(1) 指数增长时代经历了哪几个阶段？每个阶段让计算机性能大幅提升的机制都是什么？

(2) 导致指数增长时代的终结的因素有哪些？

(3) 在多核时代，为了充分利用硬件性能，操作系统需要支持什么样的新特性？

免费软件和自由软件

在英文里，“免费软件”和“自由软件”都叫做“free software”，看起来很一致。事实上免费的软件是否一定自由？自由的软件是否也一定免费？

著作传

著作传（英文：copyleft）源于自由软件运动，是一种利用现有著作权的法律体制巧妙地保证用户自由使用软件的权利的许可方式。著作传一般包含哪些规则？它和常见的著作权有什么区别？它和完全放弃权利的“公有领域”又有什么不同？

![](https://101.lug.ustc.edu.cn/Ch01/images/Copyleft.png)

著作传的标志，注意到它与常见的著作权标志左右颠倒

## 其他资料

[Red Hat 公司制作的录音节目 Command Line Heroes](https://www.redhat.com/en/command-line-heroes)

纪念开源世界的历史与文化，对自己英语听力有自信的同学可以选择收听一下。

## 引用来源与备注

---

[^1]: 数据来自中国互联网信息中心 [第 56 次 《中国互联网络发展状况统计报告》（全文）](https://www.cnnic.net.cn/NMediaFile/2025/0730/MAIN1753846666507QEK67ZS9DH.pdf) 。

[^2]: 信息来自维基百科条目： [操作系统](https://zh.wikipedia.org/wiki/%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F) 。

[^3]: 尽管有许多说法称 Ubuntu LTS 有十年的支持，但是后五年实际上是 Extended Security Maintenance (ESM) 阶段，需要付费的 Ubuntu Advantage 订阅，或者最多 3 台设备的个人免费订阅。ESM 的安全更新仓库与主仓库也是独立的，需要登录后才能访问。

[^4]: 数据来自 Ubuntu 介绍： [The Ubuntu lifecycle and release cadence](https://ubuntu.com/about/release-cycle) 。

## 拓展阅读

本文已基本完稿，正在审阅和修订中，不是正式版本。

## Android/Linux

Android 是 Linux 发行版，但它不是 GNU/Linux，Android 不使用 GNU 的一系列工具和库。Android 还大幅度修改了 Linux 内核以精简运行时开销、适应移动设备。

[AOSP (Android Open Source Project)](https://source.android.google.cn/) 只使用了 GPL 许可证的 Linux Kernel，而在 Kernel 之上的 [ART (Android Runtime)](https://source.android.google.cn/docs/core/runtime) 、Bionic C 库、驱动透明化的 [HAL (Hardware Abstraction Layer)](https://source.android.google.cn/docs/core/architecture/hal) 则作为用户态存在，避免 Android 系统框架、Google 移动应用服务框架（GMS）和各厂商的驱动程序被 GPL 感染而开源。

![Android Stack](https://101.lug.ustc.edu.cn/Ch01/images/Android-Stack.png)

Android 软件堆栈

GPL 感染，以及开源许可证的区别

简单而不太严谨地来说，如果你的程序使用了 GPL 许可证的代码，那么你的程序就必须以 GPL 许可证开源，这被称为「GPL 感染」。由于许多公司不希望自己的代码被感染开源，因而 Android 经过设计规避了相关的法律问题，只需要厂商将对 Linux 内核的修改开源即可。

一个被 GPL 感染的例子是用于嵌入式路由器设备的 OpenWrt。由于 Linksys 在编写自己的无线路由器固件时使用了 GPL 的代码，因此不得不将相关的代码开源。OpenWrt 即由此发展而来。

GPL 许可证是在第一章正文中提到的「著作传」（Copyleft）许可的代表。而另一类开源许可证则更加宽松，允许用户在署名等前提下将代码使用在闭源软件中。这样的许可证代表如 MIT 许可证、Apache 许可证等。

目前，GitHub 网页版在创建 `LICENSE` 文件时，会给出一些开源许可证的选项以供选择。网络上也有相关的资料以供需要选择开源许可证的开发者们参考。

## 禁用 SELinux

读者在使用 Fedora、CentOS、Scientific Linux、RHEL 等系统时，可能会遇到这样的错误：

- SELinux is preventing XXXX from read access on the file YYYY.

这是因为有一个叫做 SELinux 的安全增强组件阻止了一些有潜在风险的操作。

SELinux 的全称是 Security-Enhanced Linux，起初是为了弥补 Linux 下没有强制访问控制（Mandatory Access Control, MAC）的缺憾。我们在 [附录](https://101.lug.ustc.edu.cn/Appendix/distribution/#selinux) 中也对 SELinux 做了进一步的介绍。

但是 SELinux 的设置相当繁复，由于默认设置不可能尽善尽美，一些配置上的小问题可能会影响用户的正常使用，而初学者没有足够的技能去调试 SELinux 策略。因此在初学时，可以暂且关闭 SELinux，在掌握足够的技能后再启用它。

AppArmor

在 Debian、Ubuntu 系发行版中，默认使用的是称作 AppArmor 的同类组件。与 SELinux 相比，AppArmor 更简单一些，且一般不会对用户的正常使用造成困扰。

SELinux 有 3 种工作模式：

1. `enforcing` ：SELinux 根据安全策略，积极阻止有潜在风险的操作。
2. `permissive` ：SELinux 仅记录会被阻止的操作在日志中，但不做任何事。
3. `disabled` ：SELinux 被彻底禁用，日志也不记录。

因此，只需将 SELinux 置于 `permissive` 或 `disabled` 状态即可。

使用 `sestatus` 命令查看 SELinux 状态：

```js
$ sestatus
SELinux status:                 enabled
SELinuxfs mount:                /sys/fs/selinux
SELinux root directory:         /etc/selinux
Loaded policy name:             targeted
Current mode:                   enforcing
Mode from config file:          enforcing
Policy MLS status:              enabled
Policy deny_unknown status:     allowed
Memory protection checking:     actual (secure)
Max kernel policy version:      31
```

使用 `setenforce 0` **临时** 改变 SELinux 状态到 `permissive` ，这个状态在重启后将恢复为配置文件指定的默认值。

```js
# setenforce 0
```

修改 SELinux 的配置文件可以永久改变 SELinux 的工作状态。

1. 使用 root 权限编辑 `/etc/selinux/config` 文件；
2. 将 `SELINUX=enforcing` 中的 `enforcing` 改为 `disabled` 或 `permissive` 。

编辑完成后，使用 `sestatus` 可以看到修改效果：

```js
[...]
Current mode:                   permissive  # <-
Mode from config file:          permissive  # <- 或 disabled
[...]
```

## 虚拟机镜像常见问题

本部分提供有关我们提供的 XUbuntu 虚拟机镜像的常见问题以及解答。

### 屏幕缩放

如果在高分屏（HiDPI）上安装系统，可能会遇到屏幕缩放的问题。可以通过以下方法确认自己是否正在使用高分屏：

- Windows: 桌面右键，点击「显示设置」，在「缩放与布局」中查看其中的百分比，如果大于 100%，则是高分屏。
- Mac: 如果你的 Mac 是 Retina 屏幕，那么它就是高分屏。也可以对比「关于本机」->「更多信息」中显示器的分辨率规格与「显示器设置」中实际的分辨率。

因此，虚拟化软件有两种策略。以物理分辨率为 2560x1600，逻辑分辨率为 1440x900，全屏显示为例（缩放比大约为 178%）：

- 向虚拟机汇报实际的物理像素（2560x1600），这样默认情况（不缩放）下虚拟机中的文字和图标会变得非常小。
- 向虚拟机汇报缩放后的像素（1440x900），这样默认情况下虚拟机中的文字和图标大小是正常的，但是会模糊一些。

如果对显示效果不满意，可以采取以下任一方式调整。

#### 调整虚拟化软件的缩放策略

VirtualBox 可以在启动后调整缩放策略。点击菜单栏的「查看」（或「视图」）->「虚拟显示屏 1」（或「虚拟显示器 1」），可以看到缩放比例选项，并且有两种包含了备注的比例：

- 100%（输出未缩放/unscaled output）：代表向虚拟机汇报实际的物理像素。
- 输出自动缩放/autoscaled output：代表向虚拟机汇报缩放后的像素。

默认选择的是 100% 选项，因此可能首次开机会发现界面过小。如果可以接受界面略显模糊，可以选择「输出自动缩放」。

VMware Fusion (macOS) 中，相关设置在设置中的「显示器」选项卡中。默认「使用 Retina 全分辨率显示」是关闭的，代表向虚拟机汇报缩放后的像素。

VMware Workstation (Windows) 中其默认会向虚拟机汇报实际的物理像素。取消选择「在虚拟机中自动调整用户界面大小」（如果有），启用拉伸模式并减小监视器最大分辨率可以实现 UI 大小正常且模糊的效果。免费版本的 Workstation Player 不支持拉伸模式。

#### 调整 Xfce 下的缩放

Xfce 下有多处与缩放调整有关的设置。调整 Xfce 的缩放有两种方式：

- 调整显示器缩放设置
- 调整元素 DPI

点击左上角，选择设置管理。在「硬件」->「显示」中可以调整显示器缩放。

Xfce 的显示器缩放比 bug

Xfce 的显示器缩放比和正常人类认知是相反的——1.5x 的实际效果是 (1/1.5)x。 这是一个 [已知的 bug](https://gitlab.xfce.org/xfce/xfce4-settings/-/issues/259) ，并且直到现在，可能是因为担心破坏现有用户的设置，还没有被修复。

因此，如果你需要缩放，需要选择「自定义」，然后输入你想要的缩放比的倒数（保留一位小数）——例如，1.5x 的缩放需要输入 0.7。 并且有可能元素仍然是不清晰的。因此这里更推荐调整元素 DPI 的做法。

在「外观」->「字体」中可以调整元素 DPI。默认情况下，Xfce 的 DPI 是 96，将其乘以预期的缩放比并输入。 此时可能会发现 UI 不太协调，以下提供了一些可能需要调整的设置，按类似方式相乘即可：

- 桌面图标：右键桌面 -> 桌面设置 -> 图标 -> 图标大小
- 托盘大小：右键面板 -> 面板 -> 面板首选项 -> 「尺寸」下面的「行大小」
- 鼠标光标：设置 -> 硬件 -> 鼠标和触摸板 -> 主题 -> 光标大小

如果你觉得上面的做法太麻烦了，我们也提供了一个脚本 `toggle-hidpi` 来帮助你快速切换。该脚本基于 [Kali Linux 的 kali-hidpi-mode 包修改](https://gitlab.com/kalilinux/packages/kali-hidpi-mode/-/blob/kali/master/kali-hidpi-mode?ref_type=heads) 。使用方法如下：

```js
$ # 如果没有使用我们最新的虚拟机镜像，可以先下载脚本：
$ sudo wget -O /usr/local/bin/toggle-hidpi https://github.com/ustclug/101strap/raw/refs/heads/master/assets/toggle-hidpi
$ sudo chmod +x /usr/local/bin/toggle-hidpi

$ # 使用方法：
$ toggle-hidpi 2  # 2x 缩放
$ toggle-hidpi 1.5  # 1.5x 缩放
```

### 扩大磁盘大小

为了在可用磁盘空间较小的情况下也能快速体验，我们提供的虚拟机镜像磁盘仅设置了 5G，有可能会遇到空间不足的问题。 VMware 的操作较为直观，而 VirtualBox 将工具放在了较深的位置： 需要选择 Tools 旁的菜单，点击 Media 后在右侧双击对应的磁盘，即可扩容。

视虚拟化软件实现，扩大磁盘后进入系统可能需要进行额外的操作。打开终端，输入 `sudo fdisk -l` 确认 **分区** 是否被扩大 （密码不会显示 `*` ，输入之后什么都不显示是正常的，确认输入正确后按下回车即可）：

```js
$ sudo fdisk -l
[sudo] ustc 的密码：
Disk /dev/sda: 10 GiB，10737418240 字节，20971520 个扇区
Disk model: VBOX HARDDISK
单元：扇区 / 1 * 512 = 512 字节
扇区大小(逻辑/物理)：512 字节 / 512 字节
I/O 大小(最小/最佳)：512 字节 / 512 字节
磁盘标签类型：gpt
磁盘标识符：12526913-E330-4CA7-A379-90A87EF858B0

设备         起点    末尾    扇区  大小 类型
/dev/sda1     2048  499711  497664  243M EFI 系统
/dev/sda2   499712  20971486  20471775  9.8G Linux 文件系统
```

这里可以看到， `/dev/sda2` 这个 **分区** 被自动扩大了。 如果没有，那么可以输入以下命令（请勿输入 `$` ，详见 [记号约定](https://101.lug.ustc.edu.cn/notations/#command-line) ）：

```js
$ LANGUAGE=C sudo growpart /dev/sda 2
```

growpart 在非英语环境下的 bug

在非英语环境中，由于 growpart 脚本会尝试检查 sfdisk 工具的版本，而其无法识别翻译之后的版本信息，因此会报错。这里使用 `LANGUAGE=C` 来临时将环境变量 `LANGUAGE` 设置为英语，以避免这个问题。

该问题已经 [在上游修复](https://github.com/canonical/cloud-utils/pull/30) 。但是 Ubuntu 22.04 未包含这个修复。

在扩大分区后，还需要扩大 **文件系统** 。使用 `df -h` 检查 `/dev/sda2` 上文件系统的使用情况。 VMware 与 VirtualBox 的扩容操作可能都不会自动扩大文件系统，因此需要执行以下命令，手动扩大文件系统。

```js
$ sudo resize2fs /dev/sda2
```

如果有过分区经验，也可以安装图形化的 GParted 工具进行操作。

### 虚拟机网卡的“模式”

在虚拟机中使用网络设备时，会发现虚拟机一般有三种网卡模式，分别叫做 `Bridged` （桥接）、 `NAT` （网络地址转换）、 `Host only` （仅主机）。虚拟机中的网络设备，是虚拟网卡（Virtual NIC），其背后需要与某个网络连接，才能实现通信功能。

在安装虚拟机前，设备上的网络通常是这样的：

#### 桥接模式

在这种模式下，虚拟机程序（例如 VMWare）会在主机上创建一个虚拟交换机。虚拟交换机上，接入了原来的物理网卡（例如有线网卡或者 Wi-Fi 适配器等）、虚拟机中安装的虚拟网卡、主机上的虚拟网卡。在这种配置下，虚拟机和主机都暴露在外部网络下，分别使用 **不同的 IP** 。

#### 网络地址转换模式

与桥接模式不同，网络地址转换下，虚拟机和主机 **共用一个 IP** ，虚拟机之间用虚拟交换机连接。从外部网络看来，虚拟机上的程序和主机上的程序发出的请求是一样的。

#### 仅主机模式

仅主机模式类似 NAT，但是虚拟机不能与外部网络通信。

### 已知问题

#### 在 macOS VirtualBox 下闪屏

我们发现 VirtualBox 在导入镜像后会为虚拟机设置有问题的显卡控制器，导致在 macOS 下出现闪屏问题。 在虚拟机设置中将显示控制器修改为 VMSVGA 后可以解决此问题。

#### VirtualBox 下图形性能较差

在虚拟机设置中将显存调整至最大（128 MB），并且启动 3D 加速，可以提升图形性能。 如果仍未改善，建议选择「输出自动缩放」模式，降低虚拟机中的分辨率。

macOS VirtualBox 的问题

macOS 下的 VirtualBox 经测试发现，在启用需要 OpenGL 的程序（如 glxgears）后可能会出现控制问题，无法正常操作窗口，原因不明。 如果遇到类似的问题，可以考虑切换至 VMware Fusion Player。

## 配置与使用 SSH 连接远程的 Linux 服务器

在本章节正文中，我们介绍了如何在本地运行 Linux 操作系统。但是在实际操作时，一个非常常见的需求是连接到远程的服务器。Linux 提供了非常方便安全的 SSH 功能，可以让用户连接到远程的 Linux 服务器命令行执行操作。

在这里，我们将简单介绍在服务器上配置 SSH，以及如何使用 SSH 连接到远程的服务器。

安装前请务必修改弱密码

互联网上有着大量爆破用户名和弱密码的自动化程序，如果密码很弱（位数不够长，或者使用了常见的密码），那么黑客就能很快使用 SSH 登录到你的系统中获取控制权，使得你的电脑（服务器）成为肉鸡（被黑客利用攻击其他服务器），在你的电脑上安装挖矿软件等恶意软件，删除你的数据进行勒索。甚至在校园网中，服务器由于 SSH 弱密码被攻击的例子也屡见不鲜。

由于 SSH 服务器默认不关闭密码验证，在安装前请务必使用 `passwd` 命令修改弱密码！

在服务器上首先安装 `openssh-server` 软件包，它提供了 SSH 服务器的功能。

```js
$ sudo apt install openssh-server
```

启动并检查 SSH 服务状态：

```js
$ sudo systemctl start ssh
$ sudo systemctl status ssh
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset: enabled)
     Active: active (running) since Thu 2022-02-24 16:47:39 CST; 1min 15s ago
       Docs: man:sshd(8)
             man:sshd_config(5)
   Main PID: 1689 (sshd)
      Tasks: 1 (limit: 2250)
     Memory: 2.0M
     CGroup: /system.slice/ssh.service
             └─1689 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups

2月 24 16:47:39 ustclug-linux101 systemd[1]: Starting OpenBSD Secure Shell server...
2月 24 16:47:39 ustclug-linux101 sshd[1689]: Server listening on 0.0.0.0 port 22.
2月 24 16:47:39 ustclug-linux101 sshd[1689]: Server listening on :: port 22.
2月 24 16:47:39 ustclug-linux101 systemd[1]: Started OpenBSD Secure Shell server.
```

我们可以使用 `ssh` 命令直接连接到本地（localhost）的 SSH 服务器。其中 `@` 符号前的是登录的用户名，后面的是服务器的域名或 IP 地址。

```js
$ ssh ustc@localhost
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:czt1KYx+RIkFTpSPQOLq+GqLbLRLZcD1Ffkq4Z3ZR2U.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'localhost' (ECDSA) to the list of known hosts.
ustc@localhost's password:
Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 5.13.0-28-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

0 updates can be applied immediately.

Your Hardware Enablement Stack (HWE) is supported until April 2025.

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

ustc@ustclug-linux101:~$
```
第一次连接时的提示

在初次连接时会有类似于下面这样的提示，需要输入 `yes` 才能继续连接：

```js
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:czt1KYx+RIkFTpSPQOLq+GqLbLRLZcD1Ffkq4Z3ZR2U.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

这是因为初次连接时，SSH 不知道连接到的服务器是否真的是我们指定要连接的服务器：网络中的「中间人」可能会截获我们与服务器之间的网络流量，将自己伪装成对应的服务器。所以，SSH 会要求你确认密钥的指纹是否与预期相一致，如果不一致，则说明可能出现安全问题，应该立刻断开连接。

服务器的密钥信息会记录在本地，之后连接相同的服务器就不会再弹出这个提示。如果远程服务器的密钥和本地记录的信息不一致，会输出类似下面的错误信息：

```js
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the RSA key sent by the remote host is
12:34:56:78:90:ab:cd:ef:12:23:34:45:56:67:78:89.
Please contact your system administrator.
Add correct host key in /home/ustc/.ssh/known_hosts to get rid of this message.
Offending RSA key in /home/ustc/.ssh/known_hosts:12
RSA host key for 127.0.0.1 has changed and you have requested strict checking.
Host key verification failed.
```

可能的原因是你连接到了错误的服务器、服务器的密钥被更换，或者最糟糕的可能性：有人在尝试对你进行网络攻击。

也可以测试一下从其他机器连接到服务器。

获取服务器的 IP 地址

可以使用 `ip a` 命令查看服务器的 IP 地址。

如果无法连接，请检查服务器的防火墙是否放行了 TCP 22 端口。

配置密钥登录

上面我们提到，弱密码会导致黑客能够轻而易举从 SSH 入侵服务器，但是每次登录输入复杂密码会很烦，怎么办呢？其实，SSH 提供了一种相当方便、简单、安全的连接方式：密钥认证。它的原理是，用户生成一对密钥，将公钥放在服务器上，登录时 SSH 自动使用私钥认证，两者相符则允许用户登录。

首先在自己的机器上使用 `ssh-keygen` 生成密钥：

```js
$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/ustc/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ustc/.ssh/id_rsa
Your public key has been saved in /home/ustc/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:/+4tXnjnilyLQvwa+qEKx0IK2jOzHRj0Nbarr3Vot1E ustc@ustclug-linux101
The key's randomart image is:
+---[RSA 3072]----+
|                 |
|                 |
|  .   +          |
| . . o o         |
|. . o . S.E      |
|.o = . o oo  .   |
|. B + B +.+.. + .|
|   * O o =.=oB + |
|  . +oo.+.o*O.+..|
+----[SHA256]-----+
```

这里的 passphrase 是密钥的密码，设置之后即使私钥被别人拿到也无法使用，可以不输入。最终得到的 `id_rsa` 是私钥（ **千万不要分享给别人！** ）， `id_rsa.pub` 是公钥（可以公开）。

在本地使用 `ssh-copy-id` 命令将公钥拷贝到服务器上：

```js
$ ssh-copy-id ustc@localhost
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
ustc@localhost's password:

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'ustc@localhost'"
and check to make sure that only the key(s) you wanted were added.
```

如果服务器不允许使用密码登录，可以将用户目录下 `.ssh/id_rsa.pub` 文件的内容复制到机器对应用户的 `.ssh/authorized_keys` 文件中。

配置完成后，可以考虑关闭 SSH 服务器的密码验证。做法是编辑 `/etc/ssh/sshd_config` 文件，将其中

```js
#PasswordAuthentication yes
```

修改为

```js
PasswordAuthentication no
```

然后让 SSH 服务器重新加载配置：

```js
$ sudo systemctl reload ssh
```

我们建议除非有特殊原因，否则所有正式生产环境服务器（例如实验室服务器）都应该关闭 SSH 密码验证。

## 适用于 Linux 的 Windows 子系统（Windows Subsystem for Linux，WSL）

如何将 Linux 下的软件与开发生态移植到 Windows 上？在 WSL 出现之前，开发者们进行了各种尝试。这也催生出了一些软件与方案，例如：

- Cygwin。它包含了一大批 Linux 上的 GNU 和其他的开源工具。它的核心是一个程序库 (`cygwin1.dll`)，这个程序库在 Windows 环境下实现了 POSIX API 的功能。Linux 上的软件，可以通过 **重新编译** ，链接 Cygwin 的方式，在 Windows 上运行。
- MinGW。它包含了 GCC 和 GNU Binutils 等工具的 Windows 移植。它不支持类似于 `fork()` 这样无法简单用 Windows API 实现的 POSIX API，但是相比于 Cygwin 来说更加轻量，甚至可以在 Linux 上使用 MinGW 交叉编译 Windows 程序。
- MSYS2。使用 Cygwin 和 MinGW 组建的开发环境，并且使用 Pacman 作为包管理器。
- Cooperative Linux。这个项目尝试让 Linux 内核和 Windows 内核同时运行在相同的硬件上。Linux 内核经过修改，以能够与 Windows 内核共享硬件资源。这个项目已经长期未活跃了。

当然，我们可以看到，没有一个稳定的方案可以不加修改地直接运行 Linux 程序，直到 WSL 出现。WSL 由微软开发，可以在 64 位的 Windows 10 和 Windows Server 2016 及以上的版本上运行原生（ELF 格式）的 Linux 程序（安装方法详见 WSL 的官方 [安装指南](https://learn.microsoft.com/zh-cn/windows/wsl/install) ）。

不要将 WSL 与 Windows Services for UNIX (SFU) 混淆

你可能会在老版本的 Windows 上注意到，在「添加与删除 Windows 组件」的地方，有一个「基于 UNIX 的应用程序子系统」。需要注意的是，这个选项和 WSL 没有任何关系。它也无法直接运行 Linux 或者其他 UNIX 的程序。并且，这个子系统目前也已经停止了开发。

WSL 对宿主机文件系统的挂载

请注意， **WSL 可能将主机的文件系统挂载在子系统的某个位置（例如将主机的 `C:\` 挂载在 `/mnt/c/` ）** 。这在通常情况下会使得主机和 WSL 之间的文件共享更加方便，但也可能导致在子系统中执行文件操作（例如文件删除）时错误地操作了主机上的文件。

### WSL 1

WSL 1 面向 Linux 应用程序提供了一套兼容的内核接口，在 Linux 程序运行的时候，WSL 1 处理（Linux 使用的）ELF 可执行文件格式，将 Linux 的系统调用翻译为 Windows 的系统调用，从而运行 Linux 程序。WSL 1 中可以访问到 Windows 下的文件，也与主机共享网络。

### WSL 2

WSL 2 尝试解决一些 WSL 1 的方式难以解决的问题：

- 由于其是以翻译系统调用的方式实现 Linux 兼容，WSL 1 无法运行依赖于复杂内核特性的程序（如 Docker），无法运行硬件驱动程序。
- 没有硬件加速，图形性能差。OpenCL 与 CUDA 也尚未在 WSL 1 中实现。
- 受到各种因素的影响（如 Windows Defender），WSL 1 的 I/O 性能远低于 Linux 内核的实现。

WSL2 使用微软的 Hyper-V 虚拟化技术，运行一个轻量的、完整的 Linux 内核。

## 在使用 Apple Silicon 处理器的机型上配置 Linux 虚拟机

正在查看 Linux 101 的你可能正在使用基于 Apple Silicon 处理器的 Mac。此时使用在文章正文中的教程是无法安装虚拟机的。本节将帮助你使用 VMWare Fusion 在基于 Apple Silicon 处理器的 Mac 上配置一个 Ubuntu 20.04 的虚拟机。

你也可以使用 [UTM](https://mac.getutm.app/) 来配置你的 Ubuntu 虚拟机。

什么是 Apple Silicon？

Apple Silicon（苹果硅）是对苹果公司使用 ARM 架构设计的单芯片系统（SoC）和封装体系（SiP）处理器之总称。它广泛运用在 iPhone、iPad、Mac 和 Apple Watch 以及 HomePod 和 Apple TV 等苹果公司产品。 [^1]

若想查看你的 Mac 是否使用了 Apple Silicon，请参照 [这个网页](https://support.apple.com/en-us/HT211814) 。

x86-64 架构和 ARM64 两种架构都是什么？它们有什么区别？

ARM64（也被称为 AArch64）是 ARM 公司推出的 64 位处理器架构。它被广泛用于移动设备、嵌入式系统和服务器领域。与之前的 32 位架构相比，它具有更高的性能和更好的功耗管理。

x86-64 也被称为 x64 或者 AMD64。它广泛应用于 PC 和服务器领域，并且兼容大部分之前的 32 位 x86 应用程序。

在使用上，这两种架构是不兼容的，即针对一种架构编译的程序无法直接在另一种架构上运行。这也是使用 Apple Silicon 处理器的 Mac 无法通过正文中的流程配置 Ubuntu 虚拟机的原因。

### 使用 VMWare Fusion 配置你的第一个 Ubuntu 虚拟机

本节内容涉及到尚未完善的系统及软件，实际操作随时会发生变化。本次更新在 2023 年 2 月。

可供参考的内容：

- [The Unofficial Fusion 13 for Apple Silicon Companion Guide](https://communities.vmware.com/t5/VMware-Fusion-Documents/The-Unofficial-Fusion-13-for-Apple-Silicon-Companion-Guide/ta-p/2939907/jump-to/first-unread-message)

如果遇到以上文档中无法解决的问题，可以继续参考下面的两个针对于 VMWare Fusion 22H2 Tech Preview 的文档：

- [Fusion 22H2 Tech Preview Testing Guide](https://communities.vmware.com/t5/Fusion-22H2-Tech-Preview/Fusion-22H2-Tech-Preview-Testing-Guide/ta-p/2867908)
- [Tips and Techniques for the Apple Silicon Tech Preview 22H2](https://communities.vmware.com/t5/Fusion-22H2-Tech-Preview/Tips-and-Techniques-for-the-Apple-Silicon-Tech-Preview-22H2/ta-p/2893986)

#### 下载 VMWare Fusion 13 Player

在 [Download VMWare Fusion](https://www.vmware.com/products/fusion/fusion-evaluation.html) 上下载 VMware Fusion 13 Player，需要注册。

#### 下载 Ubuntu Server for ARM

首先你需要选择 Ubuntu 发行版。截止到 2023 年 2 月，各个较新的发行版在 VMWare Fusion 上的支持情况为：

- Ubuntu 20.04.5 LTS (Focal Fossa)：可以使用，需要经过改动才能修改图形界面的分辨率。
- Ubuntu 22.04 LTS (Jammy Jellyfish)：从 Ubuntu 22.04.2 LTS 开始可以直接使用。

本节选用 Ubuntu 20.04.5 (arm64, server) 作为接下来安装的系统。

![Choose arm64 image](https://101.lug.ustc.edu.cn/Ch01/images/applesilicon_vmware/1.png)

你可以在 [中国科学技术大学开源软件镜像](https://mirrors.ustc.edu.cn/) 获取安装镜像。

#### 在 VMWare Fusion 上安装 Ubuntu on ARM

下载好安装镜像后，打开 VMWare Fusion，导入你下载的镜像：

![VMware Fusion](https://101.lug.ustc.edu.cn/Ch01/images/applesilicon_vmware/2.png)

点击左上角的加号创建新的虚拟机

![VMware Fusion new VM](https://101.lug.ustc.edu.cn/Ch01/images/applesilicon_vmware/3.png)

将你下载好的镜像拖入框中

![VMware Fusion choose image](https://101.lug.ustc.edu.cn/Ch01/images/applesilicon_vmware/4.png)

导入完成之后使用默认配置即可，你也可以按照自己的需求对 configuration 进行对应的改动。

![VMware Fusion Ubuntu server install](https://101.lug.ustc.edu.cn/Ch01/images/applesilicon_vmware/6.png)

用键盘对命令行界面进行操作，在配置用户名前的配置一般可以选择默认配置。本页面中你需要配置你的用户名，服务器名称和密码。

如果你不需要远程连接你的虚拟机，你可以不安装 `openssh-server` （当然，你可以在之后自行安装）。

Featured Server Snaps 一样可以选择不安装，可以之后自行配置。

安装完成之后会重启，之后你会进入命令行界面。这就是一个没有图形界面的虚拟机，你可以对它进行任何你想做的尝试了！

如果你需要带图形界面的虚拟机，只需要安装 `ubuntu-desktop` 即可。

```js
$ sudo apt-get install ubuntu-desktop
```

安装好之后需要重新启动虚拟机，这时你应该可以看到你的登陆界面了：

![VMware Fusion GDM](https://101.lug.ustc.edu.cn/Ch01/images/applesilicon_vmware/7.png)

虚拟机的图形界面

值得注意的是，在选择软件源时，你应该使用 [Ubuntu Ports 源](https://mirrors.ustc.edu.cn/help/ubuntu-ports.html) 而不是 [Ubuntu 源](https://mirrors.ustc.edu.cn/help/ubuntu.html#id3) 。

在 VMWare Fusion 13 Player 上安装的 Ubuntu 20.04.5 (arm64, server) 虚拟机并不原生支持修改分辨率

如果你通过上面的步骤安装好了带有图形界面的 Ubuntu 虚拟机，你可能会发现在设置中并不能调整图形界面的分辨率（它被限制在了 1024\*768）。简而言之，这是因为 ARM64 版本的 Linux 内核从 5.14 版本开始才支持 VMWare 为 Linux 适配的图形驱动 `vmwgfx` 。而 Ubuntu 20.04 原生 Linux 内核是 5.4 版本的，并不包含 VMWare 适配的驱动。所以如果你想修改 Ubuntu 虚拟机的分辨率的话，有两种选择：

- 使用 Ubuntu 22.04 或 22.10：目前只有部分 daily build 版本可用。
- 在 Ubuntu 20.04 上 **禁用 Wayland**:
	```js
	$ sudo nano /etc/gdm3/custom.conf
	```
	解除该行的注释（删除下面这行代码之前的 `#` ）后，保存退出：
	```js
	#WaylandEnable=false
	```

接下来自行通过 HWE 升级 Ubuntu 20.04 的内核至 5.15:

```js
$ sudo apt install --install-recommends linux-generic-hwe-20.04
```

重启虚拟机，在设置中进行分辨率的修改。

## 使用 Ventoy

使用 Ventoy 可以简单方便地从 U 盘或者其他移动介质安装各类操作系统（且支持在一个介质中存放多个系统镜像），当然也包括 GNU/Linux。有关如何使用 Ventoy，请参考其网站 [^2] 。

## 引用来源

---

[^1]: [Apple silicon - Wikipedia](https://en.wikipedia.org/wiki/Apple_silicon)

[^2]: [Ventoy 中文网站](https://www.ventoy.net/cn/index.html)
## 思考题解答

## 计算机性能的增长

提示

本题在书中没有答案，并且计算机性能的时代也不存在十分明确的分界线。所以本题可算作一个开放题，并且鼓励各位读者自行查阅资料来形成自己的答案。

本题与计算机的体系结构比较相关，建议读者查阅的时候可以以此为关键词。

解答

**(1)**

计算机的指数增长时代大致可以认为由 2 个阶段构成：

- 复杂指令集阶段：这个阶段是大规模集成电路阶段的开始。在这个阶段，得益于电路的集成度大幅度提升，计算机的性能也成指数级增长。这个阶段大致的时间范围是 1978 - 1986 年，平均每年性能提升 22%。
- 精简指令集阶段：随着时间的推移，人们发现许多指令通常都用不到，但它们的存在让处理器不得不采用更复杂的结构，因此研究员开始提倡精简之前的指令集架构以简化处理器。在使用了精简后的指令集架构后，计算机的性能相较之前有了飞跃般的提升（最初在 IBM 360 指令集架构上是 3 倍）。同时，集成电路的密度依然在继续增加，且在这个阶段开发人员通过大力改进“指令级并行”以提升性能，因此此时计算机的性能以更快的速度增长。这个阶段大致的时间范围是 1986 - 2003 年，平均每年性能提升 52%，是计算机科技的黄金时代。

**(2)**

计算机指数增长的黄金年代之所以能长期保持，主要还是因为集成电路的密度可以稳定大幅度提升。罗伯特·丹纳德（Robert Dennard）归纳了一个规律，被称之为丹纳德标度（Dennard Scaling）：“在晶体管的密度增加的时候，单个晶体管的功耗会下降，这样下来可以保持晶体管的功耗密度（每单位面积的功耗）不变”。根据这条规律，在晶体管密度增加的同时，计算机性能会提升（正比例于晶体管数目），但功耗不变，因此计算机的能量利用率会越来越高。

不过，这条规律没有考虑到一些重要的问题。一个问题是晶体管的“漏电电流”（微安级别），即晶体管在工作时会有轻微漏电，这些漏电会导致处理器发热，如果不加以控制会造成严重的散热问题。当然，可以通过降低电压的方法来减少散热，但此时也出现了第二个问题，即是晶体管的“阈值电压”（大约是 0.7 ~ 0.8 伏），可以理解成最低工作电压，低于此电压晶体管不再工作。这两个问题导致了晶体管存在一个不可跨越的最低功率（以及最低发热功率），从而使得丹纳德标度失效。进一步增加密度将需要更多能耗而不再恒定，也会导致散热问题。因此，为了避免这个问题，芯片厂商研究了多核处理器来达到并行的效果，从而进入了多核时代。

- 后丹纳德标度阶段：这是多核时代的第一个阶段，这个阶段计算机性能提升的主要因素是采用了多核处理器，通过并行的方式提升计算机的性能。这个阶段大致的时间范围是 2003 - 2011 年，平均每年性能提升 23%，相比之前的 52% 是一个巨大的跌落。

**(3)**

在多核时代，操作系统显然需要适应多核处理器，而其中一个最重要的能力就是进行并行任务调度，即将任务按合适的方式交付给不同的核来同时完成以尽可能充分利用并行的优势。

**题外话**

然而，核并不是越多越好的，因为一个任务总会有一些先后次序是不能颠倒的，所以这些部分就必须串行运行。就算假设一个任务能并行的部分可以被完美地平均切分而并行执行，剩余的串行部分也无法利用到并行的任何收益（而且往往过度的并行反而降低效率），因此增加更多核的收益会越来越低。这种规律被称之为阿姆达尔定律（Amdahl's Law），核的数目越多，越受到阿姆达尔定律的限制。

- 阿姆达尔定律阶段：这是多核时代的第二个阶段，这个阶段标志着多核所带来的性能提升已经越来越不明显了。这个阶段大致的时间范围是 2011 - 2015 年，平均每年性能提升只有 12%。

在 2015 年以后，平均每年的性能提升更是暴跌至 3%，似乎大规模集成电路计算机的性能提升已经快到了尽头，因此又被称为终结阶段。

![](https://101.lug.ustc.edu.cn/Ch01/images/Performance-Era.jpg)

大规模集成电路计算机性能的五个阶段

## 免费软件和自由软件

提示

要回答本题，需要明确了解“自由软件”的概念。依据自由软件基金会的定义，自由软件是一类可以不受限制地自由使用、复制、研究、修改和分发的，尊重用户自由的软件。 [^1] 可以注意到这里的定义和免费没有什么关系。

为了更好地理解这两种定义之间的关系，最好从正反两面举出几个实际例子。

解答

免费软件并不一定自由，因为免费的软件可能只是软件的所有者提供了免费许可，但并不一定也会同时允许用户自由地去研究、修改和分发。一些反例诸如：

- QQ: 腾讯公司推出的免费即时通讯软件，在中国十分主流，不过显然腾讯公司从来没公开过 QQ 的源代码，也不允许用户去自行修改它。
- Adobe Reader：Adobe 公司推出的免费 PDF 阅读器，但该公司拥有该软件的所有权，并且此软件也不开源，不允许用户去修改。
- WPS Office：金山办公旗下的一系列办公软件的组合，它是免费的，但同样不允许用户研究和修改。

支持这个命题的例子不胜枚举，比如许多收费的专业软件的个人版、教育版或者社区版等都是免费但不自由的软件。

自由软件也并不一定免费。虽然对于不少初接触的读者来说可能稍微难以想象：因为自由软件一般都是遵循自由软件协议开源的，谁都可以拿出去编译成自己的副本，似乎没有收费的余地。其实不然，一是自由软件的定义并不妨碍其收费，因此理论上想收费就可以收费；二是自由软件的发行商可以为顾客提供专业的技术服务，此时相当于买自由软件的这笔钱可以购买到专业技术支持。一个十分典型的例子就是本章中提到的 Red Hat 公司推出的 RHEL，它是收费的，但遵循 GPL 开源。使用 RHEL 源代码编译成的免费版本（再去掉 RHEL 本身包含的闭源软件和 Red Hat 商标信息）就是本章正文中提到的 CentOS 了。

## 著作传

提示

本题实质上仅要求读者了解“著作传”的定义和它与其它两种许可方式的区别，难度并不大。不过，本章正文中没有给出著作传的完整定义，因此本题鼓励读者自行查阅在线资料来掌握这个知识。

解答

著作传的概念源于自由软件运动，是一种利用现有的“著作权”的体制来保障用户软件自由使用权利的许可方式。通常来说，著作传保证了任何用户都可以自由地使用、复制、修改和传播所许可的软件，不过基于这个软件的复制传播和修改后的再分发通常还必须以著作传的方式发布，即后续的用户也能享受到同等的自由。

由上面的解释可见，著作传许可比通常的著作权提供的使用许可要宽容、自由得多，因此可能部分初次接触这个概念的读者会觉得这个许可方式和直接放出去让大家随便使用没什么区别，然而这种想法是不对的。事实上，著作传和著作权、公有领域的关系和区别有以下几个显著的要点：

- 著作传虽然允许软件可以以很自由的方式给用户使用，但用户依然需要遵守著作传的许可，而不是像公有领域的产品一样可以完全随心所欲。著作传许可的一个典型特性就是要求它的传播和衍生还是要继续采用著作传许可，而不可以申请自己的著作权，也不能重新赋予新的许可。这种方法保证了这个软件的权利完全由人类共同体充分享受，不过这种方式也得到了一些反对声音，因为这种许可的传播方式看起来太像是病毒传染。
- 著作传是利用了现有的著作权体系设立的，这说明著作传许可虽然自由，但实际上也可以认为是对软件的一种保护，是另一种“著作权”。这也说明了著作传理论是一种受到法律保护的许可（如果当地法律兼容的话），而不是某种大家自发遵守的倡议。不过和普通的著作权不同，著作传许可面向用户下放了许多权利，这是通常的著作权许可不会做的。

## 引用来源

---

[^1]: 定义来自维基百科条目： [自由软件](https://zh.wikipedia.org/wiki/%E8%87%AA%E7%94%B1%E8%BD%AF%E4%BB%B6) 。