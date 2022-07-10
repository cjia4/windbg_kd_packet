  
 + BOOLEAN KdRefreshDebuggerNotPresent();  
 + NTSTATUS KdEnableDebugger();
 + KeBugCheckEx(...);
 + void KdBreakPointWithStatus([in]  s);
 + NTSTATUS KdChangeOption
 + KdBreakPointWithStatus
KdPowerTransition
KdPollBreakIn

+ DbgkInitialize
+ DbgkpWakeTarget
+ DbgkCopyProcessDebugPort
+ DbgkpConvertKernelToUserStateChange

+ DbgkpSuspendProcess
+ DbgkpResumeProcess
+ DbgkpSectionToFileHandle
+ DbgkCreateThread
+ DbgkExitThread
+ DbgkExitProcess
+ DbgkMapViewOfSection
+ DbgkUnMapViewOfSection
+ DbgkpSendApiMessage

# KDCOM.dll
+ KdD0Transition
+ KdD3Transition
+ KdDebuggerInitialize0
+ KdDebuggerInitialize1
+ KdReceivePacket
+ KdRestore
+ KdSave
+ KdSendPacket


+ KiDebugRoutine
+ KdpTrap
+ KdpBreakpointTable

+ DbgKdGetVersionAPi
+ DbgKdRestoreBreakPointApi
+ DbgKdClearAllInternalBreakPointsApi
+ KdReadVirtualMemoryAPi


# Packet
+ PACKET_TYPE_KD_RESET

Ref:  

+ https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/wdm/nf-wdm-kdbreakpointwithstatus
+ https://blog.csdn.net/qq1841370452/article/details/77488331?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_title~default-0-77488331-blog-50962783.pc_relevant_aa2&spm=1001.2101.3001.4242.1&utm_relevant_index=3
+ https://blog.csdn.net/aerror/article/details/2958588?spm=1001.2101.3001.6650.15&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7Edefault-15-2958588-blog-50962783.pc_relevant_aa2&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7Edefault-15-2958588-blog-50962783.pc_relevant_aa2&utm_relevant_index=20
