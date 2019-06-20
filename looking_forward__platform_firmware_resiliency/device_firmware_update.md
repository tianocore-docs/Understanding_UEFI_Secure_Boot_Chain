<!--- @file
  device-firmware-update.md for Understanding the UEFI Secure Boot Chain

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

## Device Firmware Update {#device-firmware-update}

If the device firmware is updatable, the update must be verified.

The verifier is determined by the entity with write access to the device firmware location. The entity performing verification must be the same entity performing the update.

For example, if the device firmware is in the device internal location, which is not accessible by the host firmware, such as TPM, then the device must do the verification and update. If the device firmware is in the device internal location, but it is accessible by the host firmware, such as EC, then the host firmware may do the verification and update. If device firmware is on the external storage and loaded by system firmware, then the system firmware must do the verification and update.

Table 4-2: Device Firmware Update Verification

| **Item** | **Entity** | **Provider** | **Location** |
| --- | --- | --- | --- |
| **TP** | Firmware Update Verification | OEM or IHV | Depends |
| **CDI** | Firmware Update TCB Code | OEM or IHV | Depends |
|  | Firmware Update Signature Database (Policy) | OEM or IHV | Depends |
| **UDI** | Device Firmware Update Package | IHV | Originally on external storage (e.g. Hard drive, USB, Memory, or Read-Write Flash), loaded into device firmware unlockable environment. |