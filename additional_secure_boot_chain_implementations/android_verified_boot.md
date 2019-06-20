<!--- @file
  android-verified-boot.md for Understanding the UEFI Secure Boot Chain

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

## Android Verified Boot {#android-verified-boot}

The Android verified boot solution, like UEFI Secure Boot, is used to verify the integrity of an OS image.

_“Verified Boot strives to ensure all executed code comes from a trusted source (usually device OEMs), rather than from an attacker or corruption. It establishes a full chain of trust, starting from a hardware-protected root of trust to the bootloader, to the boot partition and other verified partitions including system, vendor, and optionally OEM partitions. During device boot up, each stage verifies the integrity and authenticity of the next stage before handing over execution.”_

_-- “Verified Boot” ([source.android.com](https://source.android.com/security/verifiedboot))_

![](/media/image11.png)

###### Figure 3-3: Android Verified Boot 1.0 without A/B (source: [Android Verified Boot 2.0](https://blog.csdn.net/rikeyone/article/details/80606147)){#3-3-android-verified-boot-1-0-without-a-b-source-android-verified-boot-2-0}

![](/media/image12.png)

###### Figure 3-4: Android Verified Boot 1.0 with A/B (source: [Android Verified Boot 2.0](https://blog.csdn.net/rikeyone/article/details/80606147)){#3-4-android-verified-boot-1-0-with-a-b-source-android-verified-boot-2-0}

![](/media/image13.png)

###### Figure 3-5: Android Verified Boot 2.0 (source: [Android Verified Boot 2.0](https://blog.csdn.net/rikeyone/article/details/80606147)){#3-5-android-verified-boot-2-0-android-verified-boot-2-0}

For additional information on OS kernel verification, see the following:

*   [https://source.android.com/security/verifiedboot](https://source.android.com/security/verifiedboot)
*   [https://android.googlesource.com/platform/external/avb/+/master/README.md](https://android.googlesource.com/platform/external/avb/+/master/README.md)<Br>
[https://blog.csdn.net/rikeyone/article/details/80606147](https://blog.csdn.net/rikeyone/article/details/80606147)