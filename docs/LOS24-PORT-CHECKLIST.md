# LineageOS 24 (Android 17) port checklist: Galaxy S21 Exynos (o1s)

Status: planning. No ETA. Nothing below has been built or tested yet.
Last checked: 2026-10-11.

## 0. What exists today

| Piece | Repo | Branches seen (anonymous read) |
|---|---|---|
| Manifest | `LineageOS/android` | `lineage-24.0` exists |
| Device tree | `exy2100/android_device_samsung_o1s` | `lineage-23.2` only |
| Common tree | `exy2100/android_device_samsung_universal2100-common` | `lineage-23.2`, `lineage-23.2-unofficial`, `drop-ril-audio` |
| Vendor blobs | `exy2100/proprietary_vendor_samsung_universal2100-common` | `lineage-23.2` only |
| Vendor blobs (device) | `exy2100/proprietary_vendor_samsung_o1s` | `lineage-23.2` only |
| Kernel | `exy2100/android_kernel_samsung_universal2100` | `lineage-23.0`, `lineage-23.2`, `android12-5.4-exynos`, ... (no 24.0) |
| My kernel fork | `Macktherealonereally/android_kernel_samsung_universal2100` | `lineage-23.2-20261006` |

Not readable anonymously, so unknown: `android_hardware_samsung_exynos2100`
and any other `exy2100/*` hardware repos. Find the full list in the 23.2
manifest or `lineage.dependencies` once the tree is synced.

Open question: is `lineage-24.0` in `LineageOS/android` stable enough to
build on? Branch existence alone doesn't tell me. Check the LineageOS wiki
and the build status of officially supported devices before starting.

## 1. Build machine (home Linux PC)

- [ ] 300+ GB free disk (SSD), 32 GB RAM or more (plus swap)
- [ ] Packages from the LineageOS build guide (`repo`, `git`, build toolchain)
- [ ] `ccache` enabled and sized (50 GB+)
- [ ] Git identity set; `repo` installed
- [ ] Machine stays on and online during `repo sync` (hundreds of GB)

## 2. Sync the 24.0 tree

- [ ] `repo init -u https://github.com/LineageOS/android.git -b lineage-24.0 --git-lfs`
- [ ] `repo sync` (use `-c --no-tags -j8` to save time and space)
- [ ] Add a local manifest (`.repo/local_manifests/o1s.xml`) pointing at the
      S21 trees, one project per repo in section 0
- [ ] Verify the roomservice / dependency list resolves with no missing repos

## 3. Create 24.0 branches for the S21 trees

For each repo: branch from `lineage-23.2`, name it `lineage-24.0`, push to my
own fork (not the upstream org) until it builds.

- [ ] device/samsung/o1s
- [ ] device/samsung/universal2100-common
- [ ] vendor/samsung/o1s and vendor/samsung/universal2100-common (blobs)
- [ ] kernel/samsung/universal2100
- [ ] any hardware/samsung repos the common tree pulls in
- [ ] Update the manifest entries and README to the new branch names

## 4. Fix what Android 17 breaks (expect iteration)

Order of work, roughly:

1. [ ] `lunch lineage_o1s-<release>-userdebug`: fix product and board
       config errors first (renamed variables, removed flags)
2. [ ] Build system: Soong (`Android.bp`), Kati, deprecated module types
3. [ ] SELinux: new neverallow rules, `*_contexts`, vendor policy
4. [ ] HAL interfaces: AIDL and HIDL versions, `vintf` manifests and
      compatibility matrices (framework matrix level changes)
5. [ ] Vendor / blob compatibility: Samsung vendor blobs are built for an older
      framework; check for missing symbols, linker namespace errors,
      `ro.vndk` and VNDK/vendor API level
6. [ ] Kernel: confirm the 5.4 kernel meets Android 17 requirements; fix
       config fragments and module list (`modules.load*`)
7. [ ] Recovery, AVB and boot image layout
8. [ ] Re-sign with release keys; confirm Odin-flashable recovery

## 5. Re-apply and re-test my 23.2 fixes

Everything here was written against 23.2 and must be re-tested on 24.0.
The fix write-ups live in `galaxy-s21-exynos-lineageos-fixes`.

- [ ] Boots to setup wizard; SELinux enforcing
- [ ] VoLTE and VoWiFi
- [ ] eSIM (OpenEUICC): rebase my fork onto the 24.0 branch
- [ ] NFC
- [ ] WPA3 hotspot, Wi-Fi country code
- [ ] 60 fps video recording (4K60) and video playback in common apps
- [ ] Camera, audio (speaker, USB-C headset), Bluetooth, sensors, fingerprint
- [ ] Root / modules (people on the thread use these)
- [ ] Known 23.2 issue to retest: quick settings reachable on lockscreen

## 6. Release

- [ ] NG and MindTheGapps variants (check MindTheGapps has an Android 17 build)
- [ ] `recovery.tar`, `SHA256SUMS`
- [ ] New release tag, e.g. `lineage-24.0-YYYYMMDD`; update README and XDA post
- [ ] Say clearly in the XDA thread if it is a test build

## Notes

- Test on the one phone first; keep a working 23.2 backup and a way back to
  stock (Odin firmware) before flashing anything.
- A full `repo sync` is far too big for the cloud session I use, which is
  why this runs on the home PC.
