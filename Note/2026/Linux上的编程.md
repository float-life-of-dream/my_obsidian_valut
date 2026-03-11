[跳转至](https://101.lug.ustc.edu.cn/Ch07/#linux)

## Linux 上的编程

本文已完稿并通过审阅，是正式版本。

导言

作为一个成熟而实用的系统，我们该如何在 Linux 上进行日常的编程开发呢？ 这一章将解答一下几个问题：

- Linux 上的 C/C++ 开发
- Linux 上的 Python 开发
- Linux 上编程语言开发的范式与共性

## C 语言开发

C 语言是大学编程语言教学中几乎必定讲解的一门编程语言。 考虑到 Linux 内核即是用 C 语言编写的，在 Linux 上 C 语言拥有近乎系统级的支持。 在 Linux 上开发 C 语言（以及 C++）是一件非常轻松、方便的事。

### 从单文件开始

现在假设我们有一份源码文件 main.c，内容如下：

```js
// main.c
#include <stdio.h>

int main() {
  printf("Hello World!\n");
  return 0;
}
```

这是一个简单的 Hello World 程序。我们如何使它变为一份二进制可执行文件呢？

在 Windows 或 Mac OS X 这样带 GUI 的系统上，通过安装 IDE，我们可以使用 IDE 中的编译功能来编译出目标。 实际上，这些带有图形界面的 IDE 的编译往往是封装了各种提供命令行接口的编译器。 自然，在众多无 GUI 的 Linux 上，我们同样可以调用这些提供命令行接口的编译器进行编译。

各平台常见编译器

Linux 上常用的编译器是 gcc 和 clang。 其中 gcc 是由 GNU 组织维护的，而 clang 是由 LLVM 组织维护的。

Windows 上常见的编译器则是 cl.exe，由微软维护。著名的 Visual C++ (MSVC) 即使用了 cl.exe。

Mac OS X 本身由 BSD 发展而来，也以 gcc 和 clang 为主。 值得一提的是，Mac OS X 上自带的 gcc 其实是 clang 的别名，在 Terminal 输入 `gcc -v` 即可发现。

这里我们使用 gcc 对这个文件进行编译，生成二进制文件：

```js
$ gcc main.c -o main
$ ./main
Hello World!
```

这里用 `-o` 指定了输出的二进制文件的文件名 `main` 。

应当注意到 `gcc main.c -o main` 这条指令没有打印出任何内容。 这是因为整个编译过程是成功的，gcc 没有需要报告的内容，因此保持沉默。 这是 Unix 哲学的一部分： *Rule of Silence: When a program has nothing surprising to say, it should say nothing.*[^1]

### 多文件的状况

只在一个文件中编写代码，对于稍微大的开发都是不够的： 对于个人维护的小项目尚可，但当你面临的是一个多人开发、模块复杂、功能繁多的大项目时（无论是在公司工程还是在实验室科研中，这都是普遍的情况）， 拆分代码到多个文件才是一个明智（或者说可行）的做法。

C 语言的多文件实现

我们假设你对于 C 语言的多文件实现有着基本的认知： 即能够在之前的系统中的 IDE 内完成 C 语言的多文件开发。

如果你不会，别急，这里将做一个简单的介绍：

假设你拥有一下两个文件：

```js
// main.c
#include "print.h"

int main() {
  print();
  return 0;
}
```
```js
// print.c
#include "print.h"

#include <stdio.h>

void print() {
  printf("Hello World!\n");
}
```

那为了在 main.c 中调用 `void print()` 这个函数，你需要做以下几件事：

- 在当前目录下新建一个头文件 print.h；
- 在 print.h 中填入以下内容：
```js
// print.h
#ifndef PRINT
#define PRINT

void print();

#endif  // PRINT
```

这里的 `#ifndef ... #define ... #endif` 是头文件保护，防止同一头文件被 `#include` 两次造成重复声明的错误， 如果你不理解这部分也没关系，只需保证 `void print();` 这一行声明存在即可。

- 在 main.c 和 print.c 中同时 `#include "print.h"` 。

这样，程序就可以被编译运行了。

假设我们有以下三个文件：

```js
// main.c
#include "print.h"

int main() {
  print();
  return 0;
}
```
```js
// print.c
#include <stdio.h>

void print() {
  printf("Hello World!\n");
}
```
```js
// print.h
#ifndef PRINT
#define PRINT

void print();

#endif  // PRINT
```

我们将依次编译链接，生成目标的二进制可执行程序。让我们看一下命令：

```js
$ gcc main.c -c  # 生成 main.o
$ gcc print.c -c  # 生成 print.o
$ gcc main.o print.o -o main
$ ./main
Hello World!
```

这里我们使用了 `gcc -c` 。 `-c` 会将源文件编译为对象文件（Object file，.o 这一后缀就源自单词 object 的首字母）。 对象文件是二进制文件，不过它不可执行，因为其中需要引用外部代码的地方，是用占位数替代的，无法真正调用函数。

注意到我们没有添加 `-o` 选项，因为 `-c` 存在时 gcc 总会生成相同文件名（这里特指 basename，main.c 中的 main 部分）的.o 对象文件。

生成了对象文件后，我们来进行链接，在相应函数调用的位置填上函数真正的地址，从而生成二进制可执行文件。 `gcc` 这一指令会根据输入文件的类型调用相应的程序完成整个编译流程。 在这里，虽然同样是 gcc 指令，但是由于输入的为.o 文件，gcc 将调用链接器进行链接，从而生成最终的可执行文件。

同样是这个原因，实际上使用 `gcc main.c print.c -o main` 是可以一步到位，但在接下来的内容里，你会看到另一个方案。

gcc 的四个部分，编译的过程

gcc 的编译其实是四个过程的集合，分别是预处理（preprocessing）、编译（compilation）、汇编（assembly）、链接（linking）， 分别由 cpp、cc1、as、ld 这四个程序完成，gcc 是它们的封装。

这四个过程分别完成：处理 `#` 开头的预编译指令、将源码编译为汇编代码、将汇编代码编译为二进制代码、组合众多二进制代码生成可执行文件， 也可分别调用 `gcc -E` 、 `gcc -S` 、 `gcc -c` 、 `gcc` 来完成。

在这一过程中，文件经历了如下变化： `main.c` 到 `main.i` 到 `main.s` 到 `main.o` 到 `main` 。

### 使用构建工具（Build tools）

上述方法在源文件较少时是比较方便的，但当我们面对的是数以千计万计的源文件（同样的，在工作或科研中这也是常见状况），我们将面临以下困难：

- 手动地一一编译实在太麻烦，太浪费精力；
- 这些源文件的编译有顺序要求，为了满足此依赖关系需要设计一个流程；
- 编译整个项目需要难以忍受的大量时间，应当考虑到一部分未更改的源文件不需要重新编译。

为了让机器帮助程序员解决这些困难，构建工具应运而生。 同样的，由于需求巨大，构建工具在 Linux 上亦获得了强力支持。

#### Makefile

Makefile 是中小型项目常用的构建工具。 让我们考虑以下例子：

假设前述 3 份源文件已存在在当前目录下。 创建以下内容的文件，并命名为 `Makefile` ：

```js
main.o: main.c print.h
print.o: print.c print.h
main: main.o print.o
```

然后在当前目录下执行：

```js
$ make main
$ ./main
Hello World!
```

为了解释这一过程，我们来分析一下 Makefile 的内容。其中：

```js
main.o: main.c print.h
```

这一行，通过冒号分割，指定了一个名为 `main.o` 的目标，其依赖为 `main.c` 和 `print.h` 。 由于整个文件中没有名为 `main.c` 的目标，所以 Makefile 会认为对应的 `main.c` 文件为一个依赖， `print.h` 同理。

在指定了目标和依赖后，紧接着的下一行如果用 **Tab** 缩进，则可以指定利用依赖获得目标的指令。 例如：

```js
main.o: main.c print.h
    gcc main.c -c  # 一定要用 Tab 缩进而不是 4 个 / 2 个空格——这是历史遗留问题。
```

以上内容表示如果要获得 `main.o` 这个目标，则会执行 `gcc main.c -c` 这个指令。 如果没有指定命令，Makefile 会尝试从文件后缀等处获取信息，推测你需要的指令。 例如此处即使不显式写出指令，Makefile 也知道用 gcc 来完成编译。

最终我们在 shell 中执行 `make main` ，正是指定了一个最终目标。 如果不提供这个目标，Makefile 则会选择 Makefile 文件中第一目标。 为了获得最终目标，Makefile 会递归地获取依赖、执行指令。

Makefile 的亮点在于引入了文件间的依赖关系。 在使用它进行构建时，Makefile 可以根据文件间的依赖关系和文件更新时间，找出需要重新编译的文件。 在项目较大时这能明显节省构建所需的时间，同时也能解决一些由于编译链接顺序造成的问题。 相较与输入一大串指令，单个的 `make [target]` 甚至是仅仅 `make` ，也更加优雅和方便。

小知识

在 Makefile 中有一些隐含规则。即使我们的 Makefile 中没有显式书写这样的规则，make 也会按照这些隐含规则来运行。 例如，上文提到的自动将 `.c` 文件编译成 `.o` 就是一种隐含规则。

除此之外，Makefile 中还有如下隐含规则：

- `filename.o` 的依赖会自动推导为 `filename.c`
- `filename` 的依赖会自动推导为 `filename.o`

利用这两条隐含规则，我们的 Makefile 还可进一步化简成：

```js
main.o: print.h
print.o: print.h
main: print.o
```

#### 其他的构建工具：CMake，ninja……

一个更大的工程可能有上万、上十万份源文件，如果一一写进 Makefile，那依然会异常痛苦，且几乎不可能维护。

为了更好的构建程序，大家想出了“套娃”的办法：用一个程序来生成构建所需的配置，CMake 则在这一想法下诞生。

CMake 在默认情况下，可以通过 `cmake` 命令生成 Makefile，再进一步进行 `make` 。

对于 CMake 的讲解已经超出了本课程的讲解范围。 CMake 作为一个足够成熟、也足够陈旧的工具，既有历史遗留问题，也有新时代下的新思路。 正如 C++ 和 Modern C++，CMake 也有 Modern CMake，更有像微软 vcpkg 那样新的辅助工具和解决方案。 如果你想了解 CMake 的一些知识，附录将会有简单的介绍，亦可以考虑看一些较新的、关于 Modern CMake 的博客，以及官方的最新文档。

另一个值得一提的是 ninja。ninja 和 Makefile、autoconf 较类似，是构建工具，所属抽象层次低于 CMake。 ninja 的特点的是相较与 Makefile 更快，对于多线程编译的支持更好。 详细信息可以到 ninja 的官方网站查看。

### 至于 C++

C++ 的工具链与 C 的是相似的。

实际上，只需将上面内容中的 `gcc` 指令改为 `g++` ，你就能同样地完成 C++ 的开发。 gcc 这一编译器本身即支持多种编程语言，包括了 C、C++、Objective C 等。 其他编译器如 clang 也会提供 `clang++` 这样的指令完成 C++ 的编译。 Makefile、CMake 这样的构建工具亦可以用于多种编程语言。

### 总结

在 Linux 下，大多编程语言都会提供一套适合命令行的、简单便捷的工具链。 善于运用这些工具，能够极大地提升你的开发效率，支持你完成自己的项目。

## Python 语言开发

Python 作为一门年长但恰逢新春的解释型语言，亦被业界广泛使用。 相较于 Windows，在 Linux 上开发 Python 要更加简单。

针对 Python 的介绍，我们将不会着力于具体代码，而是分析其一些外围架构，从而引出总结。

### 解释器 python

一般的 Python（CPython）程序的运行，依靠的是 Python 解释器（Interpreter）。 在 Python 解释器中，Python 代码首先被处理成一种字节码（Bytecode，与 JVM 运行的字节码不是一个东西，但有相似之处）， 然后再交由 PVM（Python virtual machine）进行执行，从而实现跨平台和动态等特性。

由于使用过于广泛，几乎每一份 Linux 都带有 Python 解释器，以命令 `python2` 或 `python3` 调用，分别对应两个版本的 Python。

### 包管理器 pip

为使用外部的第三方包，Python 提供了一个包管理器：pip。

pip 和 apt 之类的包管理器有相似之处：完成包的安装和管理，完成依赖的分析，等等。 不过 pip 管理的是 Python 包，可以在 Python 代码中使用这些包。让我们看下面的例子：

```js
# 安装 Python 3 和 Python 3 的 pip。对于 Python 2 和 3 间的纠纠缠缠，我们将在之后讲解。
$ sudo apt install python3 python3-pip

# 测试一下看看，是否能够正常使用它们。
# 请保证在 \`python\` 和 \`pip\` 后有 3 这个数字。这也是历史遗留问题。
$ python3 -V
$ pip3 -V

# 暂时忽略以下两条指令，我们会在之后讲解。
$ python3 -m venv venv
$ source venv/bin/activate
(venv)$ ls
venv

# 安装一个 Python 包 a、b，以及 a、b 依赖的 Python 包。
(venv)$ pip3 install a b

# 卸载一个 Python 包 b。注意：这不会删除之前一起安装的包 b 的依赖。
(venv)$ pip3 uninstall b
```

安装了 a 之后，我们就能在代码中使用 a 这个包了。

```js
# main.py
import a

print(a)
```
```js
(venv)$ python3 main.py
<module 'a' from '...'>
```

这样，我们就完成了对外部 Python 包的安装和引用。

### Python 依赖管理

一个软件一般含有众多依赖，尤其是对于追求易用、外部库众多的 Python 而言，使用外部库作为依赖是常事。

此处我们将尝试给出各种使用较多的 Python 依赖管理方案。

#### requirements.txt

在一些项目下，你可能会发现一个名为 `requirement.txt` 的文件，里面是一行行的 Python 包名和一些对于软件版本的限制，例如：

```js
# requirements.txt
django
pytest>=3.0.0
pytest-cov==1.0.0
```

为了安装这些 Python 包，使用以下指令：

```js
$ pip3 install -r requirements.txt
```

这将从 `requirements.txt` 文件中逐行读取包名和版本限制，并由 pip 完成安装。

此方案简单明了，易于使用，但对于依赖的处理能力不足。

#### setuptools: setup.py

在 PyPI，即 pip 获取 Python 包的来源中，使用 setuptools 是主流选择。 setuptools 不是 Python 官方的项目，但它已成为 Python 打包（packaging）的事实标准。

常见状况是目录下会有一个名为 `setup.py` 的文件。 要安装依赖，只需：

```js
$ ls
setup.py
$ pip3 install .
```

这种方案特点是使用广泛，易于对接，能提供的信息和配置较全，但配置起来也较复杂。

#### 其他的：pip-tools、pipenv……

pip-tools 可以看作对 requirements.txt 的增强。 它额外提供了 `requirements.dev` 文件，从而完成了对于依赖进行版本锁定的支持。

pipenv 则是一个更加全面的解决方案，它提供了类似于 npm 的配置文件和 lock 文件，对于依赖有非常强的管理功能。 但其完成度和工业中的稳定性尚有待证明。

Python 有非常多的依赖管理方案，某种意义上讲是自带的 pip 管理功能不足所造成的。 一般而言，只需熟悉常用的 requirements.txt 和 setuptools 方案即可。

### Virtualenv

让我们考虑以下情况：

Python 通过包管理器如 apt 安装的包，默认安装在系统目录 `/usr/lib/python[version]` 下， 而通过 pip 安装的包，默认安装目录在 `/usr/local/lib/python[version]` 下， 当通过 pip 安装时显式传入了一个 `--user` 选项时，则会安装在用户目录 `~/.local/lib/python[version]` 下， 另外，在普通用户下直接执行 pip install 而没有传入 `--user` 选项时，也会因为用户没有系统目录的写权限而安装到用户目录。 当普通地运行 Python 解释器时，这几个目录下的包均可见。

现在假设用户目录下已有一个包 `a` ，版本为 `1.0.0` 。 现在我们需要开发一个程序，也需要包 `a` ，但要求版本大于 `2.0.0` 。

由于 pip 不允许同时安装不同版本的同一个包，当你运行 `pip3 install a>=2.0.0` 时，pip 会更新 `a` 到 `2.0.0` ， 那原先依赖于 `a==1.0.0` 的软件就无法正常运行了。

注意 `>=`

在一些 Shell（如 zsh）中， `>=` 有特殊含义。 此时上述命令应用引号包裹 `>=` 部分，如 `pip3 install 'a>=2.0.0'`

为了解决这一问题，允许不同软件使用不同版本的包，Python 提供了 Virtualenv 这个工具。 其使用方法如下：

一般 Virtualenv 会带在默认安装的 Python 中。 如果没有，可以用 `sudo apt install python3-venv` 来安装。

常见的做法是使用 Python 的模块运行来完成在 Shell 中的执行：

```js
$ python3 -m venv venv
```

以上指令中， `-m` 表示运行一个指定的模块，前一个 `venv` 指运行 venv 这个包的主模块 `__main__` ， 后一个 `venv` 是参数，为生成目录的路径。 这将使 venv 在当前目录下生成一个名为 `venv` 的目录。

在一般的 shell 环境下，我们将使用 `source venv/bin/activate` 来启用这个 venv。

完成以上操作后，你就进入了当前目录下 venv 文件夹所对应的 Virtualenv。 此时，你使用 `pip3 install` 安装的 Python 包将会被安装在 venv 这个文件夹中， 这些包也只有在你 `source venv/bin/activate` 之后才可见，外部无法找到这些包。 通过 `deactivate` 可以退出 Virtualenv，回到之前的环境中。

实际上，由于 Python 是借助一些环境变量来完成包搜索的步骤的， `source venv/bin/activate` 其实是配置了一些环境变量，从而达到目的。这样，就实现了程序间依赖的隔离。

### Python 的版本

正如我们之前所讲，Python 不是一个新的编程语言。 现在的 Python，最新的版本已到 3.14（截至 2025 年 9 月）。 实际上还在使用中的 Python 版本，主要在 3.9 以上。

Python 2 到 3 某种程度上讲不是变革，实际上 Python 2 和 3 基本可以看作两个不同的编程语言。 在从 2 到 3 的升级中，一方面众多底层语法都发生了改变，使得迁移异常麻烦。 另一方面，由于 Python 2 的盛行，程序 `python` 普遍指向 `python2` 。 因此当 Python 3 出现时，为了有效区分两者，调用解释器时我们需要特地使用 `python3` 这一指令。 尽管在某些平台（例如 Arch 系 Linux）上， `python` 己经变为指向 `python3` ， 但考虑到 Ubuntu、CentOS、Debian 等发行版上 `python` 有可能仍指向 `python2` ， 显式地指定一个版本是更明智的选择。

实际上，Python 2 已在 2020 年初正式宣告停止维护， 现在如果我们要使用 Python，最好使用 3 版本。

而在 Python 3.x 版本中，截至 2025 年下半年，3.9 亦已经 EOL（end of life）。

我应该选择哪个版本的 Python？

Python 3.x 已经迭代到一个相对稳定的阶段，如果你没有特殊需求，请使用 Python 3.x 的最新版本。

截止到 2025 年 9 月，我们推荐 Python 3.14。(或者使用系统自带的版本)

你可以在 [Status of Python versions](https://devguide.python.org/versions/) 查看 Python 各个版本的状态。

Python 的生命支持周期

Python 的每个主版本分支都遵循一个固定的生命支持周期，以确保语言的稳定性和持续发展。

根据 Python 官方的规定，自 Python 3.9 开始，从每个 Python 3.X.0 版本发布起，Python 3.X 系列享有为期 5 年的支持。 这 5 年的生命支持周期分为以下几个阶段：

1. **错误修复支持 / 完整支持 (Bugfix / Full Support)** ： 从正式发布开始，该版本将获得全面的支持，包括接收错误修复和安全补丁。这个阶段通常持续 **2 年** 。 在此期间，大约每隔一个月会发布新的二进制文件。
2. **安全修复支持 (Security Support)** ： 在错误修复支持阶段结束后，该版本将进入为期 **3 年** 的安全修复阶段。 在此期间，将不再发布任何二进制文件，仅提供源代码形式的安全补丁。
3. **生命周期结束 (End-of-Life, EOL)** ： 在发布 5 年后，该版本的支持将正式结束。 届时，该版本将不再接收任何更改，包括安全修复，使用这些版本的项目将面临安全风险。

你可以在 [PEP 602](https://peps.python.org/pep-0602/) 查看详细的有关 Python 的生命支持周期的规定。

### Python 的其他实现

Python 作为一门编程语言，官方的实现是 CPython，我们一般使用的、成为事实标准的就是这个。 CPython 中的 C 是指此解释器是用 C 实现。

相应的，Python 还有其他的一些实现：

- JPython：将 Python 编译到 Java 字节码，由 JVM 来运行；
- PyPy：相较于 CPython，实现了 JIT（just in time）编译器，性能有极大地提升；
- Cython：引入了额外的语法和严密的类型系统，性能也有很大提升；
- Numba：将 Python 编译到机器码，从而直接运行，性能也不错。

视情况使用不同的 Python 实现能够很大程度地提升性能。 但如果你不确定自己的意向，且性能需求不大，使用官方的 CPython 也是明智之选。

### 总结

外部包引用和依赖管理是程序开发中必不可少的部分。 如果官方有成熟的方案，跟随他们是明智的选择。 否则则需根据实际情况，按需选用。

## 思考题

试试 Rust

Rust 是一门新兴编译型编程语言。 尝试查询 Rust 的文档，指出 Rust 的编译器、依赖管理程序， 介绍一下如何将 Rust 源码变为可执行程序，如何在 Rust 中引用外部包。

## 引用来源

---

[^1]: [Basics of the Unix Philosophy](https://homepage.cs.uri.edu/~thenry/resources/unix_art/ch01s06.html)
[跳转至](https://101.lug.ustc.edu.cn/Ch07/supplement/#supplement)

## 拓展阅读

## Python 环境的另一种管理方式：Conda

Conda 是一个广泛使用的开源的包管理与环境管理系统。Miniconda 与 Anaconda 是两个广为人知的基于 Conda 的 Python 的发行版本。

### Anaconda 与 Miniconda

Miniconda 和 Anaconda 都是开源的 Python 的发行版本。

Miniconda 是 Anaconda 的免费迷你版本，只包含了 Conda、Python 及其依赖，以及少量其他有用的包，例如 pip 和 zlib。而 Anaconda 则额外包含了 250 多个自动安装的科学软件包，例如 SciPy 和 NumPy，并且测试了这些软件包之间的兼容性。Anaconda 分为个人版、商业版、团队版、企业版，除了个人版以外，其余版本均为付费产品。

### 安装 Miniconda

从官网下载安装 Miniconda，并进入虚拟环境。

```js
$ sh -c "$(wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O -)"

# 前面的选项可以保持默认，也可以自行修改
please answer 'yes' or 'no':
>>> yes
# 选择 Miniconda 的安装路径
Miniconda3 will now be installed into this location:
>>> ~/.miniconda3
# 添加配置信息到 ~/.bashrc 文件，这样每次打开终端时会自动激活虚拟环境
Do you wish the installer to initialize Miniconda3 by running conda init? [yes|no]
[no] >>> yes

$ source ~/.bashrc # 应用配置文件信息，激活虚拟环境
```

### Conda 作为包管理器

类似于 pip，可以使用 `conda install` 来安装软件包。部分软件包既可以使用 pip 安装，也可以使用 conda 安装。 相比于 pip，conda 会执行更加严格的依赖检查，并且除了 Python 软件包外，还可以安装一些 C/C++ 软件包，例如 cudatoolkit、mkl 等。相对的，conda 支持的 Python 软件包的数量远少于 PyPI。

### Conda 作为环境管理器

类似于 Virtualenv，可以使用 conda 来管理虚拟环境。

常见的使用方式如下：

```js
$ conda create -n venv python=3.11 # 创建一个名为 venv，Python 版本为 3.11 的虚拟环境
# 请确认虚拟环境已经成功创建
$ conda activate venv # 切换到名为 venv 的虚拟环境
$ conda deactivate # 退出当前虚拟环境
```

### 导出导入环境

在一些 Python 项目中，你能找到一个 `environment.yml` 文件。 此文件类似于 `requirements.txt` ，是 Conda 用以描述环境配置的文件。 你可以利用此文件来分享或复制环境，从而运行其他人的项目。

`environment.yml` 文件不会自动生成。 为了获取当前环境所对应的 `environment.yml` 文件，你需要使用以下命令：

```js
$ conda env export > environment.yml
```

此文件会包含当前环境下所有已装包的版本信息以便复现。 如果你只需要导出明确由用户自己安装的包、而不包含这些包的依赖，可以使用 `--from-history` 选项。

通过 `environment.yml` 文件，你可以使用以下命令来复现环境：

```js
$ conda env create -f environment.yml
```

复现出的环境的名字与原环境相同、由 `environment.yml` 文件的 `name` 字段传递。 相似的，环境的存放位置由 `prefix` 字段传递。

由 pip 安装的包

使用 `--from-history` 选项时，由 pip 安装的包不会被包含在 `environment.yml` 文件中。 而在不使用此选项的一般情况下，由 pip 安装的包会被记录在 `environment.yml` 文件中的 `pip` 列表内，因而可以被复现。

## 动态链接与静态链接

在大部分情况下，我们编译的程序都是动态链接的。动态链接在这里指程序文件还依赖其他库文件，可以使用 `ldd` 命令确认：

```js
$ cat hello.c
#include <stdio.h>

int main() {
    puts("Hello, world!");
    return 0;
}
$ gcc -o hello hello.c
$ ldd ./hello
    linux-vdso.so.1 (0x00007ffc49703000)
    libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007f36767d3000)
    /lib64/ld-linux-x86-64.so.2 (0x00007f36769ea000)
```

这里，我们编译得到程序就依赖于 `linux-vdso.so.1` 、 `libc.so.6` 和 `/lib64/ld-linux-x86-64.so.2` 三个库文件，如果系统中没有这三个库文件，程序就无法执行。

这三个文件的用途

可以看到，即使是 Hello, world 这么简单的程序，也需要外部库文件。

- linux-vdso.so.1：这个库是为了减小用户程序调用系统调用产生的切换模式（用户态 -> 内核态 -> 用户态）的开销而设计的。这个文件事实上并不存在。在内核加载程序时，这一部分会被自动加载入程序内存中。详情可参考 vdso(7) 文档。
- libc.so.6：C 运行时库，提供各种 C 函数的实现。
- ld-linux-x86-64.so.2：动态链接加载器。当程序需要动态链接库中的函数时负责查找并加载对应的函数。

我们在编写程序时，有时需要使用到第三方的库，此时需要加上 `-l` 参数指定在 **链接** 时链接到的库。

```js
$ gcc -o thread thread.c -lpthread  # 编译一个依赖于 pthread 线程库的应用
$ ldd ./thread  # 可以看到多出了 libpthread.so.0 的动态链接依赖
    linux-vdso.so.1 (0x00007ffe6ad93000)
    libpthread.so.0 => /lib/x86_64-linux-gnu/libpthread.so.0 (0x00007fad173c7000)
    libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007fad171d5000)
    /lib64/ld-linux-x86-64.so.2 (0x00007fad17407000)
```

对于复杂的应用来说，下载后可能会因为没有动态链接库而无法运行。这一点在打包、分发自己编写的程序时也要特别注意。

而静态链接则将依赖的库全部打包到程序文件中。

```js
$ gcc -o hello-static hello.c -static  # 编译一个静态链接的应用
$ ldd ./hello-static  # 没有动态链接库的依赖
    not a dynamic executable
```

此时编译得到的程序文件没有额外的依赖，在其他机器上一般也能顺利运行。近年来流行的 Go 语言的一大特点也是静态链接，编译得到的程序有着很好的兼容性。

但是静态链接也存在一些问题。首先是程序大小，比较一下前面编译的 hello-static 和 hello 的大小吧：

```js
$ ls -l hello hello-static
-rwxrwxr-x 1 ustc ustc  17K Feb 28 14:43 hello
-rwxrwxr-x 1 ustc ustc 852K Feb 28 14:39 hello-static
```

可以看到，动态链接的程序比较小，而静态链接的程序大小接近 1M，况且这还只是一个最简单的 hello world！并且在大小方面，静态链接的程序在运行时无法共享运行库的内存，从而导致内存占用也有一定程度增加。

其次，当运行库出现问题时，用户可以选择更新库，此时所有动态链接的程序都能得到修复，但是静态链接的程序由于不使用系统库，就不得不一个个重新编译。

最后一点是，Linux 的默认 C 库 glibc 对静态链接并不友好，如果程序使用了一部分函数，在静态链接时会受到限制。

Musl libc

近年来，musl libc 开始流行，并且它也是 Alpine Linux 的 C 运行时库。它的特点是轻量、快速、对静态链接友好。我们也可以来试一下：

```js
$ sudo apt install musl-tools  # musl-tools 提供了 musl-gcc 等方便的编译工具
$ musl-gcc -o hello-static-musl hello.c -static  # 静态链接 musl libc
$ ls -lha hello hello-static hello-static-musl
-rwxrwxr-x 1 ustc ustc  17K Feb 28 14:43 hello
-rwxrwxr-x 1 ustc ustc 852K Feb 28 14:39 hello-static
-rwxrwxr-x 1 ustc ustc  26K Feb 28 15:00 hello-static-musl
$ # 可以看到静态链接 musl 得到的文件与动态链接接近，并且远小于静态链接 glibc 得到的文件。
$ musl-gcc -o getaddrinfo-example-musl getaddrinfo.c -static
$ # musl libc 的 getaddrinfo() 实现不依赖于额外的系统组件，所以可以正常静态链接
```

## 交叉编译示例

有时候，我们需要为其他的平台编写程序，例如：

- 我正在使用的电脑是 x86\_64 架构的，但是我现在需要给树莓派编写程序（体系结构不同）。
- 我正在使用 Linux，但是我现在需要编译出一个 Windows 程序（操作系统不同）。

怎么办呢？只能用虚拟化程序运行目标架构，然后在上面跑编译了吗？这样会很麻烦、速度可能会很慢，甚至有的时候不可行（例如性能低下的嵌入式设备，可能连编译器都加载不了）。

这时候就需要交叉编译了。对于常见的架构，Ubuntu/Debian 提供了对应的交叉编译器，很大程度方便了使用。以下将给出交叉编译简单的示例。

### 在 x86\_64 架构编译 aarch64 的程序

Aarch64 是 ARM 指令集的 64 位架构。

### 在 Linux 下编译 Windows 程序

这里使用 mingw 来进行交叉编译。

```js
$ sudo apt install gcc-mingw-w64  # 安装 mingw 交叉编译器
$ sudo apt install wine  # 安装 wine Windows 兼容层（默认仅安装 64 位架构支持）
$ x86_64-w64-mingw32-gcc -o hello.exe hello.c  # 编译为 64 位的 Windows 程序
$ file hello.exe  # 确认为 Windows 程序
hello.exe: PE32+ executable (console) x86-64, for MS Windows
$ wine hello.exe  # 使用 wine 运行
it looks like wine32 is missing, you should install it.
as root, please execute "apt-get install wine32"
wine: created the configuration directory '/home/ubuntu/.wine'
（忽略首次配置的输出）
wine: configuration in L"/home/ubuntu/.wine" has been updated.
Hello, world!
```

MinGW 也可以编译 Windows 下的图形界面应用程序。以下的程序例子来自 [Windows Hello World Sample](https://docs.microsoft.com/en-us/windows/win32/learnwin32/windows-hello-world-sample) （MIT License），稍作修改以符合 C 语言的语法。

```js
// winhello.c
#ifndef UNICODE
#define UNICODE
#endif

#include <windows.h>

LRESULT CALLBACK WindowProc(HWND hwnd, UINT uMsg, WPARAM wParam, LPARAM lParam);

int WINAPI wWinMain(HINSTANCE hInstance, HINSTANCE _, PWSTR pCmdLine, int nCmdShow)
{

    // Register the window class.
    const wchar_t CLASS_NAME[]  = L"Sample Window Class";

    WNDCLASS wc = { };

    wc.lpfnWndProc   = WindowProc;
    wc.hInstance     = hInstance;
    wc.lpszClassName = CLASS_NAME;

    RegisterClass(&wc);

    // Create the window.

    HWND hwnd = CreateWindowEx(
        0,                              // Optional window styles.
        CLASS_NAME,                     // Window class
        L"Learn to Program Windows",    // Window text
        WS_OVERLAPPEDWINDOW,            // Window style

        // Size and position
        CW_USEDEFAULT, CW_USEDEFAULT, CW_USEDEFAULT, CW_USEDEFAULT,

        NULL,       // Parent window
        NULL,       // Menu
        hInstance,  // Instance handle
        NULL        // Additional application data
        );

    if (hwnd == NULL)
    {
        return 0;
    }

    ShowWindow(hwnd, nCmdShow);

    // Run the message loop.
    MSG msg = { };
    while (GetMessage(&msg, NULL, 0, 0))
    {
        TranslateMessage(&msg);
        DispatchMessage(&msg);
    }

    return 0;
}

LRESULT CALLBACK WindowProc(HWND hwnd, UINT uMsg, WPARAM wParam, LPARAM lParam)
{
    switch (uMsg)
    {
    case WM_DESTROY:
        PostQuitMessage(0);
        return 0;

    case WM_PAINT:
        {
            PAINTSTRUCT ps;
            HDC hdc = BeginPaint(hwnd, &ps);

            // All painting occurs here, between BeginPaint and EndPaint.
            FillRect(hdc, &ps.rcPaint, (HBRUSH) (COLOR_WINDOW+1));
            EndPaint(hwnd, &ps);
        }
        return 0;
    }

    return DefWindowProc(hwnd, uMsg, wParam, lParam);
}
```
```js
$ x86_64-w64-mingw32-gcc -o winhello.exe winhello.c
/usr/bin/x86_64-w64-mingw32-ld: /usr/lib/gcc/x86_64-w64-mingw32/9.3-win32/../../../../x86_64-w64-mingw32/lib/libmingw32.a(lib64_libmingw32_a-crt0_c.o): in function \`main':
./build/x86_64-w64-mingw32-x86_64-w64-mingw32-crt/./mingw-w64-crt/crt/crt0_c.c:18: undefined reference to \`WinMain'
collect2: error: ld returned 1 exit status
$ # 编译失败，这是因为编译 Windows Unicode（UTF-16）程序需要额外的参数 -municode。
$ # 参见 https://sourceforge.net/p/mingw-w64/wiki2/Unicode%20apps/
$ x86_64-w64-mingw32-gcc -o winhello.exe winhello.c -municode
$ wine winhello.exe  # 需要在图形界面下执行，或者复制到 Windows 中执行亦可
```