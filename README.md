# Linux/RISC-V

This is a port of Linux kernel for the [RISC-V](http://riscv.org/)
instruction set architecture.
This is originally cloned from the branch priv-1.9 of [riscv-linux](https://github.com/riscv/riscv-linux). It is noticed that this branch is removed from the origin repository.

This kernel sources can be built using the riscv-tools (gcc 6.1.0) that are used in [fpga-zynq](https://github.com/ucb-bar/fpga-zynq).
The linux can run on a Rocket Chip hosted on Zedboard. 

## Obtaining kernel sources

	   $ git clone https://github.com/phthinh/riscv-linux.git linux-4.6.2

        $ curl -L https://cdn.kernel.org/pub/linux/kernel/v4.x/linux-4.6.2.tar.xz | tar -xJKf
        $ cd linux-4.6.2

## Building the kernel image

1. Apply some modifications (if required):
	   $ git apply patch.diff

1. Create kernel configuration based on architecture defaults:

        $ make ARCH=riscv defconfig

1. Optionally edit the configuration via an ncurses interface:

        $ make ARCH=riscv menuconfig

1. Build the uncompressed kernel image:

        $ make -j8 ARCH=riscv vmlinux

## Exporting kernel headers

The `riscv-gnu-toolchain` repository includes a copy of the kernel header files.
If the userspace API has changed, export the updated headers to the
`riscv-gnu-toolchain` source directory:

    $ make ARCH=riscv headers_check
    $ make ARCH=riscv INSTALL_HDR_PATH=path/to/riscv-gnu-toolchain/linux-headers headers_install

Rebuild `riscv64-unknown-linux-gnu-gcc` with the `linux` target:

    $ cd path/to/riscv-gnu-toolchain
    $ make linux

