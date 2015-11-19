init
====

- handled by daemon manager daemon
- does dependency based booting similar to systemd
	- puts daemons in rounds of mass startup based on dependency levels and targets
- will run as user init (on login or with system)
	- just does not have system targets


targets
-------


### base

- things up to the second ring will depend on this
- a system at base really only has an emergency shell available - there is no networking, session management, time synchronization
- still no filesystems mounted


### file (base)

- mount filesystems (since those might require extra daemons)


### misc (base, file)

- things necessary for miscellaneous system functions
- time daemon
- journal daemon


### network (base)

- things necessary for a networked system
- network daemon
- firewall daemon


### user (base, file, [network], [misc])

- things necessary for a multi-user system
- session daemon
- user applications and inits


### graphic (user)

- things necessary for a graphical system
- graphic daemon
- some kind of login program running on a screen
