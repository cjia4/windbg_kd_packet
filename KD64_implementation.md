
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
Winbagility can be connected on 4 types of support:
        * Raw Physical Memory Dump Mode
            Just do a physical memory dump with a specialized tool
            link: https://www.magnetforensics.com/computer-forensics/acquiring-memory-with-magnet-ram-capture/
        
            cmd: winbagility.exe \\.\pipe\client CRASH 10_x64.bin
            cmd: "C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\windbg.exe" -k com:pipe,port=\\.\\pipe\\client,resets=0,reconnect
        
        * GDB VMWare Mode
            You need to start VMWare Virtual Machine with GDB activated.
            link: http://wiki.osdev.org/VMware#Guest_debugging
            link: http://ddeville.me/2015/08/using-the-vmware-fusion-gdb-stub-for-kernel-debugging-with-lldb/
        
            cmd: winbagility.exe \\.\pipe\client GDB 127.0.0.1:8864
            cmd: "C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\windbg.exe" -k com:pipe,port=\\.\\pipe\\client,resets=0,reconnect
        
        * LiveKD-like Mode
            You need to load WinPmem Driver (winpmem-2.1.post4.exe)
            link: https://github.com/google/rekall/releases
        
            cmd(as administrator): winpmem-2.1.post4.exe -l
            cmd(as administrator): winbagility.exe \\.\pipe\client LIVEKADAY ?
            cmd(as administrator): "C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\windbg.exe" -k com:pipe,port=\\.\\pipe\\client,resets=0,reconnect
        
        * Fast Debugging Protocol Mode
            ! See Fast Debugging Protocol section !  

Where can I get the source/binaries ?
    The project uses cmake and compile on Visual Studio 2013 and Visual Studio 2015
    link: https://github.com/Winbagility/Winbagility
    
    cmd: build.bat
        
How to contribute ?
    * extend Kd Server, some message are missing (ex.: !pci)
    * bugfix (Stub and Kd server)
    * x86 support (Read Only for the moment)
    * create windows profils
    * file reorganisation
    * extend GDB VMWare stub (Memory breakpoint with Debug Registers)
    * add stub
    * extend CRASH stub to support more Windows version (Pdb brute force)
    * multi-cpu support
    * bug repport

========================FAST DEBUGGING PROTOCOL========================
What is this ?
    FDP is an introspection API for VirtualBox.
    
How does it work ?
    This is a patch of VirtualBox that provides :
        *Virtual memory read
        *Virtual memory write
        *Physical memory read
        *Physical memory write
        *Register/MSR read
        *Register/MSR write
        *Pause of the guest
        *Resume of the guest
        *Save of the guest
        *Restore of the guest
        *Stealth memory breakpoint (PageHyperBreakpoint)
        *Stealth software breakpoint (SoftHyperBreakpoint)
        *Stealth hardware breakpoint (HardHyperBreakpoint)
        *Python bindings
    
How to use ?
    1. Apply path on Virtualbox and compile it or,
    1. Download precompiled Virtualbox version
    
    2. go to VBoxBin directory
        cmd(as administrator): comregister.cmd
        cmd(as administrator): loadall.cmd
       
    3. Start virtualbox
        cmd: Virtualbox.exe
        
    4. Use FDP library to connect to the virtual machine
    

Where can I get the source/binaries ?
    link: https://github.com/Winbagility/Winbagility
    link: https://www.virtualbox.org/wiki/Windows%20build%20instructions
    
Python Bindinds ?
    Volatility and Rekall address space is available.
    
    code example:
        from FDP import *
        import struct
        
        fdp = FDP("7_SP1_x64")
        
        NtWriteFile = 0xfffff800029ee9a0
        
        fdp.Pause()
        fdp.UnsetAllBreakpoint()
        fdp.WriteRegister(FDP_CPU0, FDP_DR7_REGISTER, 0x400)
        fdp.SetBreakpoint(FDP_CPU0, FDP_SOFTHBP, 0, FDP_EXECUTE_BP, FDP_VIRTUAL_ADDRESS, NtWriteFile, 1)
        fdp.Resume()
        
        while True:
            if fdp.WaitForStateChanged() & FDP_STATE_BREAKPOINT_HIT:
                print ".",
                Rsp = fdp.ReadRegister(FDP_CPU0, FDP_RSP_REGISTER)
                BufferPtr = fdp.ReadVirtualMemory64(FDP_CPU0, Rsp+(6*8))
                BufferSize = fdp.ReadVirtualMemory32(FDP_CPU0, Rsp+(7*8))
                if BufferSize > 3 and BufferSize < FDP_1M:
                Buffer = fdp.ReadVirtualMemory(FDP_CPU0, BufferPtr, BufferSize)
                if Buffer != None and Buffer[1] == 'P' and Buffer[2] == 'N' and Buffer[3] == 'G': 
                    f = open("./test.png", "wb")
                    f.write(Buffer)
                    f.close()
                    print "\nFile Written"
                fdp.SingleStep(FDP_CPU0)
                fdp.Resume()
                
Performances ?
    *600000 Reads of Virtual 4K per second
    *800000 Reads of Physical 4K per second
    *2GB VM Restore in 2 seconds
    *27000 HardHyperBreapoints per second
    *21000 SoftHyperBreakpoints per second
    *7000 PageHyperBreapoints per second
 
Winbagility connection ?
    Start a Virtual Machine in a FDP patched version of VirtualBox
    cmd: winbagility.exe \\.\pipe\client FDP VBox_Virtual_Machine_Name
    cmd: "C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\windbg.exe" -k com:pipe,port=\\.\\pipe\\client,resets=0,reconnect
    
Known bugs ?
    * Please don't debug a Virtual machine with more than one CPUs
    * FDP_SetFxState is bugged !
    * Some <2010 CPU aren't supported (xgetbv/xsetbv)
        
How to contribute ?
    * x86 support
    * bugfix
    * performance improvement (memory mapping, new breakpoint)
    * missing registers read/write
    * file reorganisation
    * multi-cpu support
    * bug repport    
https://github.com/Winbagility/Winbagility/blob/master/src/Winbagility/kd.c
https://github.com/Winbagility/Winbagility/blob/master/src/Winbagility/kdproxy.c
https://github.com/Winbagility/Winbagility/blob/master/src/Winbagility/kdserver.c
