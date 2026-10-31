# LineageOS 23.2 for the Galaxy S21 Exynos (SM-G991B)

Unofficial LineageOS 23.2 (Android 16) builds for the Galaxy S21 Exynos (`o1s`), with VoLTE, eSIM (OpenEUICC), 60 fps video, a WPA3 hotspot and more. SELinux enforcing, signed with my own release keys.

Downloads are on the [Releases](../../releases) page. There are three variants; pick one (switching between them needs a clean install, i.e. Format data):

| File | What it is |
|---|---|
| `…-o1s-NG.zip` | No Google apps |
| `…-o1s-MTG.zip` | With the minimal MindTheGapps set (Play Store, Play Services) |
| `…-o1s-AMTG.zip` | MTG plus the full Google suite: Google app ("Hey Google", Circle to Search) and Pixel apps (Phone, Messages, Contacts, Gboard, Calendar, Clock, Photos, Android System Intelligence). First release: `lineage-23.2-20261021-amtg` |
| `recovery.tar` | LineageOS recovery for Odin (works for all variants) |
| `SHA256SUMS` | Checksums |

Installation, known issues and support: see the XDA thread.

## Source code
Every release has a tag with the same name in the source repos below, pointing at exactly the commits that were built. Branches named `next-…` may move ahead of the last build.

| Release | Device tree o1s | universal2100-common | Kernel | Extra |
|---|---|---|---|---|
| `lineage-23.2-20261006` | – | – | [`lineage-23.2-20261006`](https://github.com/Macktherealonereally/android_kernel_samsung_universal2100/tree/lineage-23.2-20261006) | – |
| `lineage-23.2-20261020` (MTG hotfix) | [tag](https://github.com/Macktherealonereally/android_device_samsung_o1s/tree/lineage-23.2-20261020) | [tag](https://github.com/Macktherealonereally/android_device_samsung_universal2100-common/tree/lineage-23.2-20261020) | same as 20261006 | frameworks/base patch |
| `test-2026-10-21` (NG, MTG) | [tag](https://github.com/Macktherealonereally/android_device_samsung_o1s/tree/test-2026-10-21) | [tag](https://github.com/Macktherealonereally/android_device_samsung_universal2100-common/tree/test-2026-10-21) | same as 20261006 | frameworks/base patch, vendor_mack-apps |
| `lineage-23.2-20261021-amtg` (AMTG) | [tag](https://github.com/Macktherealonereally/android_device_samsung_o1s/tree/lineage-23.2-20261021-amtg) | [tag](https://github.com/Macktherealonereally/android_device_samsung_universal2100-common/tree/lineage-23.2-20261021-amtg) | same as 20261006 | frameworks/base patch, vendor_mack-apps, vendor_amtg |
| `lineage-23.2-20261031` (NG, MTG, AMTG) | NG/MTG: [tag](https://github.com/Macktherealonereally/android_device_samsung_o1s/tree/lineage-23.2-20261031); AMTG: [tag](https://github.com/Macktherealonereally/android_device_samsung_o1s/tree/lineage-23.2-20261031-amtg) | [tag](https://github.com/Macktherealonereally/android_device_samsung_universal2100-common/tree/lineage-23.2-20261031) | [tag](https://github.com/Macktherealonereally/android_kernel_samsung_universal2100/tree/lineage-23.2-20261031) | frameworks/base patches, [Settings](https://github.com/Macktherealonereally/android_packages_apps_Settings/tree/lineage-23.2-20261031), [Aperture](https://github.com/Macktherealonereally/android_packages_apps_Aperture/tree/lineage-23.2-20261031), vendor_mack-apps, vendor_amtg (AMTG only) |

- Device trees: forks of the exy2100 trees, [android_device_samsung_o1s](https://github.com/Macktherealonereally/android_device_samsung_o1s) and [android_device_samsung_universal2100-common](https://github.com/Macktherealonereally/android_device_samsung_universal2100-common). Working branches: o1s `next-2026-10-31` (NG/MTG) and `next-amtg-2026-10-31` (AMTG), common `next-2026-10-31`.
- Kernel: [android_kernel_samsung_universal2100](https://github.com/Macktherealonereally/android_kernel_samsung_universal2100), branch `lineage-23.2-20261006` (releases up to 20261021) and `lineage-23.2-20261031` (adds the charging-voltage fix).
- OpenEUICC (GPLv3): [OpenEUICC fork, branch `lineage-23.2-20261006`](https://gitea.angry.im/Macktherealonereally/OpenEUICC/src/branch/lineage-23.2-20261006) (used by all releases so far).
- frameworks/base (MTG and AMTG builds, from 20261020 on): one patch on LineageOS `lineage-23.2`, [privapp-updated-allowlist](https://github.com/Macktherealonereally/galaxy-s21-exynos-lineageos-fixes/tree/main/patches/lineage-frameworks-base/privapp-updated-allowlist). It lets Play services updated from the Play Store get the privileged permissions our allowlist grants it. This is a deliberate change from AOSP, made only for these GApps builds; it is not submitted upstream.
- frameworks/base (20261031): three more patches on top of that one, in [qs-lock-and-tile-gap](https://github.com/Macktherealonereally/galaxy-s21-exynos-lineageos-fixes/tree/main/patches/lineage-frameworks-base/qs-lock-and-tile-gap): the optional "Lock network and security" quick settings lock and a tile icon-gap fix. Apply `privapp-updated-allowlist` first, then these.
- Settings (20261031): [android_packages_apps_Settings](https://github.com/Macktherealonereally/android_packages_apps_Settings), branch `lineage-23.2-20261031`, one commit on exy2100's `lineage-23.2` (the setting for the quick settings lock).
- Aperture (20261031): [android_packages_apps_Aperture](https://github.com/Macktherealonereally/android_packages_apps_Aperture), branch `lineage-23.2-20261031`, one commit on LineageOS `lineage-23.2` (preview matches the video aspect ratio and frame rate).
- [vendor_mack-apps](https://github.com/Macktherealonereally/vendor_mack-apps): Aurora Store as a prebuilt (sha256-pinned, fetched at build time; the APK is not in git). Aurora's GPL source is attached to each release that contains it.
- [vendor_amtg](https://github.com/Macktherealonereally/vendor_amtg): the AMTG layer (makefiles, permission lists, fetch script with pinned hashes). The Google APKs are not in the repo.
- MindTheGapps: [vendor_gapps](https://gitlab.com/MindTheGapps/vendor_gapps), branch `baklava`, commit `f8cdcff`.
- Every fix explained (symptom → log → cause → fix → PR): [galaxy-s21-exynos-lineageos-fixes](https://github.com/Macktherealonereally/galaxy-s21-exynos-lineageos-fixes)

## Credits
@ata-kaner, @mst8981 and @Flopster101 (exy2100 trees and kernel), ExtremeXT and everyone on Exynos AOSP, krazey (open-source IMS stack), PeterCxy and septs (OpenEUICC), the MindTheGapps team.

The fixes were developed with the help of Claude (Anthropic) as a coding assistant; every change was tested on my own S21.

*Your warranty is now void. Knox will trip; Samsung Pay/Wallet and Secure Folder stop working for good. Make a backup first.*
