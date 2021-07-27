### CPU
### ABI (Application Binary Interface):
- armeabi-v7a
- arm64-v8a
- x86
- x86_64


### Bootloader
### is used for initializing kernel
CPU -> Boot ROM (piece of code) -> Bootloader -> Kernel -> Init -> Native Daemons -> 
-> Android Runtime -> Zygote -> System Server


Kernel
- power management (wake locks)
- Aggressive Low Memory Killer (VS regular Linux OOM Killer)
-- foreground process
-- visible process 
-- service process
-- cached process


### Init
### The file: init.rc
it triggers Zygote process



### Native Daemons
### Native Daemons communicate via Unix Domain Socket 
### with bootstrap services (i.e. NetworkService, StorageService, etc.)
### (not very secure, not very fast)
- installd (used for installing/uninstalling apps)
(PackageManagerService communicates with installd via Unix Domain Socket)
- vold
- netd
- rild
- keystore
- ...


### Android Runtime
- it is a cpp class that starts Zygote and System Server



### Zygote process
### It has:
- DalvikVM (or ART)
- Preload Classes
- create ZygoteServer
- start System Server

### ZygoteInit -> ZygoteServer.runSelectLoop() -> forkAndSpecialize() (i.e. creates new processes)



### System Server
- starts SystemServerManager
- starts Activity Thread 
### In System Server:
### ActivityThread
ActivityThread.main() 
  Looper.prepareMain() (this launches app's UI thread with Handler)
    Looper.loop()









