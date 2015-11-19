executables
===========

- executables depend on servers that the loader daemon tells the daemon manager daemon to start and stop
- libraries and programs both use the same executable format
- programs can be loaded as libraries


programs
--------

- have entry point defined


libraries
---------

- strong versioning
- can have many versions of the same library installed many times
- easy static or dynamic linking from the same executable files
- static linking inlines library at the end of the program and puts a memory address in the library table
- dynamic linking only requires a library name in the table
- official repo will be dynamically linked since cost should be low per the loader daemon
- since libraries are executables, they can depend on other libraries obviating the need to link together every library dependency into a program
