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

## 参考资料

[Linux源码趣读](https://book.douban.com/subject/36573361/)

[Intel® 64 and IA-32 Architectures Software Developer’s Manual](https://www.kdocs.cn/l/cogPTYblkdO9)

[汇编语言与接口技术](https://www.kdocs.cn/l/cgbvUL9UEkdd)