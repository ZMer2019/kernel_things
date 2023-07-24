# kernel config for debuging kernel

```
Kernel hacking 
	printk and demsg options --->
		[*] Show timing information on printks
	Compile-time checks and compiler options  --->
		[*] Compile the kernel with debug info
		[*]   Provide GDB scripts for kernel debugging
		[*] Enable full Section mismatch analysis
	[*] Magic SYsRq key

Processor type and features
	-*- Build a relocatable kernel
	[ ]   Randomize the address of the kernel image (KASLR)
```

# 修改Makefile 中的编译优化等级(for linux-4.19.248)
编辑Makefile，将-O2替换为-O0 同时加入-g参数，如下修改
```
KBUILD_HOSTCFLAGS   := -Wall -Wmissing-prototypes -Wstrict-prototypes -O0 -g \
					-fomit-frame-pointer -std=gnu89 $(HOST_LFS_CFLAGS) \
					$(HOSTCFLAGS)
KBUILD_HOSTCXXFLAGS := -O0 -g $(HOST_LFS_CFLAGS) $(HOSTCXXFLAGS)

ifdef CONFIG_CC_OPTIMIZE_FOR_SIZE
KBUILD_CFLAGS   += -Os
else
KBUILD_CFLAGS   += -O1#此处改称O0会导致asm文件的编译出错
endif
```
