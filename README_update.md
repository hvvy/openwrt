基于 [OpenWrt](https://openwrt.org) 官方源 https://github.com/openwrt/openwrt
增加Lean插件： https://github.com/coolsnowwolf/lede 及部分第三方插件


### 编译过程

**注意**

* 不要用 root 和 git 用户编译！！！
* 默认登陆IP 192.168.1.1 密码 password

安装编译依赖环境

``` bash
sudo apt-get update
sudo apt-get -y install build-essential asciidoc binutils bzip2 gawk gettext git libncurses5-dev libz-dev patch unzip zlib1g-dev lib32gcc1 libc6-dev-i386 subversion flex uglifyjs git-core gcc-multilib p7zip p7zip-full msmtp libssl-dev texinfo libglib2.0-dev xmlto qemu-utils upx libelf-dev autoconf automake libtool autopoint
```

下载源码 进入openwrt目录

``` bash
git clone -b master https://github.com/hvvy/openwrt.git
cd openwrt
```

更新软件包,测试编译环境
``` bash
./scripts/feeds update -a
./scripts/feeds install -a
```

配置固件菜单,按需自定义设置

``` bash
make menuconfig
```

开始下载编译

``` bash
make download V=s && make -jn V=s
```

---

**更新记录**

2019-10-21 OpenWrt合并编译lean固件

``` bash
git clone https://github.com/openwrt/openwrt
git clone https://github.com/coolsnowwolf/lede
```

1. 复制`~/lede/packgage/lean` 到`~/openwrt/package/lean`
2. 自定义安装包：修改`~/openwrt/include/target.mk`在DEFAULT_PACKAGES:=base-files libc libgcc busybox dropbear mtd uci opkg netifd fstools uclient-fetch logd 后面加上要编译的内容。
3. 应用fullconenat：拷贝lede/package/network/config/firewall/里的makefile文件及patches文件夹到openwrt下面的同目录里，覆盖openwrt官方的
4. 额外增加的插件包AdGuardHome,chinadns,luci-app-filebrowser-mini,luci-app-koolproxyR,luci-app-serverchan,openwrt-frp

更新后的插件包地址：https://github.com/hvvy/openwrt/tree/master/package/lean

