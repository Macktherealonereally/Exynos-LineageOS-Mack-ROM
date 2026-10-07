# LineageOS 23.2 for the Galaxy S21 Exynos (SM-G991B)

Unofficial LineageOS 23.2 (Android 16) builds for the Galaxy S21 Exynos (`o1s`), with VoLTE, eSIM (OpenEUICC), 60 fps video, a WPA3 hotspot and more. SELinux enforcing, signed with my own release keys.

Downloads are on the [Releases](../../releases) page. Each release has two variants; pick one (switching between them needs a clean install):

| File | What it is |
|---|---|
| `…-o1s-NG.zip` | No Google apps |
| `…-o1s-MTG.zip` | With the minimal MindTheGapps set (Play Store, Play Services) |
| `recovery.tar` | LineageOS recovery for Odin (works for both variants) |
| `SHA256SUMS` | Checksums |

Installation, known issues and support: see the XDA thread.

## Source code
- Kernel: [android_kernel_samsung_universal2100, branch `lineage-23.2-20261006`](https://github.com/Macktherealonereally/android_kernel_samsung_universal2100/tree/lineage-23.2-20261006)
- OpenEUICC (GPLv3): [OpenEUICC fork, branch `lineage-23.2-20261006`](https://gitea.angry.im/Macktherealonereally/OpenEUICC/src/branch/lineage-23.2-20261006)
- Device trees: [exy2100](https://github.com/exy2100) plus my changes as PRs there
- Every fix explained (symptom → log → cause → fix → PR): [galaxy-s21-exynos-lineageos-fixes](https://github.com/Macktherealonereally/galaxy-s21-exynos-lineageos-fixes)

## Credits
@ata-kaner, @mst8981 and @Flopster101 (exy2100 trees and kernel), ExtremeXT and everyone on Exynos AOSP, krazey (open-source IMS stack), PeterCxy and septs (OpenEUICC), the MindTheGapps team.

The fixes were developed with the help of Claude (Anthropic) as a coding assistant; every change was tested on my own S21.

*Your warranty is now void. Knox will trip; Samsung Pay/Wallet and Secure Folder stop working for good. Make a backup first.*
