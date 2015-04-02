# 练习1

1. 操作系统镜像文件 ucore.img 是如何一步一步生成的?(需要比较详细地解释 Makefile 中每一条相关命令和命令参数的含义,以及说明命令导致的结果)

+ cc kern/init/init.c
gcc -Ikern/init/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -Ilibs/ -Ikern/debug/ -Ikern/driver/ -Ikern/trap/ -Ikern/mm/ -c kern/init/init.c -o obj/kern/init/init.o
+ cc kern/libs/readline.c
gcc -Ikern/libs/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -Ilibs/ -Ikern/debug/ -Ikern/driver/ -Ikern/trap/ -Ikern/mm/ -c kern/libs/readline.c -o obj/kern/libs/readline.o
+ cc kern/libs/stdio.c
gcc -Ikern/libs/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -Ilibs/ -Ikern/debug/ -Ikern/driver/ -Ikern/trap/ -Ikern/mm/ -c kern/libs/stdio.c -o obj/kern/libs/stdio.o
+ cc kern/debug/kdebug.c
gcc -Ikern/debug/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -Ilibs/ -Ikern/debug/ -Ikern/driver/ -Ikern/trap/ -Ikern/mm/ -c kern/debug/kdebug.c -o obj/kern/debug/kdebug.o
+ cc kern/debug/kmonitor.c
gcc -Ikern/debug/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -Ilibs/ -Ikern/debug/ -Ikern/driver/ -Ikern/trap/ -Ikern/mm/ -c kern/debug/kmonitor.c -o obj/kern/debug/kmonitor.o
+ cc kern/debug/panic.c
gcc -Ikern/debug/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -Ilibs/ -Ikern/debug/ -Ikern/driver/ -Ikern/trap/ -Ikern/mm/ -c kern/debug/panic.c -o obj/kern/debug/panic.o
+ cc kern/driver/clock.c
gcc -Ikern/driver/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -Ilibs/ -Ikern/debug/ -Ikern/driver/ -Ikern/trap/ -Ikern/mm/ -c kern/driver/clock.c -o obj/kern/driver/clock.o
+ cc kern/driver/console.c
gcc -Ikern/driver/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -Ilibs/ -Ikern/debug/ -Ikern/driver/ -Ikern/trap/ -Ikern/mm/ -c kern/driver/console.c -o obj/kern/driver/console.o
+ cc kern/driver/intr.c
gcc -Ikern/driver/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector 

-Ilibs/ -Ikern/debug/ -Ikern/driver/ -Ikern/trap/ -Ikern/mm/ -c kern/driver/intr.c -o 

obj/kern/driver/intr.o
+ cc kern/driver/picirq.c
gcc -Ikern/driver/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector 

-Ilibs/ -Ikern/debug/ -Ikern/driver/ -Ikern/trap/ -Ikern/mm/ -c kern/driver/picirq.c -o 

obj/kern/driver/picirq.o
+ cc kern/trap/trap.c
gcc -Ikern/trap/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -

Ilibs/ -Ikern/debug/ -Ikern/driver/ -Ikern/trap/ -Ikern/mm/ -c kern/trap/trap.c -o 

obj/kern/trap/trap.o
+ cc kern/trap/trapentry.S
gcc -Ikern/trap/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -

Ilibs/ -Ikern/debug/ -Ikern/driver/ -Ikern/trap/ -Ikern/mm/ -c kern/trap/trapentry.S -o 

obj/kern/trap/trapentry.o
+ cc kern/trap/vectors.S
gcc -Ikern/trap/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -

Ilibs/ -Ikern/debug/ -Ikern/driver/ -Ikern/trap/ -Ikern/mm/ -c kern/trap/vectors.S -o 

obj/kern/trap/vectors.o
+ cc kern/mm/pmm.c
gcc -Ikern/mm/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -

Ilibs/ -Ikern/debug/ -Ikern/driver/ -Ikern/trap/ -Ikern/mm/ -c kern/mm/pmm.c -o 

obj/kern/mm/pmm.o
+ cc libs/printfmt.c
gcc -Ilibs/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -Ilibs/  

-c libs/printfmt.c -o obj/libs/printfmt.o
+ cc libs/string.c
gcc -Ilibs/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -Ilibs/  

-c libs/string.c -o obj/libs/string.o
首先将内核需要的各个.c源文件编译成.o文件
+ ld bin/kernel
ld -m    elf_i386 -nostdlib -T tools/kernel.ld -o bin/kernel  obj/kern/init/init.o 

obj/kern/libs/readline.o obj/kern/libs/stdio.o obj/kern/debug/kdebug.o 

obj/kern/debug/kmonitor.o obj/kern/debug/panic.o obj/kern/driver/clock.o 

obj/kern/driver/console.o obj/kern/driver/intr.o obj/kern/driver/picirq.o 

obj/kern/trap/trap.o obj/kern/trap/trapentry.o obj/kern/trap/vectors.o obj/kern/mm/pmm.o  

obj/libs/printfmt.o obj/libs/string.o
然后将上一步生成的.o文件都链接起来，生成kernel映像
+ cc boot/bootasm.S
gcc -Iboot/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -Ilibs/ 

-Os -nostdinc -c boot/bootasm.S -o obj/boot/bootasm.o
+ cc boot/bootmain.c
gcc -Iboot/ -fno-builtin -Wall -ggdb -m32 -gstabs -nostdinc  -fno-stack-protector -Ilibs/ 

-Os -nostdinc -c boot/bootmain.c -o obj/boot/bootmain.o
+ cc tools/sign.c
gcc -Itools/ -g -Wall -O2 -c tools/sign.c -o obj/sign/tools/sign.o
gcc -g -Wall -O2 obj/sign/tools/sign.o -o bin/sign
编译Bootloader需要的bootasm.S和bootmain.c，生成.o文件；同时编译生成bootblock需要的sign工具
+ ld bin/bootblock
ld -m    elf_i386 -nostdlib -N -e start -Ttext 0x7C00 obj/boot/bootasm.o 

obj/boot/bootmain.o -o obj/bootblock.o
将两个.o文件链接起来生成bootblock.o
'obj/bootblock.out' size: 472 bytes
objcopy将bootblock.o中除了符号表的部分拷贝到bootblock.out
build 512 bytes boot sector: 'bin/bootblock' success!
使用sign工具将bootblock.out处理成x86 bootloader格式的文件bootblock
dd if=/dev/zero of=bin/ucore.img count=10000
dd if=bin/bootblock of=bin/ucore.img conv=notrunc
dd if=bin/kernel of=bin/ucore.img seek=1 conv=notrunc
创建一个大小为10000块的映像文件，首先全部写成0，然后依次写入Bootloader和内核kernel

2.  一个被系统认为是符合规范的硬盘主引导扇区的特征是什么?
磁盘主引导扇区只有512字节，且最后两个字节是55 AA。

# 练习2
1. 从CPU加电后执行的第一条指令开始，单步跟踪BIOS的执行。  
在lab1目录下，执行make debug，打开gdb，输入"target remote :1234"，然后使用si或者ni指令就可以单步跟踪BIOS了。

2. 在初始化位置0x7c00设置实地址断点,测试断点正常。
测试正常

3. 从0x7c00开始跟踪代码运行,将单步跟踪反汇编得到的代码与bootasm.S和 bootblock.asm进行比较。
单步跟踪反汇编得到的代码与bootasm.S和bootblock.asm的代码相同。

4. 自己找一个bootloader或内核中的代码位置，设置断点并进行测试。
测试正常

# 练习3
请分析bootloader是如何完成从实模式进入保护模式的。
1. 首先将所有寄存器和标志位清零。
2. 然后开启A20，通过给A20线高电平打开，然后就可以访问4G的内存空间了。
3. 装载GDT表
4. 使能CR0寄存器的PE位置
5. 通过longjmp protcseg进入保护模式

# 练习4
通过分析源代码和通过qemu来运行并调试bootloader&OS，
1. bootloader如何读取硬盘扇区的？
首先一直等待直到硬盘空闲，然后向0x1f2写入1表示一个扇区,0x1f3-0x1f6位置写入secno表示扇区的编号,0x1f7写入0x20表示读取。再一直等待直到硬盘准备好，最后从0x1f0开始读取数据。

2. bootloader是如何加载ELF格式的OS？
首先读取硬盘的第二个扇区即kernel的第一部分，包括elfheader。然后判断魔数是否为ELF_MAGIC。是的话再读取program header和end program header作为起始和结束位置。最后依次读取后边扇区的内容，进入内核的入口函数entry。

# 练习5
请完成实验，看看输出是否与上述显示大致一致，并解释最后一行各个数值的含义。  
与上述显示大致一致。  
最后一行ebp:0x00007bf8 eip:0x00007d68 args:0xc031fcfa 0xc08ed88e 0x64e4d08e 0xfa7502a8
ebp是由于堆栈从0x7c00开始，压入了两个元素;eip指向的是((void (*)(void))(ELFHDR->e_entry & 0xFFFFFF))();的下一条语句即outw(0x8A00, 0x8A00);的地址;后边的四个参数是Bootloader起始地址0x7c00开始的几条指令的机器码

# 练习6
中断向量表中一个表项占多少字节？其中哪几位代表中断处理代码的入口？
一个表项占用8字节，第16-31位是中断处理代码的段选择子，0-15和48-63位组成中断处理代码的偏移量。
