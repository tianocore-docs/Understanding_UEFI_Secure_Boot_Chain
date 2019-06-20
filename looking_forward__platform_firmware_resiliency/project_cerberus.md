<!--- @file
  project-cerberus.md for Understanding the UEFI Secure Boot Chain

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

## Project Cerberus {#project-cerberus}

As part of the Open Compute Project (OCP), Project Cerberus defines a hierarchical Root of Trust (RoT) architecture. All active components are required to support both hardware and firmware combined identifing through the Device Identifier Composition Engine (DICE).

Figure 4-3 thru 4-6 describe the power on sequence, boot flow, recovery flow, and firmware update flow.

![](/media/image16.png)

###### Figure 4-3: Cerberus power on sequence (source: “[Project Cerberus Hardware Security](https://f990335bdbb4aebc3131-b23f11c2c6da826ceb51b46551bfafdc.ssl.cf2.rackcdn.com/images/fbbdd5feceb6e6328373417e1ab7c06a13a2ef2c.pdf)”){#4-3-cerberus-power-on-sequence-source-project-cerberus-hardware-security}

![](/media/image17.png)

###### Figure 4-4: Cerberus boot flow (source: “[Project Cerberus Hardware Security](https://f990335bdbb4aebc3131-b23f11c2c6da826ceb51b46551bfafdc.ssl.cf2.rackcdn.com/images/fbbdd5feceb6e6328373417e1ab7c06a13a2ef2c.pdf)”){#4-4-cerberus-boot-flow-source-project-cerberus-hardware-security}

![](/media/image18.png)

###### Figure 4-5: Cerberus recovery flow (source: “[Project Cerberus Hardware Security](https://f990335bdbb4aebc3131-b23f11c2c6da826ceb51b46551bfafdc.ssl.cf2.rackcdn.com/images/fbbdd5feceb6e6328373417e1ab7c06a13a2ef2c.pdf)”){#4-5-cerberus-recovery-flow-source-project-cerberus-hardware-security}

![](/media/image19.png)![](/media/image20.png)

###### Figure 4-6: Cerberus firmware update (source: “[Project Cerberus Hardware Security](https://f990335bdbb4aebc3131-b23f11c2c6da826ceb51b46551bfafdc.ssl.cf2.rackcdn.com/images/fbbdd5feceb6e6328373417e1ab7c06a13a2ef2c.pdf)”){#4-6-cerberus-firmware-update-source-project-cerberus-hardware-security}

The concept of Cerberus is similar to Intel® Boot Guard., but there are several key differences:

1.  Intel® Boot Guard uses Microcode as RoT, while Cerberus uses a dedicated RoT device.
2.  Intel® Boot Guard can mitigate hardware bus attacks.
3.  Intel® Boot Guard only verifies the host system firmware, while Cerberus verifies all boot firmware (platform firmware, BMC, etc.)
4.  Cerberus defines a detailed flow for update and recovery.

Table 4-3: Cerberus Boot

| **Item** | **Entity** | **Provider** | **Location** |
| --- | --- | --- | --- |
| **TP** | Boot Firmware Verification (in Cerberus Microcontroller) | OEM | Flash (Read Only Code), Device ROM. |
| **CDI** | Cerberus Microcontroller | OEM | Flash (Read Only Code), Device ROM. |
|  | Boot Firmware Signature Database (Policy) | OEM | Flash (Read Only Data), ROM |
| **UDI** | Boot Firmware (BMC, Firmware) | OEM/IHV | Flash (Read Only Data) – active area |

Table 4-4: Cerberus Recovery

| **Item** | **Entity** | **Provider** | **Location** |
| --- | --- | --- | --- |
| **TP** | Boot Firmware Verification (in Cerberus Microcontroller) | OEM | Flash (Read Only Code), Device ROM. |
| **CDI** | Cerberus Microcontroller | OEM | Flash (Read Only Code), Device ROM. |
|  | Boot Firmware Signature Database (Policy) | OEM | Flash (Read Only Data), ROM |
| **UDI** | Boot Firmware Recovery (BMC, Firmware) | OEM/IHV | Flash (Read Only Data) - recovery area |

Table 4-5: Cerberus Firmware Update

| **Item** | **Entity** | **Provider** | **Location** |
| --- | --- | --- | --- |
| **TP** | Boot Firmware Verification (in Cerberus Microcontroller) | OEM | Flash (Read Only Code), Device ROM. |
| **CDI** | Cerberus Microcontroller | OEM | Flash (Read Only Code), Device ROM. |
|  | Boot Firmware Signature Database (Policy) | OEM | Flash (Read Only Data), ROM |
| **UDI** | Boot Firmware (BMC, Firmware) | OEM/IHV | Flash (Read Only Data) – staging area |