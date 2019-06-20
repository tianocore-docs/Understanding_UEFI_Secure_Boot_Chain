<!--- @file
  coreboot.md for Understanding the UEFI Secure Boot Chain

  Copyright (c) 2019, Intel Corporation. All rights reserved.<BR>

  Redistribution and use in source (original document form) and 'compiled'
  forms (converted to PDF, epub, HTML and other formats) with or without
  modification, are permitted provided that the following conditions are met:

  1) Redistributions of source code (original document form) must retain the
     above copyright notice, this list of conditions and the following
     disclaimer as the first lines of this file unmodified.

  2) Redistributions in compiled form (transformed to other DTDs, converted to
     PDF, epub, HTML and other formats) must reproduce the above copyright
     notice, this list of conditions and the following disclaimer in the
     documentation and/or other materials provided with the distribution.

  THIS DOCUMENTATION IS PROVIDED BY TIANOCORE PROJECT "AS IS" AND ANY EXPRESS OR
  IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF
  MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO
  EVENT SHALL TIANOCORE PROJECT  BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
  SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
  PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS;
  OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY,
  WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR
  OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS DOCUMENTATION, EVEN IF
  ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

-->

## coreboot {#coreboot}

The open source [coreboot](https://coreboot.org) firmware project implements [verified boot](https://doc.coreboot.org/security/vboot/index.html?highlight=verified%20boot), which is similar to a combination of OBB verification and UEFI Secure Boot.

Figure 3-2 shows the verified boot flow. Table 3-2 shows keys used in the verified boot flow.

![](/media/image9.png)

###### Figure 3-2: coreboot Verified Boot (source: “[Verified Boot in Chrome OS and how to make it work for you](https://static.googleusercontent.com/media/research.google.com/en/pubs/archive/42038.pdf)”){#3-2-coreboot-verified-boot-source-verified-boot-in-chrome-os-and-how-to-make-it-work-for-you}



Table 3-2: Keys used by coreboot verified boot (source: “[Verified Boot: Surviving in the Internet of Insecure Things](https://www.coreboot.org/images/c/ce/Verified_Boot_-_Surviving_in_the_Internet_of_Insecure_Things.pdf)”)



| **Key** | **Verifies** | **Stored in** | **Versioned** | **Notes** |
| --- | --- | --- | --- | ---|
|Root Key    |   Firmware Data Key |   RO Firmware |  NO  | Private key in a locked room guarded by laser sharks; N of M present. RSA4096+    |
|Firmware Data Key    | RW Firmware    | RW FW Header   |  YES  | Private key on signing server. RSA4096.   |
| Kernel Subkey   |  Kernel Data Key  | RW Firmware   | YES (as FW)   | Private key only needed to sign new kernel data key. RSA4096.   |
| Kernel Data Key   | OS Kernel  |   OS kernel Header | YES   |  Private key on signing server. RSA2048.  |
| Recovery Key   | Recovery OS Kernel   |  RO Firmware  |  NO  | Locked room and laser sharks. RSA4096+. <br>Different than all keys above.<br>Signs recovery installer, not payload.   |


Table 3-3: coreboot Verified Boot (for firmware)

| **Item** | **Entity** | **Provider** | **Location** |
| --- | --- | --- | --- |
| **TP** | Read/Write Firmware Verification | OEM | Flash (Read Only Region) |
| **CDI** | Read-Only Firmware | OEM | Flash (Read Only Region) |
|  | Root key | OEM | RO firmware, Google Binary Blob (GBB) |
| **UDI** | Read/Write Firmware | OEM | Flash (Read Write Region) |

Table 3-4: coreboot Verified Boot (for OS)

| **Item** | **Entity** | **Provider** | **Location** |
| --- | --- | --- | --- |
| **TP** | OS Kernel Verification | OEM | Flash (Read Write Region) |
| **CDI** | Read-Write Firmware | OEM | Flash (Read Write Region) |
|  | Kernel Subkey | OSV | R/W firmware, Google Binary Blob (GBB) |
| **UDI** | OS Kernel | OSV | External storage |