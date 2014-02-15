Architecture
- Microkernel
- Provide a module API and let modules do the rest of the work
- Modules in their own package that is released independently
- Minor kernel version indicates driver or module changes
- Major kernel version indicates core module architecture or base kernel changes

Modules
- On startup, modules loaded sequentially after kernel in memory
- Module information is read and each module's init point is called in a row
- The entry point allows modules to set themselves up, init communication with hardware, add interrupt to PM if necessary, etc.
- Upon return from the last module, the deinit point will be called for each module, in reverse of the init point order
- The last module loaded will usually be a looped module that keeps running
- The first module loaded will usually be the one to halt the computer and possibly power it off
- Keep a record of module locations and their respective init point and deinit points
- Beginning of modules has a table of functions provided by that module
- Kernel provides API of getting and calling those functions
- Driver modules are loaded, if not already, when they are called
- Driver modules provide information about the ID of their hardware, which is used to identify them
- Driver modules are not ever search for more than once, there is a way to interface for the driver at each call without searching for it
- All modules can be loaded dynamically, including PM and MMM, by including a ramfs driver in the kernel and specifying a driver list by config option or by kernel argument

Rough order of modules when loaded on a normal desktop system:

Processor Module (PM)
- Provides functions for working with the processor
- Load is detecting processors and keeping them in a list
- Unload is calling a halt command, if registered, and running halt on all of the processors
- The halt command is by default set to power off but can be set to something else if necessary
- Calls an underlying driver's calls for most of its functions
- Defines the functions an underlying driver must implement
- Provides API for interrupts
- Keeps track of interrupts and makes sure too many interrupts aren't used
- Can return UNSUPPORTED in functions are not implemented

Memory Management Module (MMM)
- Keeps a record of memory available and used
- Provides API for adding and removing memory, will mostly be used by PMM
- Has API for adding a process and redirecting its memory calls
- Implements stack and heap for processes
- Both stack and heap are dynamic and fragmented where available in the memory
- Dynamically allocate its own memory for adding more processes
- Possibly overcommit memory, but need to keep very close eye on it
- Prevents processes from accessing other's memory
- Uses PM for underlying memory operations

Disk Module (DM)
- Abstracts storage format from partitions and storage medium
- Manages partition tables, partitions
- Determines disk driver based on ID data and calls the underlying driver's calls
- Defines the functions an underlying driver must implement
- Can return UNSUPPORTED in functions are not implemented

File System Module (FSM)
- Abstracts files and paths from their storage format
- Provides API for getting file/path descriptor
- Provides API for moving, deleting, etc. files and paths
- Utilizes DM for actually writing to disk
- Manages a list of filesystems and their mount points
- Checks permissions of things accessed and if origin does not have permission, returns UNAUTHORIZED

File Management Module (FMM)
- Loads open files into memory
- Allows editing of files
- When closed, it writes them to a file
- It also periodically, when nothing much is happening, writes to the disk
- It also implements disk caching for quick access to files by doing unloading of files with a low usage score and keeping files with a high score

Resource Management Module (RMM)
- Keeps track of loaded resources 
- Provides API for requiring resources that loads them if not already loaded
- Resources have a count for dependencies and are unloaded when count drops to 0

Executable Loading Module (ELM)
- Provides an API for loading executables by path
- Uses FMM to load main executable into memory
- Feeds library table to RMM for loading
- Defines executable format

Preemptive Multitasking Module (PMM)
- Interrupts the CPU at regular intervals for running processes and switch between them in line based on priority
- Selectable schedulers (at compile time)
- Uses PM to set the current execution pointer and add the interrupt
- More priority means more time
- Keeps process list, but uses MMM to allow dynamically expanding it
- Has API for starting more processes by command
- Sets up process information and passes command to ELM for loading
- Adds process to list
- List also keeps origin information, such as user, etc.
- Load is creating process 0, the init process, setting interrupt, and going into a loop of executing each process, which the processor comes back to at each interrupt
- Unload is killing each process one by one (calling their unloads) and removing interrupts
