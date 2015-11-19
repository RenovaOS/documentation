kernel
======


### features

- basic interrupts (timers)
- basic scheduling (using kernel itself as its own process to register it's resources and in case it needs to do processing)
- message bus
- kernel will be pid 0
- stop signal will halt system
- reload signal will cause it to restart the kernel as any other process allowing for live upgrades (will be tough)
	- probably could exec itself with serialized state on command line
