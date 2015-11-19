filesystem
==========

- all actions are queued on the disk and keep state so after a crash can be seamlessly resumed - moving the filesystem from block x to block y, copying a file from x to y, copying a file from memory 0xDEADBEEF to y, moving a file from x to y, moving block from block x to block y
- mounting makes directory
	- can't mount onto existing directory
- can copy conf and rebuild identical system (var for program data and home for users)
