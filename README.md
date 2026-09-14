<div align="center">

# OnePlus 13 ReSukiSU + SUSFS Kernel

**My personal kernel build repository for the OnePlus 13**

[![Build](https://github.com/yyzmiao/OnePlus_ReSukiSU_SUSFS/actions/workflows/build-kernel-release.yml/badge.svg)](https://github.com/yyzmiao/OnePlus_ReSukiSU_SUSFS/actions/workflows/build-kernel-release.yml)
[![ReSukiSU](https://img.shields.io/badge/ReSukiSU-supported-2ea44f)](https://github.com/ReSukiSU/ReSukiSU)
[![SUSFS](https://img.shields.io/badge/SUSFS-integrated-orange)](https://gitlab.com/simonpunk/susfs4ksu)

English · [简体中文](README_CN.md)

</div>

## About this repository

This is my own streamlined build repository for the **OnePlus 13**. It is not a general-purpose multi-device kernel project: the extra device configurations and manifests from upstream have intentionally been removed so that the repository has one clear target and one reproducible build profile.

The build keeps the parts I use—ReSukiSU, SUSFS, networking features, and selected optimizations—while disabling optional components that are unnecessary for my device or usage. The repository remains public for transparency and reproducibility, but every build should be treated as a personal/custom kernel rather than an official OnePlus, ReSukiSU, or WildKernels release.

## Supported target

| Item | Value |
| --- | --- |
| Device | OnePlus 13 |
| SoC | Snapdragon 8 Elite (`sun` / SM8750) |
| Firmware target | OxygenOS 16 |
| Source platform | Android 15 |
| Kernel branch | Linux 6.6 |
| Manifest | `oneplus_13_w.xml` |
| Default root solution | ReSukiSU |
| Filesystem integration | SUSFS |

Only `configs/oos16/OP13.json` is maintained. Other OnePlus, Oppo, Realme, Nord, Ace, Pad, and Open devices are outside the scope of this fork.

## My build profile

Enabled in the current OnePlus 13 configuration:

- ReSukiSU and SUSFS integration
- ThinLTO and the repository's optimization patch set
- BBR v1 and BBR v3 networking support
- TTL target support
- IP set and IPv6 NAT support
- Unicode bypass fix
- A device-specific module blacklist

Intentionally disabled in this profile:

- HMBIRD/SCX
- Baseband Guard (BBG)
- Droidspaces
- NTSync

These choices are deliberate: this fork favors the features I actually use and avoids optional components that add unwanted behavior, overhead, heat, or maintenance for my OnePlus 13 setup.

## Building with GitHub Actions

1. Fork this repository or use it from your own GitHub account.
2. Open **Actions → Build and Release OnePlus 13 Kernel**.
3. Select **Run workflow**.
4. Keep `ReSukiSU` as the KSU type unless you specifically need standard KernelSU.
5. Enable the release option if you want the completed package published under GitHub Releases.
6. Download the generated AnyKernel3 ZIP from the workflow artifacts or release page.

The workflow is intentionally restricted to the OnePlus 13 configuration. A clean build is slower but useful after toolchain, patch, or source changes; normal builds can reuse ccache.

## Installation and safety

Before flashing:

- Confirm that the package was built for **OnePlus 13, OxygenOS 16, Android 15 / kernel 6.6 source**.
- Back up your boot-critical partitions and important data.
- Keep a known-good boot image and a working recovery method available.
- Do not assume compatibility after a major OTA or kernel source change.
- Read the build log and release notes before using the package.

Flashing a custom kernel can cause boot loops, data loss, broken hardware features, or an unbootable device. You are responsible for understanding and accepting those risks.

## Repository layout

```text
configs/oos16/OP13.json                 OnePlus 13 build profile
manifests/oos16/oneplus_13_w.xml        OnePlus 13 source manifest
.github/actions/build-kernel/           Reusable kernel build action
.github/workflows/build-kernel-release.yml
                                        Manual build and release workflow
```

## Credits

This personal fork builds on work from the Android kernel community, especially:

- [huangdihd/OnePlus_ReSukiSU_SUSFS](https://github.com/huangdihd/OnePlus_ReSukiSU_SUSFS)
- [WildKernels/OnePlus_KernelSU_SUSFS](https://github.com/WildKernels/OnePlus_KernelSU_SUSFS)
- [ReSukiSU](https://github.com/ReSukiSU/ReSukiSU)
- [KernelSU](https://github.com/tiann/KernelSU)
- [SUSFS by simonpunk](https://gitlab.com/simonpunk/susfs4ksu)
- [SUSFS userspace module by sidex15](https://github.com/sidex15)
- [AnyKernel3](https://github.com/osm0sis/AnyKernel3)

All credit for upstream projects and patches belongs to their respective maintainers. My changes focus on the OnePlus 13 build profile, repository cleanup, and the fixes needed by this personal build.

## Disclaimer

This project is provided **as is**, without warranty or a guarantee of support. It is not affiliated with or endorsed by OnePlus. If you choose to build or flash it, you accept full responsibility for the result.
