<!--- @file
  smm-runtime-communication.md for Understanding the UEFI Secure Boot Chain

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

## SMM Runtime Communication {#smm-runtime-communication}

System Management Mode (SMM) is a special highly privileged processor execution mode. One usage of SMM is that the Firmware may provide some special service in SMM, which is referred to as an SMI handler. The SMI handler uses a shared buffer ([SMM Communication Buffer](https://github.com/tianocore-docs/Docs/raw/master/White_Papers/A_Tour_Beyond_BIOS_Secure_SMM_Communication.pdf)), to convey information to the service consumer during OS runtime. Table 2-11 describes SMM Runtime Communication Verification.

Table 2-11: SMM Runtime Communication Verification

| **Item** | **Entity** | **Provider** | **Location** |
| --- | --- | --- | --- |
| **TP** | SMM Communication Verifier Code | OEM | Originally on flash, loaded in SMRAM |
| **CDI** | SMI handler | OEM | Originally on flash, loaded in SMRAM |
| **UDI** | SMM communication buffer | Any | DRAM |

The SMM communication buffer is not signed because any program may use the buffer to invoke SMM services. SMM communication is treated as an attack surface, so the SMI handler must verify the contents of the SMM communication buffer. Since there is no signature, common verification is limited to prevent SMM attacks since it cannot verify the originator.