# Chapter 6: Packet filtering with Raw Sockets

A full description of this example can be found in Chapter 6.

If you follow this example from the book it will ask you to download kernel sources for `libbpf`
and install the dependencies. However, since you are here you are following the examples
in the Vagrant machine so all the dependencies are already handled if you followed the instructions in the main [README.md](/README.md).

In the vagrant machine:

Enter into this example folder:

```bash
cd /vagrant/code/chapter-6/packet-filtering-raw-sockets
```

Compile the loader

```bash
./build-loader.sh
```

It will create a binary file named `loader-bin`

Compile the program

```bash
./build-bpf-program.sh
```
It will create a BPF ELF named `bpf-program.o`


Execute the program using the loader:

```
./loader-bin bpf_program.o 
```

It will show something like this, ten results, one every second for ten seconds:

```
TCP 0 UDP 0 ICMP 0 packets
TCP 0 UDP 0 ICMP 0 packets
TCP 0 UDP 0 ICMP 0 packets
TCP 0 UDP 0 ICMP 0 packets
TCP 0 UDP 0 ICMP 4 packets
TCP 0 UDP 0 ICMP 8 packets
TCP 0 UDP 0 ICMP 12 packets
TCP 0 UDP 0 ICMP 16 packets
TCP 0 UDP 0 ICMP 16 packets
TCP 0 UDP 0 ICMP 16 packets
```

Since the program is attached to the loopback interface `lo` (see `loader.c` line 30) we need to generate traffic on
that interface to show the packets flow.

You can simply do a ping to localhost in the VM while the program is running.

```
ping 127.0.0.1
```
