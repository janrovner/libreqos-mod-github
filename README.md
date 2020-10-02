# LibreQoS
A simple way to shape hundreds of clients and reduce bufferbloat using fq_codel or CAKE. This is alpha software, please do not deploy in production.

## Lab Requirements
* Edge and Core routers with MTU 1500 on links between them
* OSPF primary link (low cost) through the server running LibreQoS
* OSPF backup link recommended
![Diagram](docs/diagram.png?raw=true "Diagram")

## Server Requirements
* VM or physical server
* One management network interface
* Two dedicated network interface cards, preferably SFP+ capable
* 8GB RAM or more recommended
* Python 3
* Recent Linux kernel
* tc (usually pre-installed)

## Server Spec Recommendations
* For up to 1Gbps
    * 4+ CPU cores
    * 8GB RAM
    * 32GB Disk Space
    * Passmark score of 17,000 or more (AMD Ryzen 5 3600 or better)
* For up to 5Gbps
    * 8+ CPU cores
    * 16GB RAM
    * 32GB Disk Space
    * Passmark score of 23,000 or more (AMD Ryzen 7 3800X or better)
* For up to 10Gbps
    * 16+ CPU cores
    * 32GB RAM
    * 32GB Disk Space
    * Passmark score of 38,000 or more (AMD Ryzen 9 3950X or better)
https://www.cpubenchmark.net/high_end_cpus.html


## Features
* fq_codel
* Cake (Common Applications Kept Enhanced) [Experimental]
* HTB (Hierarchy Token Bucket)
* tc filters divided into groups with hashing filters to significantly increase efficiency

## How to use
* Add linux interface bridge br0 to the two dedicated interfaces
    * For example on Ubuntu Server 20.04 which uses NetPlan, you would add the following to the .yaml file in /etc/netplan/
```
bridges:
    br0:
      interfaces:
           - eth4
           - eth5
```
* Modify setting parameters in LibreQoS.py to suit your environment
* Run:
```
sudo python3 ./LibreQoS.py
```
## Special Thanks
Thank you to the hundreds of contributors to the cake and fq_codel projects. Thank you to Phil Sutter, Bert Hubert, Gregory Maxwell, Remco van Mook, Martijn van Oosterhout, Paul B Schroeder, and Jasper Spaans for contributing to the guides and documentation listed below.

## References
* https://tldp.org/HOWTO/Adv-Routing-HOWTO/lartc.adv-filter.hashing.html
* http://linux-ip.net/gl/tc-filters/tc-filters.html

## License
Copyright (C) 2020 Robert Chacón

LibreQoS is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 2 of the License, or
(at your option) any later version.

LibreQoS is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with LibreQoS.  If not, see <http://www.gnu.org/licenses/>.
