# Overview
PCIE protocol is everywhere nowadays and it is essensial for DV engineer to learn or at least get familiar with it. Just like AMBA protocol.
Thus open up this note to record my thoughs during this ramp-up process.


## Why we need PCIE protocol
Summarize: Traditional PCI&PCI-X protocol is serial interface and it is hitting the performance bottleneck.
1. PCI-X problem arise after 4 generation of PCI enhancement
* Bandwidth limiation. Even for PCI-X 533 the maximum bandwidth in 32bit machine is 4266MB/s and it is way more complex to integrate IP on chip/PCB. 
* Signal Integrity. There is signal integrity issue for every pin in serial port. 
* Lack of expansion. Maximum PCI-X endpoint/slave support is ~10 so there is no expansion space.

## PCIE protocol achievement
* 1. Less pin count
* 2. Higher bandwidth per pin
* 3. Strong Extendibility

## PCIE topology
<img width="761" height="631" alt="image" src="https://github.com/user-attachments/assets/cb847c40-fc25-4604-8fb5-bee305b9d7eb" />

