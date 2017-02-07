# Talisker
## Personalities

Talisker Personalities are packaged combinations of system-wide and per-user
services, launchers, libraries and applications which provide a particular
execution environment. With no personalities enabled, a Talisker system is
able to boot and load device drivers, and provide a command-line emergency
rescue interface.

Personalities can be self-contained, or integrated into the system.
Self-contained personalities are typically (but not exclusively) those which
which operate within virtual machines. Self-contained personalities may
establish communication channels with the host system to enable file sharing,
clipboard synchronisation, and other similar features.

In contrast, integrated personalities will operate as any native process does,
with the same access to files and other resources. The contents of the
personality bundle installed on the system for an integrated personality
may be minimal — consisting of shared frameworks and services which support
applications built for that personality. Often (but again, not exclusively),
binaries for an integrated personality are native executables which simply
make use of the frameworks provided by that personality.

