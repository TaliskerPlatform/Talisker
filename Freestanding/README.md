# Talisker
## Native components

This directory in a configured build tree will contain the components which
are built for a freestanding environment on host the machine. It is used
to compile bootloaders, kernels, and so on.

The `configure.gnu` wrapper script is invoked by the `configure` script
in the parent directory in order to ensure that the components are configured
with the correct parameters for a freestanding build alongside the rest
of the system.
