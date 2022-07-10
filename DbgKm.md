# Kernel debug API
+ DbgKmExceptionApi
+ DbgKmCreateThreadApi
+ DbgKmCreateProcessApi
+ DbgKmExitThreadApi
+ DbgKmExitProcessApi
+ DbgKmLoadDllApi
+ DbgKmUnloadDllApi
+ DbgKmMaxApiNumber

~~~
//
// Debug Event  
//  
typedef struct _DEBUG_EVENT   
{
    LIST_ENTRY EventList;
    KEVENT ContinueEvent;
    CLIENT_ID ClientId;
    PEPROCESS Process;
    PETHREAD Thread;
    NTSTATUS Status;
    ULONG Flags;
    PETHREAD BackoutThread;
    DBGKM_MSG ApiMsg;
} DEBUG_EVENT, *PDEBUG_EVENT;
~~~


DBGKM_APIMSG

ref:
https://www.cnblogs.com/yilang/p/11854419.html
