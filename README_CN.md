<div align="center">

# 一加 13 ReSukiSU + SUSFS 内核

**我自己使用的一加 13 内核构建仓库**

[![构建状态](https://github.com/yyzmiao/YYZM-OP13-ReSukiSU/actions/workflows/build-kernel-release.yml/badge.svg)](https://github.com/yyzmiao/YYZM-OP13-ReSukiSU/actions/workflows/build-kernel-release.yml)
[![ReSukiSU](https://img.shields.io/badge/ReSukiSU-支持-2ea44f)](https://github.com/ReSukiSU/ReSukiSU)
[![SUSFS](https://img.shields.io/badge/SUSFS-已集成-orange)](https://gitlab.com/simonpunk/susfs4ksu)

[English](README.md) · 简体中文

</div>

## 关于本仓库

这是我为 **一加 13** 精简和维护的个人内核构建仓库，不再定位为通用的多机型构建项目。上游仓库中其他设备的配置与清单已被有意移除，使整个仓库只有一个明确目标和一套可复现的构建配置。

当前构建保留了我需要的 ReSukiSU、SUSFS、网络功能与部分优化，同时关闭了对我的设备或使用方式没有必要的可选组件。仓库公开是为了让构建过程透明、可复现，但这里产生的内核属于个人自定义构建，并非 OnePlus、ReSukiSU 或 WildKernels 的官方版本。

## 支持目标

| 项目 | 内容 |
| --- | --- |
| 设备 | 一加 13 |
| SoC | 骁龙 8 至尊版（`sun` / SM8750） |
| 固件目标 | OxygenOS 16 |
| 源码平台 | Android 15 |
| 内核分支 | Linux 6.6 |
| Manifest | `oneplus_13_w.xml` |
| 默认 Root 方案 | ReSukiSU |
| 文件系统集成 | SUSFS |

本仓库只维护 `configs/oos16/OP13.json`。其他一加、OPPO、Realme、Nord、Ace、Pad 和 Open 设备均不在这个分支的支持范围内。

## 我的构建配置

当前一加 13 配置中启用的功能：

- ReSukiSU 与 SUSFS 集成
- ThinLTO 与仓库中的优化补丁集
- BBR v1 与 BBR v3 网络支持
- TTL Target 支持
- IP Set 与 IPv6 NAT 支持
- Unicode 绕过修复
- 针对本机使用方式设置的模块黑名单

当前配置中有意关闭的功能：

- HMBIRD/SCX
- Baseband Guard（BBG）
- Droidspaces
- NTSync

这些并非遗漏，而是我自己的取舍：只保留实际使用的能力，并避免在一加 13 上引入不需要的行为、额外开销、发热或维护成本。

## 使用 GitHub Actions 构建

1. Fork 本仓库，或直接在你自己的 GitHub 仓库中使用。
2. 打开 **Actions → Build and Release OnePlus 13 Kernel**。
3. 点击 **Run workflow**。
4. 除非明确需要标准 KernelSU，否则保持 KSU 类型为 `ReSukiSU`。
5. 如果希望构建完成后自动发布到 Releases，请打开 release 选项。
6. 构建结束后，从工作流 Artifacts 或 Releases 页面下载 AnyKernel3 ZIP。

工作流已收敛为只构建一加 13。完整清理构建速度较慢，适合工具链、补丁或源码发生变化后使用；日常构建可以继续复用 ccache。

## 刷入前须知

刷入之前请务必：

- 确认压缩包面向 **一加 13、OxygenOS 16、Android 15 / kernel 6.6 源码**。
- 备份启动关键分区和个人数据。
- 准备可用的原厂启动镜像与救砖方式。
- 系统进行大版本 OTA 或内核源码变化后，不要默认旧构建仍然兼容。
- 使用前阅读完整构建日志和 Release Notes。

刷入自定义内核可能导致卡开机、数据丢失、硬件功能异常，甚至设备无法启动。请在理解风险并具备恢复能力的前提下操作，所有后果由使用者自行承担。

## 仓库结构

```text
configs/oos16/OP13.json                 一加 13 构建配置
manifests/oos16/oneplus_13_w.xml        一加 13 源码清单
.github/actions/build-kernel/           内核构建复用 Action
.github/workflows/build-kernel-release.yml
                                        手动构建与发布工作流
```

## 致谢

这个个人分支建立在 Android 内核社区大量工作的基础上，特别感谢：

- [huangdihd/OnePlus_ReSukiSU_SUSFS](https://github.com/huangdihd/OnePlus_ReSukiSU_SUSFS)
- [WildKernels/OnePlus_KernelSU_SUSFS](https://github.com/WildKernels/OnePlus_KernelSU_SUSFS)
- [ReSukiSU](https://github.com/ReSukiSU/ReSukiSU)
- [KernelSU](https://github.com/tiann/KernelSU)
- [simonpunk 开发的 SUSFS](https://gitlab.com/simonpunk/susfs4ksu)
- [sidex15 维护的 SUSFS 用户空间模块](https://github.com/sidex15)
- [AnyKernel3](https://github.com/osm0sis/AnyKernel3)

所有上游项目和补丁的版权与贡献归各自维护者所有。我的改动主要围绕一加 13 的个人构建配置、仓库精简，以及此构建所需的兼容性修复。

## 免责声明

本项目按**现状**提供，不附带任何保证，也不承诺持续支持。本项目与 OnePlus 没有隶属关系，亦未获得其认可。选择构建或刷入，即代表你自行承担全部风险与后果。
