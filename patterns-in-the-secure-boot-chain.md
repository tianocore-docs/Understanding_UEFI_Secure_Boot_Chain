<!--- @file
  patterns-in-the-secure-boot-chain.md for Understanding the UEFI Secure Boot Chain

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
## Patterns in the Secure Boot Chain {#patterns-in-the-secure-boot-chain}

Definition:

1.  Firmware[N] - the N level firmware binary. Any firmware layer is updatable.

    Firmware[0] means the component verified by Hardware.

    Firmware[N] means the component verified by Firmware[N-1].

    It may include both code (Firmware[N].Code) and data (Firmware[N].Data).

2.  Firmware[N].Code - the code of the N level firmware binary.

    It may include the verifier (Firmware[N].Code.Verifier.)

3.  Firmware[N].Data - the data of the N level firmware binary.

    It may include the verification policy. (Firmware[N].Data.Policy.)

4.  Firmware[N].Code.Verifier - the verification function of the N level firmware binary.

5.  Firmware[N].Data.Policy - the policy data inside of the N level firmware binary. This data is used by the verification function. Both verification function and policy data have below subcategory:

    1.  Boot - the firmware boot

    2.  FirmwareUpdate - the firmware update (it may or might not include policy data)

    3.  PolicyUpdate - the policy update. It may or might not exist.

    4.  Recovery - the firmware recovery

    5.  Communication - the firmware runtime communication

6.  Hardware – the hardware, including Register Transfer Level (RTL) and register. The hardware is not updatable. The hardware must be fused when it is shipped to the end user.

There are two types of verification:

1.  The verifier for boot (verified boot). The read-only code and read-only data are in this category. This category includes both initial installation and upgrade. For example, UEFI Secure Boot is for code installation, or signed capsule update is for code/data upgrade. In most cases, the verification is based upon a crypto-algorithm, such as Secure Hash Algorithm (SHA) or Rivest-Shamir-Adleman Algorithm (RSA). The policy data can be the hash value of the firmware or the public key hash of the firmware. Above 5.a, 5.b, 5.c, 5.d belongs to this type.

2.  The verifier for communication (verified communication). The read/write data are in this category. This category is for cross-boundary data passing such as SMM communication, including the UEFI non-volatile variable. In most cases, the verification is based upon the boundary check, valid range check, etc. Above 5.e belongs to this type.

### Patterns for Verified Boot {#patterns-for-verified-boot}

Table 1-3: Patterns for Verified Boot

| **Item** | **Entity** | **Provider** | **Location** |
| --- | --- | --- | --- |
| **TP** | Firmware[N].Code.Verifier.Boot (Firmware[N].Data.Policy.Boot, Firmware[N+1]) | Firmware Owner | Same as Firmware[N] |
| **CDI** | Firmware[N] | Firmware Owner | Originally on Flash, loaded into RAM by Firmware[N-1] |
| **UDI** | Firmware[N+1] | Firmware Owner | Originally on Flash, loaded into RAM by Firmware[N] |

NOTE: If N == 0, Firmware[-1] means the hardware.

### Patterns for Verified Policy Update {#patterns-for-verified-policy-update}

Table 1-4: Patterns for Verified Policy Update

| **Item** | **Entity** | **Provider** | **Location** |
| --- | --- | --- | --- |
| **TP** | Firmware[N].Code.Verifier.PolicyUpdate (Firmware[N].Data.Policy.PolicyUpdate, Firmware[N].Data.Policy:New) | Firmware Owner |  |
| **CDI** | Firmware[N].Code.Verifier.PolicyUpdate + Firmware[N].Data.Policy.PolicyUpdate | Firmware Owner | In an isolated execution environment. As such the rest of Firmware[N] cannot tamper with it. |
| **UDI** | Firmware[N].Data.Policy:New | Policy Data Owner | Memory, loaded into an isolated environment, by Firmware[N]. Code.Verifier. PolicyUpdate |

#### Patterns for Verified Firmware Update {#patterns-for-verified-firmware-update}

Table 1-5: Patterns for Verified Firmware Update

| **Item** | **Entity** | **Provider** | **Location** |
| --- | --- | --- | --- |
| **TP** | Firmware[N].Code.Verifier.FirmwareUpdate (Firmware[N].Data.Policy.FirmwareUpdate, Firmware[N]:New) | Firmware Owner |  |
| **CDI** | Firmware[N] | Firmware Owner | Flash unlockable environment, loaded by Firmware[N-1] |
| **UDI** | Firmware[N]:New | Firmware Owner | Flash unlockable environment, loaded by original Firmware[N] |

#### Patterns for Verified Recovery {#patterns-for-verified-recovery}

Table 1-6: Patterns for Verified Recovery

| **Item** | **Entity** | **Provider** | **Location** |
| --- | --- | --- | --- |
| **TP** | Firmware[N].Code.Verifier.Recovery (Firmware[N].Data.Policy.Recovery, Firmware[N+1]:Recovery) | Firmware Owner |  |
| **CDI** | Firmware[N] | Firmware Owner | Originally on flash, loaded into RAM by Firmware[N-1] |
| **UDI** | Firmware[N+1]:Recovery | Firmware Owner | Originally on recovery storage (Flash, USB, Hard drive), loaded into RAM by Firmware[N] |

#### Patterns for Verified Runtime Communication {#patterns-for-verified-runtime-communication}

Table 1-7: Patterns for Verified Runtime Communication

| **Item** | **Entity** | **Provider** | **Location** |
| --- | --- | --- | --- |
| **TP** | Firmware[N].Code.Verifier.RuntimeCommunication (Firmware[N].Data.Policy.RuntimeCommunication, Data:New) | Firmware Owner |  |
| **CDI** | Firmware[N].Code.Verifier.RuntimeCommunication + Firmware[N].Data.Policy.RuntimeCommunication | Firmware Owner | In an isolated execution environment. As such the rest of Firmware[N] cannot tamper it. |
| **UDI** | Data:New | Any | Memory, loaded into an isolated environment, by Firmware[N]. Code.Verifier. PolicyUpdate. <br> This can be any Data, as long as the format is known by the producer and consumer.|
