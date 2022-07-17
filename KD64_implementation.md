
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

kd support branch
https://github.com/LemonBoy/radare2/tree/kdbg
https://github.com/radareorg/radare2/pull/1692

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

# Winbagility
Winbagility is a tool that gives you ability to connect WinDbg on non /DEBUG Windows x64 systems

How does it work ?
    Winbagility simulates a debugged kernel.
    It retrieves over the STUB for some essentials information (KDBG, KPCR...) and forward these informations to WinDbg over KD.
    link: https://www.reactos.org/wiki/Techwiki:Kd
    link: http://articles.sysprogs.org/kdvmware/kdcom.shtml
    
How to use ?
    Winbagility needs PDB to work. You need to set your _NT_SYMBOL_PATH and get the PDB of the kernel your want to debug.
    link: https://msdn.microsoft.com/en-us/library/windows/desktop/ee416588(v=vs.85).aspx
    link: https://msdn.microsoft.com/en-us/library/windows/hardware/ff558829(v=vs.85).aspx
    link: http://programming.realworldrobotics.com/system-kernel/microsoft-symbol-server-1/setting-the-_nt_symbol_path-environment-variable

https://github.com/Winbagility/Winbagility.github.io/blob/master/index.html

https://github.com/Winbagility/Winbagility/blob/master/src/Winbagility/kd.c
https://github.com/Winbagility/Winbagility/blob/master/src/Winbagility/kdproxy.c
https://github.com/Winbagility/Winbagility/blob/master/src/Winbagility/kdserver.c
