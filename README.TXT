*************************************************************************
*									*
*	EMS 4.0 Driver for TOPCAT mainboards, rev.01, Apr-20		*
*									*
*	This code is TASM source.					*
*									*
*	Based on original works Copyright (c) 1988, Alex Tsourikov.	*
*	All rights reserved.						*
*									*
*	Original source kindly provided subject to the BSD 3-Clause	*
*	License: http://opensource.org/licenses/BSD-3-Clause		*
*									*
*	Based on an adaption for the Lo-Tech EMS board, which is	*
*	provided subject to the terms of use at:			*
*									*
*	http://www.lo-tech.co.uk/wiki/lo-tech.co.uk:General_disclaimer	*
*									*
*									*
*	No charge has been made for this software.			*
*									*
*************************************************************************

Please find binary releases at https://karcherm.github.io/topemm/

Syntax:    DEVICE=LTEMM.EXE [/switches]
 /p:nnnn - Page frame address (E000)
 /h:nnn  - Maximal number of handles (64)
 /d:nn   - Depth of contest saves (5)
 /n      - Bypass memory test
 /x      - Perform long memory test
 /3      - Use only EMS 3.2 functions
 /q      - Quiet mode

Defaults in parentheses. This driver has been tested under MS-DOS 6.22.

This driver is compatible with UMB_DRVR by Christopher Blum. Load UMB_DRVR
first and exclude 64K UMB space (by putting '-' characters into the map).
This space can be used for as page frame for TOPEMM.

Issues remaining:
 - The initialization code is incompatible with the VL82C330 / Intel 82346
   80386DX system controller. It recognizes the chip, but treats it the
   wrong way:
    - SLTPTR is 10 bits instead of 8 bits, so top of XMS is not correctly
      determined.
    - The lookup table for memory size needs to be interpreted in whole
      megabytes instead of half megabytes.

Nice-to-have:
 - Support for the alternate mapping registers
 - Support for more mapped pages (EMS 4.0 only)
 - Support for non-volatile memory (my Quadtel BIOS does not clear EMS
   during reboot)
 - Dynamic allocation of handle management and page management data.
