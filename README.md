# me_cleaner [![Donation](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=B5HCXCLZVCVZ8)

Intel ME is a coprocessor integrated in all post-2006 Intel boards, for which
this [Libreboot page](https://libreboot.org/faq.html#intelme) has an excellent
description. The main component of Intel ME is Intel AMT, and I suggest you to
read [this Wikipedia page](https://en.wikipedia.org/wiki/Intel_Active_Management_Technology)
for more informations about it. In short, Intel ME is an unremovable environment
with an obscure signed proprietary firmware, with full network and memory
access, which poses a serious security threat.
Even when disabled from the BIOS settings, Intel ME is active: the only way to
be sure it is disabled is to remove its firmware from the flash chip.

Before Nehalem (ME version 6, 2008/2009) the ME firmware could be removed
completely from the flash chip by setting a couple of bits inside the flash
descriptor, without the need of reverse-engineer the ME firmware.

Starting from Nehalem the Intel ME firmware can't be removed anymore: without a
valid firmware the PC shuts off forcefully after 30 minutes. This project is an
attempt to remove as much code as possible from such firmware without falling
into the 30 minutes window mode.

me_cleaner currently works on most architectures, see [me_cleaner status](https://github.com/corna/me_cleaner/wiki/me_cleaner-status) (or [its discussion](https://github.com/corna/me_cleaner/issues/3))
for more info about them. me_cleaner works also on the TXE and SPS firmware.

If you want to understand how me_cleaner works, you can read the ["How does it work?" page](https://github.com/corna/me_cleaner/wiki/How-does-it-work%3F).

If you want to apply me_cleaner on your plaform I suggest you to read the
["How does it work?" page](https://github.com/corna/me_cleaner/wiki/How-does-it-work%3F)
and then follow the guide ["How to apply me_cleaner"](https://github.com/corna/me_cleaner/wiki/How-to-apply-me_cleaner).

For pre-Skylake firmware (ME version < 11) this tool removes almost everything,
leaving only the two fundamental modules needed for the correct boot, ROMP and
BUP. The code size is reduced from 1.5 MB (non-AMT firmware) or 5 MB (AMT
firmware) to ~90 kB of compressed code.

For Skylake and the later architectures (ME version >= 11), since the internal
structure of the partitions is not yet known, the FTPR partition is left intact.
The code size is reduced from 1.5 MB/5 MB to ~650 kB of compressed code.

This project is based on the work of the community; in particular I thank Igor
Skochinsky, for the core informations about Intel ME and its firmware structure,
and Federico Amedeo Izzo, for its help during the study of Intel ME.
