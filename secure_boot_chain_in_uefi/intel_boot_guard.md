<!--- @file
 intel-boot-guard.md for Understanding the UEFI Secure Boot Chain

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

## Intel® Boot Guard {#intel-boot-guard}

UEFI Secure Boot assumes the OEM platform firmware is a Trusted Computing Base (TCB) and trusts it implicitly. A better implementation relies on a smaller TCB to verify the OEM platform firmware. A solution can be implemented using [Intel® Boot Guard](https://downloads.dell.com/solutions/servers-solution-resources/Direct%20from%20Development%20-%20Cyber-Resiliency%20In%20Chipset%20and%20BIOS.pdf). This feature verifies the entire OEM platform firmware image using two components:

*   Authenticated Code Module (ACM) Initial Boot Block (IBB) Verification

*   Microcode ACM Verification.

Figure 2-4 shows the components involved in Intel® Boot Guard. Table 2-4 shows the key usage in Intel® Boot Guard.

![](/media/image5.png)

###### Figure 2-4: Intel® Boot Guard diagram (credit: “[CYBER-RESILIENCY IN CHIPSET AND BIOS](https://downloads.dell.com/solutions/servers-solution-resources/Direct%20from%20Development%20-%20Cyber-Resiliency%20In%20Chipset%20and%20BIOS.pdf)” by Dell EMC){#2-4-intel-boot-guard-diagram-credit-cyber-resiliency-in-chipset-and-bios}

Table 2-4: Key Usage in Intel® Boot Guard

| **Key** | **Verifies** | **Storage** | **Verified By** |
| --- | --- | --- | --- |
| ACM Key | ACM | CPU | Microcode |
| Key Hash | Key Manifest | PCH | ACM |
| BP Key | Boot Policy Manifest | Key Manifest (Flash) | ACM |
| IBB Hash | IBB | Boot Policy Manifest (Flash) | ACM |

Please note that Intel Boot Guard is not the only solution available for OEM platform firmware verification. This document uses it as an example to illustrate the concept.

Table 2-5 shows how to reduce TCB from OEM platform firmware to ACM.

### ACM IBB Verification {#acm-ibb-verification}

Table 2-5: ACM IBB Verification

| **Item** | **Entity** | **Provider** | **Location** |
| --- | --- | --- | --- |
| **TP** | ACM IBB Verification | Intel | Originally on flash, loaded into Authenticated Code RAM (AC-RAM) |
| **CDI** | ACM Code | Intel | Originally on flash, loaded into AC-RAM |
|  | Boot Policy Manifest (Policy) | OEM | Originally on flash, loaded into cache |
|  | Key Manifest (Policy) | OEM | Originally on flash, loaded into cache |
|  | Key Hash (Policy) | OEM | Write once PCH register, programmed in manufacture fuse. |
| **UDI** | Firmware Initial Boot Block, aka IBB | OEM | Originally on flash, loaded into cache |

Intel introduced the Intel® Boot Guard Authenticated Code Module (ACM), which is a module signed by Intel. The ACMs modules assume responsibility to verify OEM platform firmware before the host CPU transfers control to OEM firmware. Because verifying the entire image is time-consuming, the ACM only verifies the initial boot block (IBB) code. The IBB is then responsible for verifying the OEM boot block (OBB).

#### Signing {#signing}

The UDI here is the firmware IBB, so only the IBB needs to be signed.

#### Public Key Storage {#public-key-storage}

Intel® Boot Guard defines a set of Manifests to record the signature information.

1.  Boot Policy Manifest – It records the hash of IBB and is signed by the Key Manifest Key.

2.  Key Manifest – It records a set of hashes for the public key pair which signs the Boot Policy Manifest, and it is signed Boot Guard Key.

3.  Key Hash - It records the hash for the public key pair which signs the Key Manifest. It is provisioned into the PCH hardware.

The Key Hash is read-only. It cannot be updated.

The Boot Policy Manifest and Key Manifest can be updated in the firmware.

#### Verification {#verification}

During runtime update, the TP – ACM IBB Verification gets the CDI - Key Hash from PCH - and verify the first UDI – the Key Manifest. If the verification passes, the Key Manifest is transformed into a CDI. Then ACM continues to get the key hash from the CDI - Key Manifest - and verify the UDI - Boot Policy Manifest. If the verification passes, the Boot Policy Manifest is transformed into a CDI. Then the ACM gets the final UDI – Firmware IBB code - and verify it according to the CDI – Boot Policy Manifest. If the final verification passes, then the Firmware IBB is transformed into a CDI, and the ACM transfers control to the IBB.

### Microcode ACM Verification {#microcode-acm-verification}

The ACM binary is signed by Intel. Now the question becomes who verifies the ACM binary. The answer is the CPU Microcode.

Table 2-6: Microcode ACM Verification

| **Item** | **Entity** | **Provider** | **Location** |
| --- | --- | --- | --- |
| **TP** | Microcode ACM Verification | Intel | CPU |
| **CDI** | Microcode | Intel | CPU |
|  | ACM Key hash | Intel | CPU |
| **UDI** | ACM Code | Intel | Originally on flash, loaded into AC-RAM |

#### Signing {#signing-0}

The UDI is the ACM binary. As such, the ACM needs to be signed with the Intel key.

#### Public Key Storage {#public-key-storage-0}

The hash of the ACM public key is inside of the CPU. A debug ACM is signed with the debug key. A production ACM is signed with the production key.

The policy can NOT be updated.

#### Verification {#verification-0}

During the ACM launch, the CPU Microcode loads the UDI - ACM to authenticated code execution area. Then the TP – ACM verification performs the verification. If the verification passes, then the UDI is transformed to CDI, the ACM starts executing. If the verification fails, the TXT shutdown is signaled.

The Intel® Boot Guard is one implementation to support boot ROM verification. Some other projects may have similar functions, such as [Cerberus](https://github.com/opencomputeproject/Project_Olympus/blob/master/Project_Cerberus).

### OBB Verification {#obb-verification}

Intel® Boot Guard only verifies the initial boot block (IBB) of the whole OEM Firmware. To make sure the whole OEM Firmware is unmodified, the IBB needs to verify the reset OEM boot block (OBB).

Table 2-7: OBB Verification

| **Item** | **Entity** | **Provider** | **Location** |
| --- | --- | --- | --- |
| **TP** | OBB Verification | OEM | Originally on flash, loaded into DRAM |
| **CDI** | Firmware Initial Boot Block, aka IBB | OEM | Originally on flash, loaded into DRAM |
|  | OBB Hash, OBB public key hash (Policy) | OEM | Originally on flash, loaded into DRAM |
| **UDI** | Firmware OEM Boot Block, aka OBB | OEM | Originally on flash, loaded into DRAM |

#### Signing {#signing-1}

The UDI is OBB, which is not verified by IBB. Since both IBB and OBB are provided by OEM, the OEM may define a separate specific format to sign the OBB.

#### Public Key Storage {#public-key-storage-1}

The OBB public key hash must be stored into the IBB region to make sure it is validated by ACM. As implementation choice, OEM may store the OBB hash directly to the IBB without using the public key.

#### Verification {#verification-1}

During Firmware boot, the TP is the OBB verification code inside of IBB. If the OBB passes the verification, the OBB is installed by IBB. If the OBB fails the verification, the OBB is skipped.