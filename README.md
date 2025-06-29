# README

> [Linux 0.11](https://elixir.bootlin.com/linux/0.11/source)
>
> ```shell
> .
> ├── boot
> │   ├── bootsect.s
> │   ├── head.s
> │   └── setup.s
> ├── fs
> │   ├── bitmap.c
> │   ├── block_dev.c
> │   ├── buffer.c
> │   ├── char_dev.c
> │   ├── exec.c
> │   ├── fcntl.c
> │   ├── file_dev.c
> │   ├── file_table.c
> │   ├── inode.c
> │   ├── ioctl.c
> │   ├── Makefile
> │   ├── namei.c
> │   ├── open.c
> │   ├── pipe.c
> │   ├── read_write.c
> │   ├── stat.c
> │   ├── super.c
> │   └── truncate.c
> ├── include
> │   ├── a.out.h
> │   ├── asm
> │   │   ├── io.h
> │   │   ├── memory.h
> │   │   ├── segment.h
> │   │   └── system.h
> │   ├── const.h
> │   ├── ctype.h
> │   ├── errno.h
> │   ├── fcntl.h
> │   ├── linux
> │   │   ├── config.h
> │   │   ├── fdreg.h
> │   │   ├── fs.h
> │   │   ├── hdreg.h
> │   │   ├── head.h
> │   │   ├── kernel.h
> │   │   ├── mm.h
> │   │   ├── sched.h
> │   │   ├── sys.h
> │   │   └── tty.h
> │   ├── signal.h
> │   ├── stdarg.h
> │   ├── stddef.h
> │   ├── string.h
> │   ├── sys
> │   │   ├── stat.h
> │   │   ├── times.h
> │   │   ├── types.h
> │   │   ├── utsname.h
> │   │   └── wait.h
> │   ├── termios.h
> │   ├── time.h
> │   ├── unistd.h
> │   └── utime.h
> ├── init
> │   └── main.c
> ├── kernel
> │   ├── asm.s
> │   ├── blk_drv
> │   │   ├── blk.h
> │   │   ├── floppy.c
> │   │   ├── hd.c
> │   │   ├── ll_rw_blk.c
> │   │   ├── Makefile
> │   │   └── ramdisk.c
> │   ├── chr_drv
> │   │   ├── console.c
> │   │   ├── keyboard.S
> │   │   ├── Makefile
> │   │   ├── rs_io.s
> │   │   ├── serial.c
> │   │   ├── tty_io.c
> │   │   └── tty_ioctl.c
> │   ├── exit.c
> │   ├── fork.c
> │   ├── Makefile
> │   ├── math
> │   │   ├── Makefile
> │   │   └── math_emulate.c
> │   ├── mktime.c
> │   ├── panic.c
> │   ├── printk.c
> │   ├── sched.c
> │   ├── signal.c
> │   ├── sys.c
> │   ├── system_call.s
> │   ├── traps.c
> │   └── vsprintf.c
> ├── lib
> │   ├── close.c
> │   ├── ctype.c
> │   ├── dup.c
> │   ├── errno.c
> │   ├── execve.c
> │   ├── _exit.c
> │   ├── Makefile
> │   ├── malloc.c
> │   ├── open.c
> │   ├── setsid.c
> │   ├── string.c
> │   ├── wait.c
> │   └── write.c
> ├── Makefile
> ├── mm
> │   ├── Makefile
> │   ├── memory.c
> │   └── page.s
> ├── README.md
> └── tools
>     └── build.c
> 
> 15 directories, 101 files
> ```

## 操作系统的编译过程

操作系统的编译过程通过`Makefile`和`build.c`配合完成，最终实现：

1. 把`bootsect.s`编译成`bootsect`放在硬盘的第1扇区；
2. 把`setup.s`编译成`setup`放在硬盘的第2～5扇区；
3. 把剩下的全部代码(（`head.s`作为开头，与其它`.s`和`.c`文件）编译并链接成`system`放在硬盘随后的240个扇区中；

---

`setup`调用BIOS中断获取一些信息，并存储到内存中。

| 内存地址  | 长度(B) |   存储内容   |
| :-------: | :-----: | :----------: |
| `0x90000` |    2    |   光标位置   |
| `0x90002` |    2    |  扩展内存数  |
| `0x90004` |    2    |   显示页面   |
| `0x90006` |    1    |   显示模式   |
| `0x90007` |    1    |   字符列数   |
| `0x90008` |    2    |     XXX      |
| `0x9000A` |    1    |   显示内存   |
| `0x9000B` |    1    |   显示状态   |
| `0x9000C` |    2    | 显卡特性参数 |
| `0x9000E` |    1    |   屏幕行数   |
| `0x9000F` |    1    |   屏幕列数   |
| `0x90080` |   16    | 硬盘1参数表  |
| `0x90090` |   16    | 硬盘2参数表  |
| `0x901FC` |    2    |   根设备号   |

进入内核前

```mermaid
graph TD
A(开机)-->B(加载启动区)-->C(加载setup.s)-->D(加载内核)-->E(分段机制)-->F(进入保护模式)-->G(中断机制)-->H(分页机制)-->I(跳转到内核)
```

## 参考资料

[Linux源码趣读](https://book.douban.com/subject/36573361/)

[Intel® 64 and IA-32 Architectures Software Developer’s Manual](https://www.kdocs.cn/l/cogPTYblkdO9)

[汇编语言与接口技术](https://www.kdocs.cn/l/cgbvUL9UEkdd)