<!--- @file
  platform-firmware-resiliency.md for Understanding the UEFI Secure Boot Chain

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

## Platform Firmware Resiliency {#platform-firmware-resiliency}

In modern platforms, system firmware is only one of multiple firmware images. Most system components rely on some form of device firmware. The scope of PFR covers both system firmware and device firmware images, so the trust chain is maintained for all boot firmware components. See Figure 4-1 for an overview diagram.

![](/media/image14.png)

###### Figure 4-1: Component and Trust Chain, from NIST [SP800-193](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-193.pdf){#4-1-component-and-trust-chain-from-nist-sp800-193}

Device firmware may exist in a device-specific region that is managed by the device. In some cases, device firmware may reside in the same location as the system firmware, such as Serial Peripheral Interface (SPI) attached to flash, and the system firmware is responsible for loading the device firmware into a device firmware region.

Most device firmware initializes the hardware so it is functional at runtime. Examples include:

*   Network Interface Card (NIC)
*   Solid State Drive (SSD)
*   Universal Serial Bus (USB)
*   Battery management

Some device firmware is involved in the system boot process and may play an important role in system firmware verification. Examples include:

*   Embedded Controller (EC) firmware
*   Baseboard Management Controller (BMC) firmware
*   Intel® Converged Security and Management Engine (Intel® CSME)
*   Glue logic in a Field Programmable Gate Array (FPGA) or Complex Programmable Logic Device (CPLD)

There are multiple existing standards describing device authentication, including:

*   [PCIe Device Security](https://www.intel.com/content/www/us/en/io/pci-express/pcie-device-security-enhancements-spec.html)
*   [USB Authentication](https://www.usb.org/document-library/usb-authentication-specification-rev-10-ecn-and-errata-through-january-7-2019)
*   Security Protocol and Data Model ([SPDM](https://www.dmtf.org/sites/default/files/standards/documents/DSP0274_0.9.0a.pdf))

Figure 4-2 shows a high-level view of an authentication protocol.

![](/media/image15.png)

###### Figure 4-2: High-level View of PCIe® Component Authentication (source: [PCIe® Component Authentication](https://pcisig.com/pcie%C2%AE-component-authentication)){#4-2-high-level-view-of-pcie-component-authentication-source-pcie-component-authentication}
