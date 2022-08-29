# LEDE固件Github- Actions在线云编译

### 本云编译基于 Hyy2001X/AutoBuild-Actions && coolsnowwolf/lede 基础上，仅针对新路由2与新路由3进行魔改，更多详情请访问以下链接

Hyy2001X/AutoBuild-Actions仓库地址: [AutoBuild-Actions](https://github.com/Hyy2001X/AutoBuild-Actions)

coolsnowwolf/lede仓库地址: [coolsnowwolf/lede](https://github.com/coolsnowwolf/lede)

支持的 OpenWrt 源码: `coolsnowwolf/lede`、`immortalwrt/immortalwrt`、`openwrt/openwrt`、`lienol/openwrt`

### 使用本AutoBuild-Actions制作的bin文件默认输出至Release,去除一键更新固件脚本，保留tools 固件工具箱，固件默认管理IP 10.10.10.1 ，默认管理员root/password

## 维护设备列表

| 机型 | 配置文件 | 自用 | 是否发布 |
| :----: | :----: | :----: | :----: |
| [x86_64](./.github/workflows/AutoBuild-x86_64.yml) | [x86_64](./Configs/x86_64) | ❎ | ❎ |
| [新路由3](./.github/workflows/AutoBuild-d-team_newifi-d2.yml) | [d-team_newifi-d2](./Configs/d-team_newifi-d2) | ✅ | ✅ |
| [新路由2](./.github/workflows/AutoBuild-lenovo_newifi-d1.yml) | [lenovo_newifi-d1](./Configs/lenovo_newifi-d1) | ✅ | ✅ |
| [zte_e8820s](./.github/workflows/AutoBuild-zte_e8820s.yml) | [zte_e8820s](./Configs/zte_e8820s) | ❎ | ❎ |

## 一、定制固件(可选)

   🎈 **提示**: 文中的 **TARGET_PROFILE** 为要编译的设备名称, 例如: `d-team_newifi-d2`、`lenovo_newifi-d1`

   从本地获取: 在源码目录执行`egrep -o "CONFIG_TARGET.*DEVICE.*=y" .config | sed -r 's/.*DEVICE_(.*)=y/\1/'`
   
   或执行`grep 'TARGET_PROFILE' .config`, 请先执行`make menuconfig`进行配置

1. 进入你的`AutoBuild-Actions`仓库, **下方所有操作都将在你的`AutoBuild-Actions`仓库下进行**

   建议使用`Github Desktop`和`Notepad++`进行操作 [[Github Desktop](https://desktop.github.com/)] [[Notepad++](https://notepad-plus-plus.org/downloads/)]

2. 编辑`/Configs`目录下的配置文件, 若配置文件不存在则需要在本地生成`.config`重命名并上传

   请根据需要自定义`.config`文件对LEDE固件进行个性化修改

3. 编辑`/.github/workflows/某设备.yml`文件, 修改`第 7 行`为随便的名称

4. 编辑`/.github/workflows/某设备.yml`文件, 修改`第 38 行`为上传的`.config`配置文件名称

5. 按照需求且编辑 [/Scripts/AutoBuild_DiyScript.sh](./Scripts/AutoBuild_DiyScript.sh), `/Scripts`下的其他文件无需修改

**/Scripts/AutoBuild_DiyScript.sh: Firmware_Diy_Core() 函数中的变量解释:**
```
   Author 作者名称, AUTO: [自动识别]
   
   Author_URL 自定义作者网站或域名, AUTO: [自动识别]

   Default_Flag 固件标签 (名称后缀), 适用不同配置文件, AUTO: [自动识别]

   Default_Title Shell 终端首页显示的额外信息

   Default_IP 固件 IP 地址 //默认10.10.10.1

   Short_Fw_Date 简短的固件日期, 例如 true: [20210601]; false: [202106012359]

   x86_Full_Images 额外上传已检测到的 x86 虚拟磁盘镜像
   
   Fw_Format 自定义固件格式; false: [自动识别]

   Regex_Skip 输出固件时丢弃包含该内容的文件

   AutoBuild_Features 自动添加 AutoBuild 固件特性, 例如 一键更新固件; 固件工具箱

   注: 禁用某功能请将变量值修改为 false, 开启则为 true

```

## 二、编译固件(必选)

   **手动编译** 点击上方`Actions`, 在左栏选择要编译的设备,点击右方`Run workflow`再点击`绿色按钮`即可开始编译  //默认

   **一键编译** 删除`第 29-30 行`的注释并保存, 以后点击两次右上角的 **Star** 按钮即可一键编译

   **定时编译** 删除`第 26-27 行`的注释, 然后按需修改时间并提交修改 [Corn 使用方法](https://www.runoob.com/w3cnote/linux-crontab-tasks.html)

   **临时修改固件 IP 地址** 该功能仅在**手动编译**生效, 点击`Run workflow`后即可输入 IP 地址
   
   **使用其他 [.config] 配置文件** 点击`Run workflow`后即可输入位于`/Configs`下的配置文件名称

   🔔 **为了你的账号安全, 请不要使用 SSH 连接 Github Action**, `.config`配置以及固件定制等操作请务必在本地完成 🔔


## 使用 tools 固件工具箱

   打开`TTYD 终端`或者使用`SSH`, 执行指令`tools`即可启动固件工具箱

   当前支持以下功能:

   - USB 扩展内部空间
   - Samba 相关设置
   - 打印端口占用详细列表
   - 打印所有硬盘信息
   - 网络检查 (基础网络 | Google 连接检测)
   - AutoBuild 固件环境修复
   - 系统信息监控
   - 打印在线设备列表

## 鸣谢

   - [Hyy2001X/AutoBuild-Actions](https://github.com/Hyy2001X/AutoBuild-Actions)

   - [Lean's Openwrt Source code](https://github.com/coolsnowwolf/lede)

   - [P3TERX's Blog](https://p3terx.com/archives/build-openwrt-with-github-actions.html)

   - [ImmortalWrt's Source code](https://github.com/immortalwrt)

   - [eSir 's workflow template](https://github.com/esirplayground/AutoBuild-OpenWrt/blob/master/.github/workflows/Build_OP_x86_64.yml)
   
   - [[openwrt-autoupdate](https://github.com/mab-wien/openwrt-autoupdate)] [[Actions-OpenWrt](https://github.com/P3TERX/Actions-OpenWrt)]

   - 测试与建议: [CurssedCoffin](https://github.com/CurssedCoffin) [Licsber](https://github.com/Licsber) [sirliu](https://github.com/sirliu) [神雕](https://github.com/teasiu) [yehaku](https://www.right.com.cn/forum/space-uid-28062.html) [缘空空](https://github.com/NaiHeKK) [281677160](https://github.com/281677160)
