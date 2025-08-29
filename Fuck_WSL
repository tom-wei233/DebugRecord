# WSL2 USB/IP 直通限制与经验总结

## 问题描述

在 WSL2 环境下，使用通用版 usbip 工具（`linux-tools-generic`）时，attach USB 设备（如 ST-Link）会出现如下警告：

```
WARNING: usbip not found for kernel 6.6.87.2-microsoft
You may need to install the following packages for this specific kernel:
  linux-tools-6.6.87.2-microsoft-standard-WSL2
  linux-cloud-tools-6.6.87.2-microsoft-standard-WSL2
```

## 原因分析

- WSL2 使用的是微软定制内核，APT 源没有配套的 kernel module/tools 包。
- 通用 usbip 工具只能提供命令行，无法驱动内核 module，导致设备 attach 失败。

## 现有解决方案

1. **Windows 侧操作为主**  
   - WSL2 仅做代码开发、编译
   - 烧录、串口等直接用 Windows 工具

2. **持续关注 WSL2 官方/社区动态**  
   - 未来可能会支持 apt 一键安装或预装 usbip 工具

## 实践建议

- 遇到该警告/问题，无需反复尝试，当前无解。
- 开发流程建议在 Windows 与 WSL2 间切换使用。

## 参考链接

- [WSL Issues - GitHub](https://github.com/microsoft/WSL/issues)
################################################################
    豆包发现了端倪！！！copilot败下阵来，争辩休如息
################################################################
# WSL2 USB/IP 直通新方案经验总结

## 新流程（usbipd-win 3.0+，WSL2最新版）

1. **在 Windows PowerShell（管理员）执行：**
   ```powershell
   usbipd list
   usbipd attach --wsl --busid <busid>
   ```
   - 设备会自动映射到所有WSL2发行版，无需在 WSL2 Ubuntu 内部手动attach。

2. **在 WSL2 Ubuntu 内部：**
   - 直接运行 `lsusb`、`ls /dev/ttyUSB*` 等命令查看设备节点。
   - 设备已可被 Linux 工具访问（如 st-link、minicom、JLink）。

## 说明

- 该方案无需在 WSL2 内部安装 usbip 工具，省去旧版 attach 步骤。
- 适用新版 WSL2 和 usbipd-win，推荐升级环境后使用。

## 参考

- [usbipd-win GitHub](https://github.com/dorssel/usbipd-win)
- [微软 WSL2 官方文档](https://learn.microsoft.com/en-us/windows/wsl/connect-usb)
