<!--- @file
  uefi-secure-boot.md for Understanding the UEFI Secure Boot Chain

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

## UEFI Secure Boot {#uefi-secure-boot}

UEFI Secure Boot is a feature defined in the UEFI Specification. It guarantees that only valid 3<sup>rd</sup> party firmware code can run in the Original Equipment Manufacturer (OEM) firmware environment. UEFI Secure Boot assumes the system firmware is a trusted entity. Any 3<sup>rd</sup> party firmware code is not trusted, including the bootloader installed by the Operating System Vendor (OSV) and peripherals provided by an Independent Hardware Vendor (IHV). The end user may choose to enroll and revoke entries in the UEFI Secure Boot image security database as part of managing verification policy.

UEFI Secure Boot includes two parts - verification of the boot image and verification of updates to the image security database. Figure 2-1 shows the UEFI Secure Boot verification flow. Table 2-1 shows the key/image security database used in UEFI Secure Boot.

![](/media/image2.png)

###### Figure 2-1: UEFI Secure Boot{#2-1-uefi-secure-boot}

Table 2-1: Key Usage in UEFI Secure Boot

| **Key** | **Verifies** | **Update is verified by** | **NOTES** |
| --- | --- | --- | --- |
| PK | New PK <br>New KEK <br>New db/dbx/dbt/dbr <br>New OsRecoveryOrder <br>New OsRecovery#### | PK | Platform Key |
| KEK | New db/dbx/dbt/dbr <br>New OsRecoveryOrder <br>New OsRecovery#### | PK | Key Exchange Key |
| db | UEFI Image | PK/KEK | Authorized Image Database |
| dbx | UEFI Image | PK/KEK | Forbidden Image Database |
| dbt | UEFI Image + dbx | PK/KEK | Timestamp Database |
| dbr | New OsRecoveryOrder <br>New OsRecovery#### | PK/KEK | Recovery Database |

### UEFI Secure Boot Image Verification {#uefi-secure-boot-image-verification}

Table 2-2: UEFI Secure Boot Image Verification

| **Item** | **Entity** | **Provider** | **Location** |
| --- | --- | --- | --- |
| **TP** | UEFI Secure Boot Image Verification | OEM | Originally on flash, loaded into DRAM |
| **CDI** | Manufacture Firmware Code | OEM | Originally on flash, loaded into DRAM |
|  | UEFI Secure Boot Image Security Database (Policy) | End user (or OEM default) | Originally on flash, authenticated variable region, loaded into DRAM |
| **UDI** | 3<sup>rd</sup> party Firmware Code, (OS boot loader) | OSV | Originally on external storage (e.g. Hard drive, USB), loaded into DRAM |
|  | 3<sup>rd</sup> party Firmware Code, (PCI Option ROM) | IHV | Originally on PCI card, loaded into DRAM |
|  | 3<sup>rd</sup> party Firmware Code, (UEFI Shell Tool) | Any | External Storage (e.g. hard drive, USB), loaded into DRAM |

Table 2-2 shows the component involved in the UEFI Secure Boot Image Verification.

#### Signing {#signing}

In UEFI Secure Boot, the UDI is any 3<sup>rd</sup> part firmware code, including the OS boot loader, PCI option ROMs, or a UEFI shell tool. The component provider needs to sign these components with a private key and publish the public key.

#### Public Key Storage {#public-key-storage}

The OEM or end user may enroll the public key as a CDI (UEFI Secure Boot Image Security Database). The database is in a UEFI Authenticated Variable region. The database can also be

updated during runtime. It can be read by anyone but only be written after data authentication. See Table 2 below.

#### Verification {#verification}

During boot, the TP (Image Verification Procedure) verifies the UDI (3<sup>rd</sup> party firmware code), according to the CDI (UEFI Secure Boot Image Security Database) as policy. If the verification passes, the UDI is transformed into a CDI and the 3<sup>rd</sup> party firmware code is executed. If the verification fails, the 3<sup>rd</sup> party firmware code is discarded.

Figure 2-2 shows a verification flow using db/dbx.

![](/media/image3.png)

###### Figure 2-2: Image Verification flow{#2-2-image-verification-flow}

Figure 2-3 shows a verification flow introducing dbt. An additional check is required based dbx signature.

![](/media/image4.png)

###### Figure 2-3: Image Verification with timestamp signature database{#2-3-image-verification-with-timestamp-signature-database}

### UEFI Authenticated Variable Verification (Policy Update) {#uefi-authenticated-variable-verification-policy-update}

Table 2-3: UEFI Authenticated Variable Verification

| **Item** | **Entity** | **Provider** | **Location** |
| --- | --- | --- | --- |
| **TP** | UEFI Authenticated Variable Verification | OEM | Originally on flash, loaded into SMRAM |
| **CDI** | Manufacture Firmware Code in SMM. | OEM | Originally on flash, loaded into SMRAM |
|  | UEFI Secure Boot Image Security Database (Policy) | End user (or OEM default) | Originally on flash, loaded into SMRAM |
| **UDI** | New UEFI Secure Boot Image Security Database | End user | Originally in normal DRAM, loaded into SMRAM |

In Table 2-2, the CDI (UEFI Secure Boot Image Security Database) is updatable. The database itself is in the UEFI Authenticated Variable region. Table 2-3 shows the component involved in the UEFI Authenticated Variable Verification.

#### Signing {#signing-0}

To update the existing Image Security Database (CDI), the new Image Security Database (UDI) needs to be signed if UEFI Secure Boot is enabled.

#### Public Key Storage {#public-key-storage-0}

The signer’s public key must be enrolled in system firmware. It is the same as the public key used for UEFI Secure Boot Image Verification. The database is stored in a UEFI Authenticated Variable region.

#### Verification {#verification-0}

During runtime update, the TP (Authenticated Variable Verification Procedure) verifies the UDI (new Image Security Database), according to the CDI (UEFI Secure Boot Image Security Database) as policy. If verification passes, then the UDI is transformed into a CDI, and the new Image Security Database takes effect on the next boot. If verification fails, the new Image Security Data is discarded.

For details on the authenticated variable flow, please refer to the “Implementing

UEFI Authenticated Variables in SMM with EDK II” whitepaper.