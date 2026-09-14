# store
此项目用于存储 [ImmortalWrt-ImageBuilder](https://github.com/wukongdaily/ImmortalWrt-ImageBuilder) 仓库以外的第三方软件包。
本仓库的 IPK 文件来自多个项目，版权归原作者，见 README 列表。

## 项目定位

本仓库是 OpenWrt 固件流水线**第二层的参考实现**：

- **新项目 [AutoBuildImmortalTWrt](https://github.com/passengerya/AutoBuildImmortalTWrt) 已改为内嵌 store 方案，不再依赖本仓库**——它每天从 [CloudRunFilesBuilder](https://github.com/passengerya/CloudRunFilesBuilder) 的最新 Release 同步 .run，并把 .run 里的 ipk 解压到应用同名子目录，详见其 README 的「第三方软件包机制」章节；
- 本仓库仍然保留两件事：
  1. **.run 自动同步**：`.github/workflows/sync-run-files.yml` 每天 23:00 UTC（北京 7:00）从 CloudRunFilesBuilder 最新 Release 同步 .run 到 `run/x86/`、`run/arm64/` 并自动提交；
  2. **手工 ipk 目录**：`run/<arch>/<应用名>/` 下的 ipk 为人工维护的软件包集合（来源见下方列表）。

### run 目录命名

- `.run` 放架构目录根，与上游 Release 资产同名；24.10 ipk 版无前缀/`24_`，25.12 apk 版 `25_`/`25-`；
- `.ipk` 按应用建同名子目录：`run/<arch>/<应用名>/<ipk原名>.ipk`。


| 软件名称                  | 简介 / 功能描述                        | 来源 / 项目地址                                                                           |
| --------------------- | -------------------------------- | ----------------------------------------------------------------------------------- |
| luci-app-store        | iStore应用商店(0.2.1-r1)             | [linkease/luci-app-store](https://github.com/linkease/istore)                 |
| luci-app-quickstart   | iStore首页和网络向导                  | [linkease/luci-app-quickstart](https://github.com/linkease/nas-packages-luci/tree/main/luci/luci-app-quickstart)
| luci-app-unishare             | 统一文件共享(linkease/nas-packages-luci) | [webdav共享](https://github.com/linkease/nas-packages-luci/tree/main/luci/luci-app-unishare)                      |
| luci-app-amlogic             | 晶晨宝盒(仅限ARM-64平台) | [ophub/luci-app-amlogic](https://github.com/ophub/luci-app-amlogic)                       |
| luci-app-adguardhome  | 本地 DNS 去广告解决方案                   | [AdGuardTeam/AdGuardHome](https://github.com/AdguardTeam/AdGuardHome)               |
| luci-app-advancedplus | 高级设置                   | [sirpdboy/luci-app-advancedplus](https://github.com/sirpdboy/luci-app-advancedplus)                                                                 |
| luci-app-netwizard    | 网络配置向导插件                          | [sirpdboy/luci-app-netwizard](https://github.com/sirpdboy/luci-app-netwizard)                                                                 |
| luci-app-partexp      | 分区扩容插件         | [sirpdboy/luci-app-partexp](https://github.com/sirpdboy/luci-app-partexp)                             |
| luci-theme-kucat      | 酷猫主题                  | [sirpdboy/luci-theme-kucat](https://github.com/sirpdboy/luci-theme-kucat)                 |
| luci-app-taskplan             | 任务计划 |[sirpdboy/luci-app-taskplan](https://github.com/sirpdboy/luci-app-taskplan)|
| luci-app-watchdog      |  openwrt看门狗                 | [sirpdboy/luci-app-watchdog](https://github.com/sirpdboy/luci-app-watchdog)                 |                                                                 |
| luci-app-turboacc     | TurboACC 网络加速器（集成BBR、shortcut）   | [chenmozhijin/turboacc](https://github.com/wukongdaily/store/tree/master/run/x86/luci-app-turboacc) |
| luci-app-mosdns                | 高性能 DNS 分流器，支持 DoH/DoQ 等         | [sbwml/luci-app-mosdns](https://github.com/sbwml/luci-app-mosdns)                     |
| luci-app-nekobox               | 代理工具      | [Thaolga/luci-app-nekobox](https://github.com/Thaolga/openwrt-nekobox)       |
| luci-app-nikki                 | 代理工具               | [nikkinikki-org/nikki](https://github.com/nikkinikki-org/OpenWrt-nikki)                                                                     |
| luci-app-momo                 | 代理工具               | [nikkinikki-org/momo](https://github.com/nikkinikki-org/OpenWrt-momo)                                                                     |
| luci-app-passwall2             | 代理工具           | [Openwrt-Passwall/openwrt-passwall2](https://github.com/Openwrt-Passwall/openwrt-passwall2)       |
| luci-app-ssr-plus              | 代理工具(mihomo 内核)                | [coolsnowwolf/luci-app-ssr-plus](https://github.com/fw876/helloworld) |
| luci-app-passwall               | 代理工具                | [xiaorouji/openwrt-passwall](https://github.com/xiaorouji/openwrt-passwall) |
| homeproxy                | ImmortalWrt 现代代理平台（基于 sing-box）                | [immortalwrt/homeproxy](https://github.com/immortalwrt/homeproxy) |
| OpenClash               | Clash 代理客户端                | [vernesong/OpenClash](https://github.com/vernesong/OpenClash) |
| openlist2              | OpenList（Alist 变体）LuCI 支持                | [sbwml/luci-app-openlist2](https://github.com/sbwml/luci-app-openlist2) |
| openwrt-daede          | 基于 eBPF 的高性能透明代理（dae/daed） | [kenzok8/openwrt-daede](https://github.com/kenzok8/openwrt-daede) |
| sing-box               | 通用代理平台                | [SagerNet/sing-box](https://github.com/SagerNet/sing-box) |
| xray-core              | Xray 代理内核                | [XTLS/Xray-core](https://github.com/XTLS/Xray-core) |
| dufs                   | 轻量文件服务器（静态托管/上传/搜索/WebDAV） | [sigoden/dufs](https://github.com/sigoden/dufs) |
| clashoo              | 代理工具                | [kenzok8/openwrt-clashoo](https://github.com/kenzok8/openwrt-clashoo) |
| tailscale             | ZeroTier 类似的 VPN 工具，基于 WireGuard | [tailscale/tailscale](https://github.com/tailscale/tailscale)                       |
| luci-app-lucky           | Lucky大吉,软硬路由公网神器,ipv6/ipv4 端口转发,反向代理 | [程序 gdy666/lucky](https://github.com/gdy666/lucky) [ipk仓库](https://dl.openwrt.ai/packages-24.10/aarch64_cortex-a53/kiddin9/)                      |
| luci-app-gecoosac           | 集客AC                | [lwb1978/openwrt-gecoosac](https://github.com/lwb1978/openwrt-gecoosac) |
| luci-app-easytier             | 组网 | https://github.com/EasyTier/luci-app-easytier                       |
| luci-app-uninstall             | 高级卸载(v1.2.6) | [用于彻底卸载插件 点这里出处](https://www.bilibili.com/video/BV1dK1xBVEHF)                     |
| luci-theme-aurora      | 极光主题 0.11                 | [eamonxg/luci-theme-aurora](https://github.com/eamonxg/luci-theme-aurora)                 |
| luci-theme-argon      | Argon 简洁主题（支持明暗自动切换）                 | [jerrykuku/luci-theme-argon](https://github.com/jerrykuku/luci-theme-argon)                 |
| luci-app-bandix      | Bandix流量监控 0.11                 | [timsaya/luci-app-bandix](https://github.com/timsaya/luci-app-bandix)                 |
| luci-app-rtp2httpd      |  IPTV 流媒体转发服务器                 | [stackia/rtp2httpd](https://github.com/stackia/rtp2httpd)                 |
| luci-app-tailscale-community      |  Tailscale (Community)                 | [Tokisaki-Galaxy/luci-app-tailscale-community](https://github.com/Tokisaki-Galaxy/luci-app-tailscale-community)                 |
| luci-app-quickfile      |  轻量级 OpenWrt/LuCI 网页文件管理器                 | [sbwml/luci-app-quickfile](https://github.com/sbwml/luci-app-quickfile)                 |

## 如何集成到AutoBuildImmortalWrt
https://github.com/wukongdaily/AutoBuildImmortalWrt/discussions/209
## ❤️其它GitHub Action项目推荐🌟 （建议收藏）⬇️
- ### [一键生成run插件] 🆕
- https://github.com/wukongdaily/RunFilesBuilder<br>
- ### [一键生成docker离线镜像] 🆕
- https://github.com/wukongdaily/DockerTarBuilder<br>
- ### [OpenWrt/Armbian IMG安装器ISO] 🆕
- https://github.com/wukongdaily/img-installer

## 25.12.x 相关仓库
[25.12.x 相关仓库 ](https://github.com/wukongdaily/apk)