# l2fwdshared test environment

This directory contains Vagrant configuration files which will bring up a test
environment for [l2fwdshared](https://github.com/asavie/xdp/examples/l2fwdshared/l2fwdshared.go).

The environment consists of 3 virtual machines, 'Server', where you run the
`iperf` server, 'Client' where you run the `iperf` client and 'L2fwdshared', where
you run `l2fwdshared`.

'Client' and 'Server', in addition to the usual NAT interface, each have their
own additional 'Internal Network' interface.
'L2fwdshared' has two additional 'Internal Network' interfaces, one in 'Client'
network and one in 'Server' network. Thus 'L2fwdshared' is able to bridge the
networks between 'Client' and 'Server'.

## Key Feature

The main difference from the original l2fwd is that l2fwdshared implements shared UMEM
between two AF_XDP sockets. This approach optimizes memory usage and potentially
improves performance by allowing both sockets to access the same user-space memory
region for packet processing.

# How to deploy

1. Install Vagrant, e.g. on Fedora Linux: `sudo dnf install vagrant`.
2. Run `vagrant up` in each of the `server`, `client` and `l2fwdshared` directories.
3. Log into each machine by running `vagrant ssh` in corresponding directory
   and run the command that was printed at the end of provisioning in previous
   step.
