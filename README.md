**基于P3TERX创建** [教程链接](https://p3terx.com/archives/build-openwrt-with-github-actions.html)

# Actions-OpenWrt

[![LICENSE](https://img.shields.io/github/license/mashape/apistatus.svg?style=flat-square&label=LICENSE)](https://github.com/P3TERX/Actions-OpenWrt/blob/master/LICENSE)
![GitHub Stars](https://img.shields.io/github/stars/P3TERX/Actions-OpenWrt.svg?style=flat-square&label=Stars&logo=github)
![GitHub Forks](https://img.shields.io/github/forks/P3TERX/Actions-OpenWrt.svg?style=flat-square&label=Forks&logo=github)

## 使用教程

- 点击 [Use this template](https://github.com/P3TERX/Actions-OpenWrt/generate) 按钮创建这个项目仓库。
- 产生 `.config` 文件使用 [Lean's OpenWrt](https://github.com/coolsnowwolf/lede) 源代码 ( 后面有介绍如何定制 )
- 把 `.config` 文件复制到你的仓库里面。
- 选择 `Build OpenWrt` 在 Actions 页面中.
- 点击 `Run workflow` 按钮.
- 构建完成后，单击 Actions 页面右上角的“Artifacts”按钮下载二进制文件。

## 创建`.config`教程

- 找一个ubuntu 20.04环境
- 克隆 [Lean's OpenWrt](https://github.com/coolsnowwolf/lede) 仓库
- 进入lede仓库目录, 编辑feeds.conf.default文件，添加`src-git kenzo https://github.com/kenzok8/openwrt-packages`，`src-git small https://github.com/kenzok8/small`两行
- 更新下载包 `./scripts/feeds update -a && ./scripts/feeds install -a`
- 执行命令 `make menuconfig`，选择你需要的软件包。

## 替换默认主题

```
# 替换默认主题为 luci-theme-argon
sed -i 's/luci-theme-bootstrap/luci-theme-argon/' feeds/luci/collections/luci/Makefile
```

## 替换默认地址

```
# 设置默认IP为 192.168.99.1
sed -i 's/192.168.1.1/192.168.99.1/g' package/base-files/files/bin/config_generate
```

## x86_64组件列表

```
Target Images ---> BuildVMwareimage files (VMDK) 取消
Target Images ---> Kernel partition size（in MB）配置 256
Target Images ---> Root filesystem partition size（in MB）配置 1024
Base system ---> Build with DHCPv6 support. 勾选
Extra packages ---> autosmaba 取消
Extra packages ---> ipv6help 勾选
Utilities --> Editors --> vim #vi 编辑器
Utilities --> Shells --> bash #命令解释程序
Utilities --> Compression --> bzip2 #bzip2压缩
Utilities --> Compression --> gzip #gzip压缩
Utilities --> Compression --> unzip #unzip压缩
Utilities --> disc --> eject #U盘卸载
Utilities --> disc --> fdisk #MBR分区工具
Utilities --> disc --> parted #分区工具
Utilities --> disc --> lsblk #列出磁盘设备及分区查看工具
Utilities --> Filesystem --> resize2fs #调整文件系统大小
Network ---> socat #多功能的网络工具
LuCI ---> Applications ---> luci-app-accesscontrol #访问时间控制
LuCI ---> Applications ---> luci-app-adbyby-plus   #去广告
LuCI ---> Applications ---> luci-app-adgurardhome  #AdGuard home广告过滤（Le库以外的插件）
LuCI ---> Applications ---> luci-app-argon-config  #Argon主题配置插件（Le库以外的插件）
LuCI ---> Applications ---> luci-app-arpbind  #IP/MAC绑定
LuCI ---> Applications ---> luci-app-autoreboot  #计划重启
LuCI ---> Applications ---> luci-app-commands  #command
LuCI ---> Applications ---> luci-app-ddns   #动态域名 DNS
LuCI ---> Applications ---> luci-app-diskman   #磁盘管理
LuCI ---> Applications ---> luci-app-dnscrypt-proxy  #DNSCrypt解决DNS污染
LuCI ---> Applications ---> luci-app-dnsfilter  #DNSFilter基于DNS的广告过滤
LuCI ---> Applications ---> luci-app-dnsforwarder  #DNSForwarder防DNS污染
LuCI ---> Applications ---> luci-app-e2guardian   #Web内容过滤器
LuCI ---> Applications ---> luci-app-eqos  #基于IP地址限速（Le库以外的插件）
LuCI ---> Applications ---> luci-app-filetransfer  #文件传输
LuCI ---> Applications ---> luci-app-firewall   #添加防火墙
LuCI ---> Applications ---> luci-app-frpc   #内网穿透Frp客户端
LuCI ---> Applications ---> luci-app-ipsec-vpnd   #VPN服务器 IPSec
LuCI ---> Applications ---> luci-app-jd-dailybonus  #京东签到服务
LuCI ---> Applications ---> luci-app-nlbwmon   #网络带宽监视器
LuCI ---> Applications ---> luci-app-ntpc   #ntp time config
LuCI ---> Applications ---> luci-app-ramfree  #释放内存
LuCI ---> Applications ---> luci-app-smartdns  #smartdns
LuCI ---> Applications ---> luci-app-ssr-plus   #SSR科学上网Plus+（Le大佬插件，trojan,v2ray,xray）
LuCI ---> Applications ---> luci-app-ttyd   #网页终端命令行
LuCI ---> Applications ---> luci-app-turboacc   #Turbo ACC 网络加速(支持 Fast Path 或者 硬件 NAT)
LuCI ---> Applications ---> luci-app-unblockmusic  #网易云音乐解锁
LuCI ---> Applications ---> luci-app-upnp  #upnp
LuCI ---> Applications ---> luci-app-vlmcsd  #kms server
LuCI ---> Applications ---> luci-app-wireguard #wireguard vpn
LuCI ---> Applications ---> luci-app-wol   #WOL网络唤醒
LuCI ---> Applications ---> luci-app-wrtbwmon  #实时流量监测
LuCI ---> Applications ---> luci-app-zerotier  #ZeroTier内网穿透
```

## xiaoyu_c5组件列表

```
Target System ---> MediaTek Ralink MIPS #勾选
Subtarget ---> MT7621 base boards #勾选
Target Profile ---> XiaoYu XY-C5
Target Images ---> squashfs #勾选
Global build settings ---> Enalbe IPv6 support in packages #勾选，其它默认
Base system ---> dnsmqsq-full --> Build with DHCPv6 support. #勾选
Base system ---> dnsmqsq-full --> Build with DNSSEC support. #勾选
Extra packages ---> ipv6help #勾选
Utilities --> Editors --> vim #vi 编辑器
Utilities --> disc --> cfdisk #分区工具
Utilities --> disc --> fdisk #分区工具
Utilities --> disc --> lsblk #磁盘列举工具
Utilities --> Filesystem --> resize2fs #调整文件系统大小
LuCI ---> Applications ---> luci-app-argon-config  #Argon主题配置插件（Le库以外的插件）
LuCI ---> Applications ---> luci-app-arpbind  #IP/MAC绑定
LuCI ---> Applications ---> luci-app-autoreboot  #计划重启
LuCI ---> Applications ---> luci-app-commands  #command
LuCI ---> Applications ---> luci-app-ddns   #动态域名 DNS
LuCI ---> Applications ---> luci-app-eqos  #基于IP地址限速（Le库以外的插件）
LuCI ---> Applications ---> luci-app-filetransfer  #文件传输
LuCI ---> Applications ---> luci-app-firewall   #添加防火墙
LuCI ---> Applications ---> luci-app-frpc   #内网穿透Frp客户端
LuCI ---> Applications ---> luci-app-nlbwmon   #网络带宽监视器
LuCI ---> Applications ---> luci-app-ntpc   #ntp time config
LuCI ---> Applications ---> luci-app-passwall   #passwall科学上网（ChinaDNS-NG,Haproxy,PDNSD,SS-client,SSR-client,Simple-Obfs,Trojan-Plus,V2ray-Plugin,Xray-Plugin）
LuCI ---> Applications ---> luci-app-ramfree  #释放内存
LuCI ---> Applications ---> luci-app-ttyd   #网页终端命令行
LuCI ---> Applications ---> luci-app-turboacc   #Turbo ACC 网络加速(Flow,BBR)
LuCI ---> Applications ---> luci-app-unblockmusic  #网易云音乐解锁
LuCI ---> Applications ---> luci-app-upnp  #upnp
LuCI ---> Applications ---> luci-app-vlmcsd  #kms server
LuCI ---> Applications ---> luci-app-watchcat # 断网检测功能与定时重启
LuCI ---> Applications ---> luci-app-wireguard #wireguard vpn
LuCI ---> Applications ---> luci-app-wol   #WOL网络唤醒
LuCI ---> Applications ---> luci-app-wrtbwmon  #实时流量监测
```

## Credits

- [Microsoft Azure](https://azure.microsoft.com)
- [GitHub Actions](https://github.com/features/actions)
- [OpenWrt](https://github.com/openwrt/openwrt)
- [Lean's OpenWrt](https://github.com/coolsnowwolf/lede)
- [tmate](https://github.com/tmate-io/tmate)
- [mxschmitt/action-tmate](https://github.com/mxschmitt/action-tmate)
- [csexton/debugger-action](https://github.com/csexton/debugger-action)
- [Cowtransfer](https://cowtransfer.com)
- [WeTransfer](https://wetransfer.com/)
- [Mikubill/transfer](https://github.com/Mikubill/transfer)
- [softprops/action-gh-release](https://github.com/softprops/action-gh-release)
- [ActionsRML/delete-workflow-runs](https://github.com/ActionsRML/delete-workflow-runs)
- [dev-drprasad/delete-older-releases](https://github.com/dev-drprasad/delete-older-releases)
- [peter-evans/repository-dispatch](https://github.com/peter-evans/repository-dispatch)

## License

[MIT](https://github.com/P3TERX/Actions-OpenWrt/blob/main/LICENSE) © [**P3TERX**](https://p3terx.com)
