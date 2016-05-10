Bootloader
========================================

启动过程
----------------------------------------

Bootloader是嵌入式系统的引导加载程序，它是系统上电后运行的第一段程序，其作用类似PC机上的BIOS.
不同的处理器上电或复位后执行的第一条指令地址并不相同，对于ARM处理器来说，该地址为0x00000000。
对于一般的嵌入式系统，通常把Flash等非易失性存储器映射到这个地址处，而bootloader就位于该存储器
的最前端，所以系统上电或复位后执行的第一段程序便是bootloader。而因为存储bootloader的存储器不同，
bootloader的执行过程也并不相同.

Arm的启动都是从0地址开始，所不同的是地址的映射不一样。在arm开电的时候，要想让arm知道以某种
方式（地址映射方式）运行，不可能通过你写的某段程序控制，因为这时候你的程序还没启动，这时候
arm会通过引脚的电平来判断。

下面我们通过实例来介绍这个启动过程:

### S3C2440

https://github.com/leeminghao/doc-linux/blob/master/arch/arm/s3c2440/README.md

### MSM8960

https://github.com/leeminghao/doc-linux/blob/master/arch/arm/msm8960/README.md

作用
----------------------------------------

在bootloader完成对系统的初始化任务之后，它会将非易失性存储器(通常是Flash或EMMC等)中的Linux内核
拷贝到RAM中去，然后跳转到内核的第一条指令处继续执行，从而启动Linux内核。

bootloader一上电就拿到了cpu的使用权，它当然得干一些初始化的工作啊，比如关闭看门狗、设置cpu的
运行模式、设置堆栈等等比较急迫的事情。当然还要对主板的一些其他硬件进行简单的初始化，比如外部
DDR内存、网卡、显示屏、nand flash等等的初始化工作，最后还要负责把Linux内核加载到内存中。

lk
----------------------------------------

https://github.com/leeminghao/doc-linux/blob/master/bootloader/lk/README.md
