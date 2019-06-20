<!--- @file
  device-firmware-boot.md for Understanding the UEFI Secure Boot Chain

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

## Device Firmware Boot {#device-firmware-boot}

If device firmware is not in TCB, it must be verified by the system firmware or device firmware in TCB.

During system boot, host firmware may choose to verify some device firmware components. For device firmware stored in the device’s internal storage, verification may happen based upon device policy. For device firmware images in external storage loaded at runtime, verification is mandatory. Device firmware verification may follow the same rules as the system firmware verification. Device firmware is only loaded after it is verified.

Table 4-1: Device Firmware Boot Verification

| **Item** | **Entity** | **Provider** | **Location** |
| --- | --- | --- | --- |
| **TP** | Device Firmware Verification | OEM or IHV | Flash (Read Only Code), Device ROM. |
| **CDI** | System Firmware or Device firmware TCB | OEM or IHV | Flash (Read Only Code), ROM |
|  | Device Firmware Signature Database (Policy) | OEM or IHV | Flash (Read Only Data), ROM |
| **UDI** | Device Firmware | IHV | Device Internal Storage (or)<br>External Storage (e.g. Hard drive, USB, Memory, or Read-Write Flash)  |