### Makefile 笔记

```
Makefile 是一个编辑脚本，指定了项目中哪些文件需要编译，文件的依赖关系及最终编辑的目标产物。
```

#### 基本语法：

```
target: depend
    command
    ...
```

- target 就是目标产物
- depend 生成 target 需要依赖 depend.
- command depend 如何生成 target 的命令

#### 一个简单地示例，来解释一下语法

```
.PHONY: clean
CC = gcc
RM = rm
EXE = demo
CFLAGS+=-c -Wall -g
SRCS = $(wildcard *.c)
OBJS = $(patsubst %.c, %.o, $(SRCS))
all:$(EXE)
	$(RUN) ./$(EXE)

$(EXE):$(OBJS)
	$(CC) $^ -o $@

%.o:%.c
	$(CC) $^ $(CFLAGS) -o $@

clean:
	$(RM) $(EXE) $(OBJS)
```

1. `.PHONY: clean`
   用`.PHONY`声明了`clean`后，Makefile 会把`clean`当做文本处理，不会当成工程下的文件或文件夹。
   我们不用`.PHONY`去声明`clean`，Makefile 会把`clean`当做文件或文件夹处理，那么我们 Makefile 中的`clean`命令将不会执行。
2. `CC = gcc`
   是声明变量，我们声明了变量后，如何使用？eg:`$(CC)`，这样就可以使用了。
3. `CFLAGS+=`
   `CFLAGS`是 make 的内置变量，这里用到了`+=`，意思就是保留`CFLAGS`的默认配置项，再加上我们自己的配置项
4. `SRCS = $(wildcard *.c)`
   声明`SRCS`变量，用`wildcard`这个函数给`SRCS`变量赋值。这句话的意思就是：取当前目录下`.c`文件赋值给`SRCS`
5. `OBJS = $(patsubst %.c, %.o, $(SRCS))`
   这句话的意思就是：取`SRCS`中的`.c`，替换成`.o`（到这里都是代表字符串，是不是文件）
6. `all:$(EXE)`
   `all`和`clean`一样都是命令，区别就是：`all` 是内置的，`clean`是我们自己定义的。解释一下这个命令`all:$(EXE)`：按照 Makefile 基本语法，`all`是我们要的目标，但是`all`又是依赖`$(EXE)`。很明显当前是没有`$(EXE)`这个可执行文件的，那么就要向下找，直到找到生成`$(EXE)`的地方。`$(RUN) ./$(EXE)`这条命令是执行`$(EXE)`的，不会生成`$(EXE)`，所以要继续向下寻找。
7. `$(EXE):$(OBJS)`
   生成目标`$(EXE)`依赖于`$(OBJS)`。还是按照老套路向下寻找依赖关系：执行`$(CC) $^ -o $@`。 `$^`:指的是向上依赖`$(OBJS)`，也就是`$^`是等价于`$(OBJS)`，是当前项目的所有`.o`文件；`$@`:是生成对应的文件，这里指的是生成`$(EXE)`
8. `%.o:%.c`
   `%`是通配符，生成目标`%.o`依赖于`%.c`。向下寻找依赖关系：`$(CC) $^ -o $@`，`$@`:是生成对应的文件，这里指的是生成`%.o`；eg: `a.c -> a.o   b.c -> b.o ...`

至此这个 Makefile 解释完毕。
