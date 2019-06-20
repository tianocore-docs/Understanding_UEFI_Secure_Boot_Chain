<!--- @file
  signed-recovery.md for Understanding the UEFI Secure Boot Chain

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

## Signed Recovery {#signed-recovery}

NIST [SP800-193](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-193.pdf) defines three principles supporting platform resiliency:

*   Protection,

*   Detection

*   Recovery

Signed UEFI capsule update and Intel® BIOS Guard provide these protections. Intel® Boot Guard and OBB verification provide detection. If firmware corruption is detected, the firmware can perform recovery to prevent a permanent denial of service (PDOS) attack. EDK II implements a signed recovery (see Table 2-10).

Table 2-10: Firmware Recovery Verification

| **Item** | **Entity** | **Provider** | **Location** |
| --- | --- | --- | --- |
| **TP** | Firmware Recovery Verification | OEM | Originally on flash, loaded into DRAM. |
| **CDI** | Firmware Recovery TCB Code | OEM | Originally on flash, loaded into DRAM. |
|  | Firmware Recovery Signature Database (Policy) | OEM | Originally on flash, loaded into DRAM. |
| **UDI** | Firmware Recovery Package | OEM | Originally on external storage (e.g. Hard drive, USB, Memory, or Flash), loaded into DRAM |

#### Signing {#signing}

The UDI is provided a new firmware image, the same as the UEFI Capsule Update implementation. The entire firmware binary must be signed using the OEM private key.

#### Public Key Storage {#public-key-storage}

The OEM public key should be embedded in the original firmware &amp; recovery launcher module.

#### Verification {#verification}

If firmware corruption is detected during boot, the recovery boot path is triggered. In this scenario, TP is the firmware recovery launcher module. This module loads the recovery image from a known source and verifies the signature. If TP passes verification, the recovery image is loaded and the recovery launcher module transfers control to the recovery image. If recovery verification fails, the recovery image is discarded and the recovery launcher attempts to locate additional recovery images. If all recovery images fail verification, the recovery process is aborted.

NOTE: The signed recovery image itself may be updatable even if it is on the flash region.