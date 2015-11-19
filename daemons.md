daemons
=======

- separated into rings of type


### zeroth ring (core) (memory mapped to bootstrap system)

- daemon manager daemon
- loader daemon


### first ring (hardware)

- CPU daemon
- RAM daemon
- PCI daemon
- ACPI daemon
- etc.


### second ring (abstractions)

- file system daemon
- link daemon
- input daemon
- screen daemon
- clock daemon
- user daemon


### third ring (system applications)

- session daemon
- network daemon
- firewall daemon
- journal daemon
- time daemon
- graphic daemon


### fourth ring (user applications)

- HTTP daemon
- SMTP daemon
