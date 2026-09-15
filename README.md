<h1 align="center">云编译红米AX6000 uboot 110M 大分区</h1>


---

## 项目背景

目前主要使用 ImmortalWrt `24.10` 和 `25.12` 两个版本。

### 背景一：使用 110M 大分区

已经根据[相关讨论帖](https://www.right.com.cn/forum/thread-8265832-1-1.html)刷入 hanwckf 大佬的不死 uboot，希望使用 uboot 的 110M UBI 大分区。


### 背景二：支持较新的系统版本

hanwckf 大佬的仓库目前主要支持 OpenWrt `21.02`：

[hanwckf/immortalwrt-mt798x](https://github.com/hanwckf/immortalwrt-mt798x)

为了使用 OpenWrt `24.10` 及以上版本，本项目基于 ImmortalWrt 官方源码的 `openwrt-24.10` 和 `openwrt-25.12` 分支进行构建：

[immortalwrt/immortalwrt](https://github.com/immortalwrt/immortalwrt)

### 背景三：尽可能保留 overlay 空间

下载的一些 `110m-squashfs-factory.bin` 固件大小约为 45 MB。按照 100 MB 分区计算，刷入后 overlay 大约只剩 55 MB，安装较大的插件时往往不够用。

例如：

- `luci-app-openclash`：约 26–32 MB
- `luci-app-daed`：约 65 MB
- `luci-app-ssr-plus`：约 66 MB

目前已经同时准备了 OpenClash 和 DAE 所需的内核支持，但相关 luci-app 仍需要手动下载。通过压缩固件，固件大小约为 16 MB，overlay 空间最多可保留约 80 MB。


## 固件配置

### ImmortalWrt 24.10

使用脚本 `immortalwrt_110m_compact_24.10.yml`。

编译适用于 OpenWrt 24.10 分支的 ImmortalWrt 110M 大分区 uboot 固件。

### ImmortalWrt 25.12

使用脚本 `immortalwrt_110m_compact_25.12.yml`。

编译适用于 OpenWrt 25.12 分支的 ImmortalWrt 110M 大分区 uboot 固件。



默认配置如下：

| 项目 | 配置 |
| --- | --- |
| 管理地址 | `192.168.16.1` |
| 用户名 | `root` |
| 默认密码 | 无 |
| 2.4G Wi-Fi | `Redmi-2.4G` |
| 5G Wi-Fi | `Redmi-5G` |
| Wi-Fi 密码 | `qwer1234` |

首次登录后请及时修改管理密码和 Wi-Fi 密码。


---

### LEDE 110M 大分区（未充分测试）

使用脚本 `LEDE_110m.yml`。

编译适用于 hanwckf 大佬 uboot / ImmortalWrt 110M 大分区的固件。

### ImmortalWrt 23.07（闭源，未充分测试）

使用脚本 `immortalwrt_237_110m.yml`。

编译适用于 hanwckf 大佬 uboot / ImmortalWrt 110M 大分区的固件。

## 刷机注意事项

1. 刷机前请确认设备已经刷入支持 110M UBI 分区的不死 uboot。
2. 请确认固件型号与设备分区布局匹配，并提前备份重要分区。
3. 刷机存在变砖风险，请准备好 uboot 恢复或串口救砖方案。
