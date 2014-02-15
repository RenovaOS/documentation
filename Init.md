Architecture
- Dependency based init system that does something like systemd and starts as many as it can at once with PMM and goes in rounds of starting things
- Has support for init files and init packages of files
- Init files generally depend on the packages and are started as early as possible
- Almost every init file will depend on base and many on users

Base Package - base
- Starts things generally expected of a base system, a device list populator, virtual filesystem manager (with vfs driver), message bus daemon

Users Package - users (base)
- Starts things associated with users, a user authentication daemon

Networking Package - networking (base)
- Starts things associated with networking, a tcp/ip stack, network manager daemon, dhcp daemon, authentication daemon (if necessary)

Desktop Package - desktop (base, users)
- Starts things associated with a desktop, login daemon, virtual terminals, etc.

Graphical Package - graphics (base)
- Starts things associated with graphics, a graphics (and compositing) daemon

Graphical Desktop Package - ?? (base, desktop, graphics)
- Starts things associated with a graphical desktop, a graphical login daemon (that in turn starts the user's associated window manager)
