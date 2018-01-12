# qubes-linux-kernel
Qubes component: linux-kernel

VERY experimental. Adds patches from the Linux Hardened project, plus various patches from the LKML that address the Meltdown/Spectre issue until official fixes are merged upstream (and maybe other issues too that are discovered over time). Could break at any moment (or not even compile??); provided as-is for anyone that wants to play around with it, with no guarantees of support. May need a Retpoline enabled compiler to fully take advantage of the security features.

**Current Status**:  Patches in fine, does *not* compile under a stock FC25 devel environment (a syntax issue with the Retpoline V5 patch set, specifically *v5-07-12-x86-retpoline-xen-Convert-Xen-hypercall-indirect-jumps.patch*)
