# G614JVR_G614JVR--Hackintosh
ROG Strix G16 G614JVR_G614JVR--Raptor Lake-HX-- i9-14900HX--Hackintosh
# ROG Strix G16 G614JVR（枪神8）黑苹果 EFI

> 适用机型：ASUS ROG STRIX G16 G614JVR_G614JVR（枪神8） 平台：Raptor Lake-HX（13/14 代酷睿 HX） CPU：英特尔 Core i9-14900HX
>
>  <span style="color:#3b82f6">💡 替代方案建议：可尝试使用雷电4接口外接AMD免驱独立显卡运行黑苹果。雷电4协议本身兼容性较好，理论上可行性较高；本人暂无雷电相关外设，因此该方案未经过实际测试，仅供参考。</span>
> 
> GPU：NVIDIA GeForce RTX 4060笔记本 + Intel UHD 显卡（核显）  
> 
> 系统：macOS Sequoia 15.8  
> 
> 安装文件为：[HeiPG.cn]Install_macOS_Sequoia_15.8（24H23）_with_OpenCore_1.0.8_Dev_and_FirPE.dmg 可前往 heipg.cn 网站下载（感谢 heipg.cn 提供此镜像）
> 
> 引导：OpenCore
> 
> <span style="color:red">⚠️ 对于实验性 NVIDIA Metal 驱动方案，截至2026.10.13为止，暂时不建议使用，有损坏财产风险。因此谨慎使用此驱动。</span>
>
> <span style="color:red">⚠️ 对于实验性 NVIDIA Metal 驱动方案，截至2026.10.13为止，暂时不建议使用，有损坏财产风险。因此谨慎使用此驱动。</span>
>
> <span style="color:red">⚠️ 对于实验性 NVIDIA Metal 驱动方案，截至2026.10.13为止，暂时不建议使用，有损坏财产风险。因此谨慎使用此驱动。</span>
>
> <span style="color:red">**重要事情说三遍！！！重要事情说三遍！！！重要事情说三遍！！！**</span>






⚠️ **重要声明**
- 本 EFI 为**笔记本**专用，并非台式机配置。
- 本 EFI 使用 nullmoth 发布的 链接：https://github.com/nullmoth/1401 的windows工具生成。
- 后续经过个人的不断测试以及经过[极光呆呆脑](https://github.com/bilijp153)完善。
- macOS 安装会**清空目标整块硬盘或某分区**，操作前务必备份重要数据。
- NVIDIA 独立显卡（RTX4060）使用 NullMoth **实验性驱动**，非苹果官方支持，存在稳定性风险，仅供测试与学习使用。
- 11 代及以上 Intel ROG 笔记本，**Resizable BAR / CSM 在 BIOS 中无手动开关**（固件内置/隐藏），无需也无法手动设置。

---

## 目录

- [硬件配置表](#硬件配置表)
- [系统与引导版本](#系统与引导版本)
- [BIOS 设置（安装前必做）](#bios-设置安装前必做)
- [鸣谢](#鸣谢)

---

## 硬件配置表

| 项目 | 型号 / 规格 | 黑苹果状态 | 说明 |
| ---- | ---- | ---- | ---- |
| 主板 | ASUS ROG STRIX G16 G614JVR（HM770 芯片组） | ✅ | Raptor Lake-HX 平台 |
| CPU | Intel Core i9-14900HX（8P+16E，24核32线程） | ✅ | 需大小核补丁 |
| 内存 | 板载 + 扩展 DDR5 | ✅ | 视具体配置 |
| 核显 | Intel UHD Graphics（Raptor Lake） | ⚠️ | 
| 独显 | NVIDIA GeForce RTX 4060 Laptop | ⚠️ | NullMoth 实验性 Metal 驱动（暂时不建议使用，谨慎使用） |
| 声卡 | 板载 Realtek（需查具体型号） | ⚠️ | 尚未完善 |
| 有线网卡 | 板载（视型号） | ✅ | RealtekRTL8111  |
| 无线网卡 | Intel 6E AX211 | ✅ | AirportItlwm / itlwm（二选一）+ 蓝牙三件套 （型号为6E的网卡，可以使用itlwm+HeliPort来驱动，若想原生驱动，请更换 intel wifi 6 AX211 或 其他的支持网卡，详见此链接：https://openintelwireless.github.io/itlwm/Compat.html|
| 蓝牙 | Intel（AX211 自带） | ✅  |
| 硬盘 | NVMe SSD（Windows + macOS 分盘） | ✅  |
| 触摸板 / 键盘 | ⚠️ | 建议禁用内置键盘，使用外接键盘，内置键盘对于黑苹果有冲突，容易重置或刷新屏幕，触摸板暂时无法驱动 |
| 电池 | 板载 | ✅ |  |

---

## 系统与引导版本

| 组件 | 版本 / 说明 |
| ---- | ---- |
| macOS | Sequoia 15.8 |
| OpenCore | 0.9.x / 1.0.x（以仓库内 EFI 为准） |
| 模拟机型（SMBIOS） | MacBookPro16,2（仅供参考，以实际为准。可能使用16.2或16.4，本人建议使用16.2） |
| 引导模式 | 纯 UEFI

> SMBIOS 中的 Serial / MLB / ROM 请自行生成自己的值，**不要直接使用他人序列号**，否则 iMessage / FaceTime 可能无法使用。

---

## BIOS 设置（安装前必做）

> 进 BIOS：开机连续按 `F2`；启动菜单：开机连续按 `Esc`。
> 改完 BIOS 后 **先让 Windows 正常启动一次**，确认系统仍能引导，再进行 macOS 安装。

### 必须设置（红色优先级最高）

| 设置项 | 目标值 | 说明 |
| ---- | ---- | ---- |
| **VMD（Volume Management Device）** | **关闭 / Disabled** | ⚠️ **最重要**。HM770 芯片组默认开 VMD，macOS 无法直接识别 VMD 下的 NVMe 硬盘，关闭后 AHCI 模式才能识别 SSD |
| **Secure Boot（安全启动）** | **关闭 / Disabled** | macOS 安装盘未经微软签名，开启会被拒绝启动。华硕：Boot → Secure Boot → OS Type 选 `Other OS` |
| **Above 4G Decoding** | **开启 / Enabled** | NullMoth NVIDIA 驱动硬性要求，将显卡完整内存映射到 4GB 以上地址空间 |



### 其他提示
- **BitLocker（Windows 磁盘加密）**：如果 Windows 开启了 BitLocker，进 BIOS 修改安全启动**之前**，先暂停 BitLocker 或保存恢复密钥（`设置 → 隐私和安全 → 设备加密`，或 `aka.ms/myrecoverykey`），否则改完安全启动后 Windows 会强制要求输入恢复密钥。


- 结构参考：

```
├── EFI/
│   └── OC/
└── com.apple.recovery.boot/
    ├── BaseSystem.dmg
    └── BaseSystem.chunklist
```


---

## 鸣谢
- [OpenCore](https://github.com/acidanthera/OpenCorePkg)
- [OpenIntelWireless](https://github.com/OpenIntelWireless)
- NullMoth 社区（NVIDIA Metal 实验驱动）：<https://github.com/nullmoth/nvidia-macos-driver>
- 生成EFI的工具来自 NullMoth 1401 Windows工具：<https://github.com/nullmoth/1401>
- itlwm 无线网卡驱动：<https://github.com/laobamac/itlwm/releases>
- [极光呆呆脑](https://github.com/bilijp153)
- https://dortania.github.io/- 技术支持与知识库
- https://github.com/acidanthera- 提供核心驱动开发
- 本文章大致结构由**豆包姐姐Ai工具**生成

---

*本仓库仅供学习与测试，请在符合当地法律法规的范围内使用。*
