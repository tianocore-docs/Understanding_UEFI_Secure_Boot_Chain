<!--- @file
  machine-owner-key-mok.md for Understanding the UEFI Secure Boot Chain

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

## Machine Owner Key (MOK) {#machine-owner-key-mok}

Multiple Linux distributions have implemented UEFI Secure Boot, but this creates problems deploying 3<sup>rd</sup> party modules and custom-built kernels alongside components signed by the UEFI certificate Authority (CA). The Machine Owner Key [MOK](https://wiki.ubuntu.com/UEFI/SecureBoot) concept can be used with a signed shim loader to enable key management at the user/sysadmin level.

Figure 3-1 and Table 3-1 provide an overview of MOK.

![](/media/image8.png)

###### Figure 3-1: Linux MOK Boot, (source: “[UEFI Secure Boot Webinar](https://www.suse.com/media/presentation/uefi_secure_boot_webinar.pdf)”){#3-1-linux-mok-boot-source-uefi-secure-boot-webinar}

Table 3-1: Linux MOK Boot

| **Item** | **Entity** | **Provider** | **Location** |
| --- | --- | --- | --- |
| **TP** | OS Kernel Verification | OSV | External storage |
| **CDI** | Shim | OSV | External storage |
|  | MOK list | User | Variable |
| **UDI** | OS Kernel | User | External storage |