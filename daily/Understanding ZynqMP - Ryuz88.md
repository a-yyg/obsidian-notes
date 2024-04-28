Original Title: [ZynqMPを理解しよう](https://zenn.dev/ryuz88/books/zynqmp_study)

This is a summary of what I could take from this series of articles.

# Chapter 1 - [はじめに](https://zenn.dev/ryuz88/books/zynqmp_study/viewer/introduction)
The author prefaces with the following reference link:
- [Zynq MPSoCで、コンピュータを学ぼう (その1) - Vengineerの戯言](https://vengineer.hatenablog.com/entry/2022/09/05/090000).

He then talks about some characteristics of the [[ZynqMP]] architecture that make it special and particularly suited towards edge computing:
- APU with support for Ether and USB peripherals like in a [[Raspberry Pi]]
- RPU for real-time processing like in an [[Arduino]] or ST microcontroller
- FPGA-like PL for creating circuits and I/O logic with flexible designs
- The three characteristics mentioned above interconnected (low communication cost)

In particular, he mentions that the RPU allows one to program a real-time OS, and that the PL allows for dense communication with devices outside the [[SoC]].

He mentions that the goal is to give the reader enough motivation and know-how to navigate and understand the technical reference manual by themselves.

# Chapter 2 - [身近なプロセッサ達](https://zenn.dev/ryuz88/books/zynqmp_study/viewer/familiar_processors)
In this article, the author talks about various [[Instruction Set|instruction sets]].
## [[x86]]
- [Intel® 64 and IA-32 Architectures Software Developer Manuals](https://www.intel.com/content/www/us/en/developer/articles/technical/intel-sdm.html)
## [[ARM]]
- The Japanese supercomputer Fugaku (富岳) uses ARM.
- The ARM-bus specification is based on [[AMBA]].
- Reference manuals:
	- [Arm Architecture Reference Manual for A-profile architecture](https://developer.arm.com/documentation/ddi0487/latest)
	- [ARM Architecture Reference Manual ARMv7-A and ARMv7-R edition](https://developer.arm.com/documentation/ddi0406/latest)
# [[RISC-V]]
- Open-source specification.
- Particularly popular among FPGA users.
- Specification sheet:
	- [Specifications – RISC-V International](https://riscv.org/technical/specifications/)
- Vector instructions are also defined:
	- [GitHub - mit-pdos/xv6-riscv: Xv6 for RISC-V](https://github.com/mit-pdos/xv6-riscv)
## [[GPGPU]]
- Very closed-source.
- [[SIMT]] architecture.
- Some references:
	- [CUDA Toolkit Documentation 12.4 Update 1](https://docs.nvidia.com/cuda/)
	- [NVIDIA H100 Tensor Core GPU Architecture Overview](https://resources.nvidia.com/en-us-tensor-core)
	- [GPU Domain Specialization via Composable
On-Package Architecture](https://arxiv.org/pdf/2104.02188)

## Computer Architecture Materials
- [コンピュータの構成と設計 MIPS Edition 第6版 上 | David Patterson, John Hennessy, 成田 光彰 |本 | 通販 | Amazon](https://www.amazon.co.jp/dp/4296070096)
- [コンピュータの構成と設計 MIPS Editoin 第6版 下 | David Patterson, John Hennessy, 成田 光彰 |本 | 通販 | Amazon](https://www.amazon.co.jp/dp/429607010X)
- [ヘネシー&パターソン コンピュータアーキテクチャ 定量的アプローチ第5版 | ジョン・L・ヘネシー, デイビッド・A・パターソン, 中條 拓伯, 天野 英晴, 吉瀬 謙二, 佐藤 寿倫, 中條 拓伯, 天野 英晴, 鈴木 貢 |本 | 通販 | Amazon](https://www.amazon.co.jp/dp/4798126233)
- [コンピュータアーキテクチャ 定量的アプローチ［第6版］【委託】 - 達人出版会](https://tatsu-zine.com/books/computer-architecture-6ed)

# Chapter 3 - [ZynqMPの中を見ていこう](https://zenn.dev/ryuz88/books/zynqmp_study/viewer/overview_zynqmp)
## Datasheets:
- [AMD Technical Information Portal](https://docs.xilinx.com/v/u/ja-JP/ds891-zynq-ultrascale-plus-overview)
- [AMD Technical Information Portal](https://docs.xilinx.com/r/ja-JP/ds925-zynq-ultrascale-plus)

One can find lots of useful information in these datasheets.
### Processor Performance
![[Pasted image 20240428202919.png|Grades -1 to -3 exist]]
### Block Diagram for the [[Zynq UltraScale+ MPSoC]]
![[Pasted image 20240428203100.png|I should try to understand what all of these components are]]
### [[PL]] and [[PS]]
The [[ZynqMP]] architecture is divided into the PL (programmable logic) and the PS (processor system).

#### PS
- Provides the necessary processing functions of an SoC
- [[Hardmacro]]
#### PL
- Basically an [[FPGA]]
- [[VCU|Video Codec Unit]] as a hard macro
- High-speed serial communication cores ([[GTH]] and [[GTY]]) as hard macros

## Functionality
### [[APU]]
[[PS]]-side. A processor unit containing a maximum of Cortex-A53 cores.
### [[RPU]]
[[PS]]-side. A processor unit containing **two** Cortex-R5 cores.
### [[Mali-400|GPU (Mali-400 MP2)]]
[[PS]]-side. Black-box GPU with a distributed Linux driver.
Possible to use OpenGL ES 1.1/2.0.
### [[PL]]
Uses [[PL#Configuration|configurable logic]] to create flexible circuits for control and computation.
### [[PMU]]
Previously a softmacro Micro-Blaze turned hardmacro.
Manages the power-related functions.
Xilinx provides a source code (?) for Linux.
### [[CSU]]
For security purposes.
Contains its own [[ROM]] and [[RAM]], as well as a [[CIB|Crypto Interface Block]].

# Chapter 10 - [ZynqMPでのLinuxプログラミング(APU)](https://zenn.dev/ryuz88/books/zynqmp_study/viewer/linux_programing)
We finally get some clues on the workflow for FPGA/Linux programming on the ZynqMP.

## Linux Configuration
Xilinx provides official Ubuntu images.
- [Getting Started with Certified Ubuntu 22.04 LTS for Xilinx Devices - Xilinx Wiki - Confluence](https://xilinx-wiki.atlassian.net/wiki/spaces/A/pages/2363129857/Getting+Started+with+Certified+Ubuntu+22.04+LTS+for+Xilinx+Devices)

**The RPU is not recognized by default.**
- Fix here: [Kria KV260 環境構築メモ](https://zenn.dev/ryuz88/articles/kv260_setup_memo)

>またその際に DeviceTree にある chosen の bootargs で cma の容量を指定しておくのも良いかもしれません。
- ?

Third-party Debian-based image also available!
- [GitHub - ikwzm/ZynqMP-FPGA-Linux: FPGA+SoC+Linux+Device Tree Overlay+FPGA Manager U-Boot&Linux Kernel&Debian11 Images (for Xilinx:Zynq Ultrascale+ MPSoC)](https://github.com/ikwzm/ZynqMP-FPGA-Linux)

## Program Flow
When programming for Linux, we use the APU as a master for the control flow.
1. Apply the DeviceTree overlay for various settings.
	1. PL download and clock set
	2. Interconnect configuration
	3. uio/u-dma-buf configuration
2. Download the softcore for the RPU.
3. Execute an APU program, opening the uio/u-dma-buf, or using OpenAMP to communicate with the RPU and PL.
4. Stop execution of the APU program by itself when the RPU and PL also exit.
5. Stop the RPU.
6. Download the bitstream and clear the PL?

- When working on uio/u-dma-buf without a proper Linux device driver, step 4 is particularly important.

# Chapter 11 - [ZynqMPでのベアメタルプログラミング(RPU)](https://zenn.dev/ryuz88/books/zynqmp_study/viewer/baremetal_programming)
#todo 