#draft
# Basics
The [[Zynq UltraScale+ MPSoC]] is composed of many functional units in the [[PS]], including the *realtime processing unit* (RPU).
The RPU is a [Cortex-R5F](https://developer.arm.com/Processors/Cortex-R5) processor with the following characteristics:
- Arm instruction set
- Dynamic branch prediction
- Redundant CPU logic for fault detection
- 32/64/128-bit AXI interface to the PL for low-latency applications

It is described in the following way in the [Technical Reference Manual](https://docs.amd.com/r/en-US/ug1085-zynq-ultrascale-trm/System-Block-Diagram?tocId=cwKt_XE8QdFp3fpI6Kusaw):
>Cortex-R5F real-time processing unit (RPU)—Arm v7 architecture-based 32-bit dual real-time processing unit with dedicated tightly coupled memory (TCM).

The block diagram can be viewed below.
![[rpu_block.png]]

It uses the Arm PL390 for the [[GIC|Generic Interrupt Controller]].

## Differences with APU
The RPU doesn't have an [[MMU]], while the APU does. Since the MMU is used for the translation of virtual addresses to physical addresses, the RPU does not do [[MMU#Paging|paging]].

# References
[Ryuz88's Analysis](https://zenn.dev/ryuz88/books/zynqmp_study/viewer/realtime_processing_unit)