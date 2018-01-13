# qubes-linux-kernel
Qubes component: linux-kernel

VERY experimental. Adds patches from the Linux Hardened project, plus various patches from the LKML that address the Meltdown/Spectre issue until official fixes are merged upstream (and maybe other issues too that are discovered over time). Could break at any moment (or not even compile??); provided as-is for anyone that wants to play around with it, with no guarantees of support. May need a Retpoline enabled compiler to fully take advantage of the security features.

**Current Status**:  Retpoline v6 and IBRS v3 patches in fine, boots and compiles successfully using a standard Fedora 25 build environment.

**Backporting Retpoline-enabled GCC to Fedora 25**

Prerequisite: Fedora 25 AppVM that can already compile a standard Qubes kernel.

Two options:

1) Compile Retpoline-enabled gcc yourself (Source Code: http://git.infradead.org/users/dwmw2/gcc-retpoline.git )

2) Backport Fedora 27 Retpoline-enabled gcc RPMs to Fedora 25:

- Grab all the RPMs from [here](https://copr-be.cloud.fedoraproject.org/results/jforbes/kernel-retpoline/fedora-27-x86_64/00700065-gcc/), as well as an x86_64 Fedora 27 version of isl from [here](https://rpmfind.net/linux/rpm2html/search.php?query=isl).
- In the Fedora 25 AppVM, install all RPMs using <code>sudo rpm -ivh --force *.rpm</code>. If complaints about missing system packages appear, make note of them, then in the Fedora 25 TemplateVM, install the Fedora 25 equivalents of the missing packages (<code> sudo dnf install *packagename*</code>). Then shut down the TemplateVM, reboot the AppVM, and then try installing the new rpms again. Keep repeating until the backported rpms install cleanly.
- Once done, run <code>make rpms</code> in the kernel build directory and the build process will use the new Retpoline-enabled gcc compiler instead of the standard Fedora 25 version. You can verify that it worked if no build messages appear warning you that your compiler isn't Retpoline enabled during kernel compilation. To make the compiler changes permanent, install the backported rpms into the TemplateVM instead of the AppVM.
