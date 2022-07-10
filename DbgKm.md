# user mode debug API
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
    DBGKM_APIMSG ApiMsg;
} DEBUG_EVENT, *PDEBUG_EVENT;
~~~

~~~
//消息结构
typedef struct _DBGKM_APIMSG { 
    PORT_MESSAGE h;                                //+0x0
    DBGKM_APINUMBER ApiNumber;                    //+0x18
    NTSTATUS ReturnedStatus;                    //+0x1c
    union { 
        DBGKM_EXCEPTION Exception;              //异常
        DBGKM_CREATE_THREAD CreateThread;       //创建线程
        DBGKM_CREATE_PROCESS CreateProcessInfo; //创建进程
        DBGKM_EXIT_THREAD ExitThread;           //线程退出
        DBGKM_EXIT_PROCESS ExitProcess;         //进程退出
        DBGKM_LOAD_DLL LoadDll;                 //映射DLL
        DBGKM_UNLOAD_DLL UnloadDll;             //反映射DLL
    } u;                                        //0x20
} DBGKM_APIMSG, *PDBGKM_APIMSG;
~~~



Dbgk是内核中处理调试功能的所有支持代码的组件。

# API
+ DbgkpWakeTarget(DebugEvent)
+ 
该实现通过一个名为DEBUG_Object的NT对象公开，并提供各种系统调用来访问它。

ref:
https://www.cnblogs.com/yilang/p/11854419.html
