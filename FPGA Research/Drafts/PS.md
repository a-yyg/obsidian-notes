#draft 
# Basics
The *processing system* (PS) goes hand-in-hand with with *user-programmable-logic* ([[PL]]) side of the [[Zynq UltraScale+ MPSoC]].

The PS system features the following processors:
- [Arm® flagship Cortex®-A53 64-bit quad-core or dual-core processor](https://www.arm.com/products/silicon-ip-cpu/cortex-a/cortex-a53)
- [[RPU|Cortex-R5F dual-core real-time processor]]

It boast the following benefits:
- Scalable PS with scaling for power and performance
- Extended connectivity support including [[PCIe]], [[SATA]], and [[USB 3.0]]
- Advanced user interface(s) with GPU and DisplayPort
- *TODO: Expand this when I understand it better*

# PS-PL Communication
## Design
As seen in [[Zynq UltraScale+ MPSoC#Boot Sequence]], the PS system always boots first. Afterwards, it boots and [[PL#Configuration|configures]] the PL.
The purpose of this design is to allow a *software-centric approach* for PL configuration.

## [[AXI]] Interfaces
See [AXI Interfaces](https://docs.amd.com/r/en-US/ug1085-zynq-ultrascale-trm/PS-PL-AXI-Interfaces?tocId=vVIByUn5R_LZdcpo8nH3oA) also.
