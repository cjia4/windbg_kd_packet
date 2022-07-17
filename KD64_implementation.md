
# DIY OS KD64 instance  

Homebrew x64 OS written in C++
Fully utilize MSVC toolchain, PE kernel, MS visual studio sln files, self-contained KD64 (interact with windbg)
https://github.com/toddsharpe/MetalOS/blob/d03e06546a165c5153909efae73f581789cdfa89/MetalOS.Kernel/Debugger.cpp
https://github.com/toddsharpe/MetalOS/tree/master/MetalOS.Kernel.kd64
https://github.com/toddsharpe/MetalOS/blob/master/_Notes/WinDBG/KernelAndRemoteDebuggers.pdf
https://github.com/toddsharpe/MetalOS/blob/d03e06546a165c5153909efae73f581789cdfa89/_Screenshots/WinDbgFull.png
https://github.com/toddsharpe/MetalOS/blob/master/_Screenshots/WinDbgInit.PNG
https://github.com/toddsharpe/MetalOS/blob/master/_Screenshots/WinDbgDemo.mp4

#  radar2 windbg support
see the https://github.com/radare/radare2/tree/master/shlr/wind - this is the implementation of the WinDbg protocol and this is a radare2 part of WinDbg support https://github.com/radare/radare2/blob/master/libr/debug/p/debug_wind.c Here is the documentation how to work with it using radare2 https://github.com/radare/radare2/blob/master/doc/windbg

I think you need to see shlr/wind/transport.[ch] and shlr/wind/iob_pipe.c

Please, notice that all WinDbg code should be under LGPLv3.

https://github.com/radareorg/radare2/issues/17130
Add network support for WinDbg/KD (KDNET) ##debug #17340
https://github.com/radareorg/radare2/pull/17340
https://github.com/radareorg/radare2/pull/17340

# other info

@Manouchehri and a bit more links:
You can find Windbg protocol description in this BlackHat paper https://www.blackhat.com/presentations/bh-usa-07/Stewart/Presentation/bh-usa-07-stewart.pdf

See also VirtualKD program http://virtualkd.sysprogs.org/
Sources http://virtualkd.sysprogs.org/download_source/

And KD protocol description http://articles.sysprogs.org/kdvmware/kdcom/
Packet log http://virtualkd.sysprogs.org/kd_VMXPPRO/

WinDbg protocol sniffer - https://code.google.com/p/windbgshark/

http://www.msuiche.net/2014/01/12/extengcpp-part-1/
http://www.msuiche.net/2014/01/15/developing-windbg-extengcpp-extension-in-c-com-interface/
http://www.msuiche.net/2014/01/20/developing-windbg-extengcpp-extension-in-c-memory-debugger-markup-language-dml-part-3/
http://www.msuiche.net/2014/04/28/developing-windbg-extengcpp-extension-in-c-symbols-part-4/

@Manouchehri and a few more links

http://standa-note.blogspot.ca/2015/06/reverse-engineering-winbg-for-profit.html
https://github.com/tandasat/ListWorkItems

Lekensteyn commented on Jun 2, 2016
I wrote a Wireshark dissector for part of the Windbg/KD network protocol:
https://github.com/Lekensteyn/kdnet

It is incomplete, but decryption works and most higher-level structures are dissected. Here is also a capture and the related Windbg output with a Windows 10 machine as debugger and Checked/Debug build of Windows 10 as debuggee:
https://lekensteyn.nl/files/p651ra-acpi-debug/

Hope it helps in some way.

ghost commented on Jun 4, 2016
Hello !

This will be usefull for you :

https://github.com/Winbagility/Winbagility/tree/master/src/Winbagility
