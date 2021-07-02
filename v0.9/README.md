Requires XDP-CPUMAP-TC
Only works on dedicated linux machine at the moment, not on VMs.
Will soon work on VMs once <a href="https://www.spinics.net/lists/bpf/msg42260.html">this patch</a> is part of the mainline linux kernel.

```
cd LibreQoS
git clone https://github.com/xdp-project/xdp-cpumap-tc.git
cd /xdp-cpumap-tc/src/
git submodule update --init
sudo apt install clang gcc llvm libelf-dev
make
```