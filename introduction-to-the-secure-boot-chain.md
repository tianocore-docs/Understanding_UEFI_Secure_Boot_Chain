<!--- @file
  introduction-to-the-secure-boot-chain.md for Understanding the UEFI Secure Boot Chain

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


## Introduction to the Secure Boot Chain {#introduction-to-the-secure-boot-chain}

According to NIST SP800-147 and SP800-193, the system needs to maintain integrity and availability during the firmware boot process. In firmware, secure boot (aka verified boot) uses a set of policy objects to verify the next entity before execution. For example, to match C5, the system uses the TP (verification procedure) to verify the UDI (untrusted firmware component), transforms the UDI into a CDI (trusted firmware component), and executes it.

In contrast, a trusted boot (aka measured boot) process does not verify the next entity. It only records the digest of the next boot entity to a trusted location, such as a Platform Configuration Register (PCR) in the Trusted Platform Module (TPM). This allows a trusted boot chain to be verified later in the boot process. Many security models use secure boot and trusted boot capabilities in combination for maximum effectiveness.

Table 1-2: Clark-Wilson model in Firmware

| **Property** | **Description** | **Rule** | **Firmware Secure Boot** |
| --- | --- | --- | --- |
| **Integrity** | An assurance that CDIs can only be modified in constrained ways to produce valid CDIs. | C1, C2, C5, E1, E4 | Yes. Firmware needs to verify the next component |
| **Access Control** | The ability to control access to resources. | C3, E2, E3 | No. There is no user concept in secure boot. |
| **Auditing** | The ability to ascertain the changes made to CDIs and ensure that the system is in a valid state. | C1, C4 | Yes, if TCG trusted boot is enabled. TCG event log may record such information. |
| **Accountability** | The ability to uniquely associate users with their actions. | E3. | No. There is no user concept in secure boot. |## Introduction to the Secure Boot Chain {#introduction-to-the-secure-boot-chain}

According to NIST SP800-147 and SP800-193, the system needs to maintain integrity and availability during the firmware boot process. In firmware, secure boot (aka verified boot) uses a set of policy objects to verify the next entity before execution. For example, to match C5, the system uses the TP (verification procedure) to verify the UDI (untrusted firmware component), transforms the UDI into a CDI (trusted firmware component), and executes it.

In contrast, a trusted boot (aka measured boot) process does not verify the next entity. It only records the digest of the next boot entity to a trusted location, such as a Platform Configuration Register (PCR) in the Trusted Platform Module (TPM). This allows a trusted boot chain to be verified later in the boot process. Many security models use secure boot and trusted boot capabilities in combination for maximum effectiveness.

Table 1-2: Clark-Wilson model in Firmware

| **Property** | **Description** | **Rule** | **Firmware Secure Boot** |
| --- | --- | --- | --- |
| **Integrity** | An assurance that CDIs can only be modified in constrained ways to produce valid CDIs. | C1, C2, C5, E1, E4 | Yes. Firmware needs to verify the next component |
| **Access Control** | The ability to control access to resources. | C3, E2, E3 | No. There is no user concept in secure boot. |
| **Auditing** | The ability to ascertain the changes made to CDIs and ensure that the system is in a valid state. | C1, C4 | Yes, if TCG trusted boot is enabled. TCG event log may record such information. |
| **Accountability** | The ability to uniquely associate users with their actions. | E3. | No. There is no user concept in secure boot. |## Introduction to the Secure Boot Chain {#introduction-to-the-secure-boot-chain}

According to NIST SP800-147 and SP800-193, the system needs to maintain integrity and availability during the firmware boot process. In firmware, secure boot (aka verified boot) uses a set of policy objects to verify the next entity before execution. For example, to match C5, the system uses the TP (verification procedure) to verify the UDI (untrusted firmware component), transforms the UDI into a CDI (trusted firmware component), and executes it.

In contrast, a trusted boot (aka measured boot) process does not verify the next entity. It only records the digest of the next boot entity to a trusted location, such as a Platform Configuration Register (PCR) in the Trusted Platform Module (TPM). This allows a trusted boot chain to be verified later in the boot process. Many security models use secure boot and trusted boot capabilities in combination for maximum effectiveness.

Table 1-2: Clark-Wilson model in Firmware

| **Property** | **Description** | **Rule** | **Firmware Secure Boot** |
| --- | --- | --- | --- |
| **Integrity** | An assurance that CDIs can only be modified in constrained ways to produce valid CDIs. | C1, C2, C5, E1, E4 | Yes. Firmware needs to verify the next component |
| **Access Control** | The ability to control access to resources. | C3, E2, E3 | No. There is no user concept in secure boot. |
| **Auditing** | The ability to ascertain the changes made to CDIs and ensure that the system is in a valid state. | C1, C4 | Yes, if TCG trusted boot is enabled. TCG event log may record such information. |
| **Accountability** | The ability to uniquely associate users with their actions. | E3. | No. There is no user concept in secure boot. |