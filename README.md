# Comake Pi D3 快速上手指南

## 1. 平台简介

### 1.1 Comake

[Comake](https://www.comake.online) 是一站式端边侧 AI 开发服务平台，提供从选型到量产的全链路支持。"Comake Pi" 是 Comake 自研的物理 AI 开发板系列，覆盖从轻智能 AIoT（1T 算力）到视频边缘计算（8T 算力）的场景需求。

### 1.2 Git Web

[Git Web](https://git.sigmastar.com.cn:9090/user/login) 是 Sigmastar 对外提供的代码托管平台。

**平台定位**：

- **代码分发**：对外发布 SDK、示例代码、工具等，供用户下载使用
- **议题反馈**：用户可通过议题功能提交问题、建议或技术咨询

**账号体系**：

[Git Web](https://git.sigmastar.com.cn:9090/user/login) 平台的账号与 Sigmastar Comake 社区（`https://www.comake.online`）打通，用户需先注册 Comake 社区账号后方可登录 Git Web。

> [!NOTE]
> **注意**：本平台为对外只读平台，**不支持用户创建个人仓库或直接提交代码**。

### 1.3 Comake Pi D3

Comake Pi D3 是一块 **面向端边侧 AI 应用的视频边缘计算开发板**。其核心计算模块搭载 SigmaStar SCM8003G 主控芯片，采用 260-Pin SO-DIMM 金手指标准封装。以下是具体的硬件规格描述。

#### 1.3.1 主板接口模块示意图

![](mymedia/board-main.svg)

#### 1.3.2 底板接口模块示意图

![](mymedia/board-base.svg)

#### 1.3.3 接口概览

| 接口（模块） | 名称 | 规格 | 用途（外设） |
| --- | --- | --- | --- |
| SCM8003G | 主控 SoC | 六核 ARM Cortex-A55，主频最高 1.8GHz | 为设备提供核心计算与控制能力，面向端边侧 AI/NVR 应用 |
| CXDB5CBAM-MA-B | DDR 内存 | LPDDR4X，总容量 4GB | 为 SCM8003G 主控提供高速运行内存 |
| JPO1 DBG | Debug UART 接口 | 4pin 调试排针，TTL 电平，波特率 115200 | 开发板标准调试串口，与计算机串口通信，用于底层固件烧录、调试、日志记录（杜邦线、USB-TTL 串口转换板、USB 延长线、Linux PC） |
| CONV1 12V DC | 电源接口 | DC 12V 直流电源输入 | 为开发板提供直流电源输入（DC 12V 电源适配器） |
| CONU8 USB2.0+USB3.0 | USB 接口 | USB 2.0 接口 + USB 3.0 接口 | 通过 fastboot 协议进行固件烧录与系统升级（双公头 USB 数据线） |
| CON11 USB2.0*2 | USB 接口 | 2 个 USB 2.0 接口 | 操作桌面系统、挂载 U 盘（鼠标、键盘、U 盘） |
| CONH1 HDMI | HDMI 接口 | HDMI Type-A 输出接口 | 高清多媒体输出，连接显示器输出 Ubuntu 桌面，支持可视化操作与界面调试（HDMI 数据线、显示屏） |
| CONG1 RJ45 GE0 | 千兆以太网口 | RJ45 接口，支持 10 / 100 / 1000Mbps | 连接网络，支持网络通信与远程调试，实现高速数据传输（网线） |
| CONG2 RJ45 GE1 | 千兆以太网口 | RJ45 接口，支持 10 / 100 / 1000Mbps | 连接网络，支持网络通信与远程调试，实现高速数据传输（网线） |
| J13 FAN CON | 风扇接口 | PWM 控制风扇，默认 5V，可选 12V | 连接散热风扇，通过 PWM 调节转速进行散热（风扇） |
| SDC2 TF Socket | TF 卡座 | Micro SD 卡槽 | 插入 TF 卡扩展存储与系统启动（TF 卡） |
| CON8 MIPI Panel | MIPI 接口 | MIPI DSI 输出接口 | 连接 MIPI 屏输出 Ubuntu 桌面（FPC 排线、MIPI 屏） |
| CON9 TP CON | 触摸接口 | FPC 触摸接口，默认左侧线序 | 连接触摸屏，实现触摸输入与界面交互（FPC 排线、触摸屏） |
| J7 SATA PWR | SATA 电源接口 | SATA 硬盘电源接口 | 为 SATA 硬盘提供电源（SATA 电源线） |
| CONS4 SATA | SATA 接口 | 支持 SATA gen3 | 连接 SATA 硬盘进行存储扩展（SATA 硬盘） |
| CONP2 PCIE CON | PCIe 连接器 | PCIe gen2×2 | 连接 PCIe 设备，扩展高速外设（PCIe 扩展卡） |
| JPF6 USB BOOT | USB 启动插针 | 2pin USB 启动插针 | 插入跳帽后强制进入 USB 启动模式，用于空片烧录或固件恢复（跳帽） |
| J1 RTC PWR | RTC 电池插针 | 2pin RTC 供电插针 | 连接 RTC 电池，断电后保持系统时钟（RTC 电池） |
| JP2 30P Expansion Header | 30P 扩展排针 | 30pin 扩展插针 | 引出 GPIO 等信号用于扩展外设（杜邦线、扩展模块） |
| JP1 40P Expansion | 40P 扩展排针 | 40pin 扩展插针 | 引出 GPIO 等信号用于扩展外设（杜邦线、扩展模块） |
| JPF9 USB2.0 PWR | USB2.0 供电插针 | CONU8 中 USB2.0 VBUS 供电插针 | 配置为 HOST 给 Device 供电时需插跳帽（跳帽） |
| JPF8 USB3.0 PWR | USB3.0 供电插针 | CONU8 中 USB3.0 VBUS 供电插针 | 配置为 HOST 给 Device 供电时需插跳帽（跳帽） |
| CON10 SPK_R | 扬声器接口（右声道） | 模拟音频输出接口 | 输出右声道音频，驱动扬声器播放（扬声器） |
| CON4 SPK_L | 扬声器接口（左声道） | 模拟音频输出接口 | 输出左声道音频，驱动扬声器播放（扬声器） |
| CON24 MIC1 | 麦克风接口 | 模拟音频输入接口 | 采集音频信号输入系统，用于语音录入与通话（麦克风） |
| CON23 MIC0 | 麦克风接口 | 模拟音频输入接口 | 采集音频信号输入系统，用于语音录入与通话（麦克风） |
| J4 mSATA | mSATA 接口 | mSATA 硬盘接口 | 连接 mSATA 硬盘进行存储扩展（mSATA 硬盘） |
| CN1 M.2 B-KEY 2230 | M.2 B-Key 连接器 | PCIe 2.0×2 + USB 2.0 | 包含 PCIe 2.0×2 可接 NVMe SSD 2230 硬盘，并提供一对 USB 2.0 可接 4G 模块 EM05-CN（NVMe SSD、4G 模块） |
| JZ2 DMIC | DMIC 接口 | 4ch DMIC，最多支持 8 颗 DMIC | 连接数字麦克风采集音频输入（DMIC） |
| JW1 IPEX | IPEX 座子 | Wi-Fi 天线 IPEX 座子 | 连接 Wi-Fi 天线（Wi-Fi 天线） |
| UW2 USB-Wifi | USB Wi-Fi 模组接口 | 预留 USB Wi-Fi 模组，接 SSW105AT，USB P0 默认做 Type-A | 接入 USB Wi-Fi 模组实现无线网络（USB Wi-Fi 模组） |
| CN4 NANO-SIM CON | NANO-SIM 卡座 | NANO-SIM 卡座 | 插入 SIM 卡，配合 M.2 的 4G 模块使用（SIM 卡） |

---

## 2. 准备工作

### 2.1 安装 Docker

**Step 1: 安装依赖**

    sudo apt-get update && sudo apt-get install -y qemu-user-static binfmt-support docker.io

**Step 2: 验证 aarch64 跨架构支持**

    update-binfmts --display | grep "aarch64"

预期输出：

    qemu-aarch64 (enabled):
     interpreter = /usr/libexec/qemu-binfmt/aarch64-binfmt-P

若未启用，执行：

    sudo update-binfmts --enable

**Step 3: 配置 Docker 用户权限（root 用户可跳过）**

将当前用户加入 `docker` 用户组，避免每次执行 `docker` 命令都需要 `sudo`：

    sudo usermod -aG docker $USER

> **注意**：执行上述命令后，需重新登录或执行 `newgrp docker` 使配置生效。

### 2.2 获取 Git 下载凭证

在 [Comake 社区](https://www.comake.online)注册账号后，访问 [Comake 用户中心](https://www.comake.online/account)，记录以下信息以便进行 Git 认证：

- 邮箱：注册 Comake 账号时用到的邮箱

    ![](mymedia/login.png)

- Token：在 “HTTP 凭据” 界面点击 “获取下载凭证” 按钮生成

    ![](mymedia/git-key.png)

### 2.3 配置 Git 环境

1. 将 Git 下载凭证写入本地 `.netrc` 文件（让 Git 自动使用凭据进行认证，无需每次手动输入用户名和密码）：

        echo "machine git.sigmastar.com.cn login <邮箱> password <Token>" >> ~/.netrc
        chmod 600 ~/.netrc

2. 安装 `repo` 多仓库管理工具（下载脚本会通过它拉取 SDK 源码）：

        sudo wget https://mirrors.tuna.tsinghua.edu.cn/git/git-repo -O /usr/bin/repo
        sudo chmod a+x /usr/bin/repo

3. 设置 Git 全局用户名和邮箱：

        git config --global user.name "你的用户名"
        git config --global user.email "你的邮箱"

---

## 3. 下载 SDK

### 3.1 克隆下载脚本

```bash
git clone https://git.sigmastar.com.cn:9090/sigmastar/download_scripts.git
cd download_scripts
```

### 3.2 Debian SDK（推荐新手）

Debian SDK 提供完整的 Ubuntu 桌面体验，适合新手入门、桌面交互和多媒体播放场景。

**快速上手：**

```bash
# 一键下载所有资源（Docker 镜像、工具链、SDK、工具集等）
bash D3_debian_setup.sh all
```

执行 `all` 后的目录结构：

```
.
├── D3_debian_setup.sh
├── docker_versions.yaml
├── docs/                # 文档
├── hw_ref_design/       # 硬件参考设计
├── sgs_model_zoo/       # 算法模型库
├── SourceCode/          # SDK 源码（详见第 4 章）
│   ├── boot/
│   ├── kernel/
│   ├── optee/
│   ├── project/
│   └── sdk/
└── tools/               # SDK 工具集
    ├── BWLATool/
    ├── CalibrationTool/
    ├── FlashTool/
    ├── GenScalerTbl/
    ├── MakeBin/
    ├── PQTool/
    ├── SystemTool/
    ├── ToolChain/        # 交叉编译工具链
    ├── UsbDevelopTool/
    └── ...
```

**命令速查表：**

| 命令 | 说明 |
|------|------|
| `bash D3_debian_setup.sh list_version` | 查看可用版本号 |
| `bash D3_debian_setup.sh all` | 一键下载最新版本全部资源 |
| `bash D3_debian_setup.sh all <version>` | 一键下载指定版本全部资源 |
| `bash D3_debian_setup.sh docker` | 下载最新版本 Docker 镜像 |
| `bash D3_debian_setup.sh docker <version>` | 下载指定版本 Docker 镜像 |
| `bash D3_debian_setup.sh sdk_toolchains` | 下载交叉编译工具链 |
| `bash D3_debian_setup.sh sdk` | 下载最新版本 SDK 源码 |
| `bash D3_debian_setup.sh sdk <version>` | 下载指定版本 SDK 源码 |
| `bash D3_debian_setup.sh list_tools` | 查看可用工具列表 |
| `bash D3_debian_setup.sh tools` | 下载全部工具 |
| `bash D3_debian_setup.sh tools <tool_name>` | 下载单个工具 |
| `bash D3_debian_setup.sh model_zoo` | 下载最新版本算法模型库 |
| `bash D3_debian_setup.sh model_zoo <version>` | 下载指定版本算法模型库 |
| `bash D3_debian_setup.sh docs` | 下载最新版本文档 |
| `bash D3_debian_setup.sh docs <version>` | 下载指定版本文档 |
| `bash D3_debian_setup.sh hw_ref_design` | 下载硬件参考设计资料 |
| `bash D3_debian_setup.sh build_rootfs` | 使用对应 SDK 版本的 Docker 镜像构建 Ubuntu 根文件系统 |
| `bash D3_debian_setup.sh build_rootfs <version>` | 使用指定版本的 Docker 镜像构建 Ubuntu 根文件系统 |
| `bash D3_debian_setup.sh build_image` | 使用对应 SDK 版本的 Docker 镜像编译系统镜像 |
| `bash D3_debian_setup.sh build_image <version>` | 使用指定版本的 Docker 镜像编译系统镜像 |

**使用 `latest` 参数：**

将 `latest` 作为 `<version>` 传入，可获取开发中的最新代码，而非固定的发布版本：

| 命令 | `latest` 行为 |
|------|--------------|
| `bash D3_debian_setup.sh all latest` | 一键下载最新全部资源 |
| `bash D3_debian_setup.sh docker latest` | 下载最新 Docker 镜像 |
| `bash D3_debian_setup.sh sdk latest` | 下载最新 SDK 源码 |
| `bash D3_debian_setup.sh model_zoo latest` | 下载最新算法模型库 |
| `bash D3_debian_setup.sh docs latest` | 下载最新版本文档（与不传 `<version>` 等效） |
| `bash D3_debian_setup.sh build_rootfs latest` | 使用最新 Docker 镜像构建 Ubuntu 根文件系统 |
| `bash D3_debian_setup.sh build_image latest` | 使用最新 Docker 镜像编译系统镜像 |

### 3.3 Linux SDK

Linux SDK 提供精简的 64-bit Linux 系统（无桌面），适合产品化部署、资源受限或不需要图形界面的场景。Linux SDK 还支持直接下载预编译的固件镜像，无需本地编译。

**快速上手：**

```bash
# 一键下载所有资源（Docker 镜像、工具链、SDK、工具集等）
bash D3_linux_setup.sh all
```

执行 `all` 后的目录结构：

```
.
├── D3_linux_setup.sh
├── docker_versions.yaml
├── docs/                # 文档
├── hw_ref_design/       # 硬件参考设计
├── image/               # 预编译固件镜像（images.tar.gz）
├── sgs_model_zoo/       # 算法模型库
├── SourceCode/          # SDK 源码（详见第 4 章）
│   ├── boot/
│   ├── kernel/
│   ├── optee/
│   ├── project/
│   └── sdk/
└── tools/               # SDK 工具集
    ├── BWLATool/
    ├── CalibrationTool/
    ├── FlashTool/
    ├── GenScalerTbl/
    ├── MakeBin/
    ├── PQTool/
    ├── SystemTool/
    ├── ToolChain/        # 交叉编译工具链
    ├── UsbDevelopTool/
    └── ...
```

**命令速查表：**

| 命令 | 说明 |
|------|------|
| `bash D3_linux_setup.sh list_version` | 查看可用版本号 |
| `bash D3_linux_setup.sh all` | 一键下载最新版本全部资源 |
| `bash D3_linux_setup.sh all <version>` | 一键下载指定版本全部资源 |
| `bash D3_linux_setup.sh docker` | 下载最新版本 Docker 镜像 |
| `bash D3_linux_setup.sh docker <version>` | 下载指定版本 Docker 镜像 |
| `bash D3_linux_setup.sh sdk_toolchains` | 下载交叉编译工具链 |
| `bash D3_linux_setup.sh sdk` | 下载最新版本 SDK 源码 |
| `bash D3_linux_setup.sh sdk <version>` | 下载指定版本 SDK 源码 |
| `bash D3_linux_setup.sh image` | 下载最新版本烧录固件 |
| `bash D3_linux_setup.sh image <version>` | 下载指定版本烧录固件 |
| `bash D3_linux_setup.sh list_tools` | 查看可用工具列表 |
| `bash D3_linux_setup.sh tools` | 下载全部工具 |
| `bash D3_linux_setup.sh tools <tool_name>` | 下载单个工具 |
| `bash D3_linux_setup.sh model_zoo` | 下载最新版本算法模型库 |
| `bash D3_linux_setup.sh model_zoo <version>` | 下载指定版本算法模型库 |
| `bash D3_linux_setup.sh docs` | 下载最新版本文档 |
| `bash D3_linux_setup.sh docs <version>` | 下载指定版本文档 |
| `bash D3_linux_setup.sh hw_ref_design` | 下载硬件参考设计资料 |
| `bash D3_linux_setup.sh build_image` | 使用对应 SDK 版本的 Docker 镜像编译系统镜像 |
| `bash D3_linux_setup.sh build_image <version>` | 使用指定版本的 Docker 镜像编译系统镜像 |

> **与 Debian SDK 的主要差异：** Linux SDK 多了 `image` 命令可直接下载预编译固件镜像，无需本地编译。

**使用 `latest` 参数：**

将 `latest` 作为 `<version>` 传入，可获取开发中的最新代码，而非固定的发布版本：

| 命令 | `latest` 行为 |
|------|--------------|
| `bash D3_linux_setup.sh all latest` | 一键下载最新全部资源 |
| `bash D3_linux_setup.sh docker latest` | 下载最新 Docker 镜像 |
| `bash D3_linux_setup.sh sdk latest` | 下载最新 SDK 源码 |
| `bash D3_linux_setup.sh image latest` | 下载最新版本烧录固件（与不传 `<version>` 等效） |
| `bash D3_linux_setup.sh model_zoo latest` | 下载最新算法模型库 |
| `bash D3_linux_setup.sh docs latest` | 下载最新版本文档（与不传 `<version>` 等效） |
| `bash D3_linux_setup.sh build_image latest` | 使用最新 Docker 镜像编译系统镜像 |

---

## 4. SDK 目录结构

下载完成后的 `SourceCode/` 目录结构如下：

```
SourceCode/
├── boot/                # U-Boot 引导程序
│   ├── arch/            #   架构相关代码（ARM）
│   ├── board/           #   板级支持（SigmaStar 平台）
│   ├── cmd/             #   U-Boot 命令实现
│   ├── configs/         #   板级默认配置文件
│   ├── drivers/         #   外设驱动（USB、MMC、NET 等）
│   ├── dts/             #   设备树源文件
│   ├── include/         #   头文件
│   ├── tools/           #   辅助工具
│   └── Makefile         #   U-Boot 编译入口
│
├── kernel/              # Linux 内核
│   ├── arch/arm64/      #   ARM64 架构代码（设备树在此）
│   ├── drivers/         #   内核驱动
│   ├── include/         #   内核头文件
│   ├── net/             #   网络协议栈
│   ├── sound/           #   音频子系统
│   └── Makefile         #   内核编译入口
│
├── project/             # 编译工程入口
│   ├── board/           #   板级配置
│   ├── configs/         #   defconfig 配置文件
│   ├── image/           #   镜像打包脚本与输出
│   ├── kbuild/          #   内核编译集成
│   ├── release/         #   发布输出
│   ├── tools/           #   工程辅助工具
│   └── makefile         #   顶层 Makefile（编译入口）
│
├── sdk/                 # 核心媒体 SDK
│   ├── driver/          #   多媒体驱动
│   ├── linux/           #   用户空间库
│   ├── vendor/          #   第三方组件（ffmpeg、gstreamer 等）
│   └── verify/          #   示例代码与测试程序
│       └── sample_code/ #   demo 代码（LLM/VLM、DLA 等）
│
└── optee/               # OP-TEE 安全执行环境
    ├── optee_os/        #   可信 OS 内核
    ├── optee_client/    #   客户端库
    ├── optee_examples/  #   示例 TA 应用
    └── optee_test/      #   测试套件
```

---

## 5. 编译固件

下载完成后，使用脚本一键编译：

### 5.1 Debian SDK

```bash
# 构建 Ubuntu 根文件系统
bash D3_debian_setup.sh build_rootfs

# 编译 64-bit Ubuntu 系统镜像
bash D3_debian_setup.sh build_image
```

其中 `SourceCode/project/image/output/images/UsbUpgradePackage` 目录生成的 `SgsUsbUpgrade.bin` 为 USB 升级固件，升级方法详见[固件升级](#6-固件升级)。

### 5.2 Linux SDK

```bash
# 编译 64-bit Linux 系统镜像
bash D3_linux_setup.sh build_image
```

其中 `SourceCode/project/image/output/images/UsbUpgradePackage` 目录生成的 `SgsUsbUpgrade.bin` 为 USB 升级固件，升级方法详见[固件升级](#6-固件升级)。

---

## 6. 固件升级

### 6.1 硬件接线

<img src="mymedia/board-connect.png" style="zoom: 35%">

1. 开发板 CONV1 12V DC 电源接口接入 DC 12V 电源适配器。
2. 将双公头 USB 数据线一端接入开发板 CONU8 USB2.0 接口（黑色），另一端接入 PC。
3. 开发板任意 CON11 USB2.0 接口接入鼠标。
4. 将 HDMI 数据线一端接入开发板 CONH1 HDMI 接口，另一端接入显示屏。
5. 开发板 CONG1 RJ45 GE0 网口接入网线，确保开发板与 PC 连接至同一网段。

### 6.2 串口接线

串口是嵌入式开发的基础调试手段，可在无网络或系统未启动时使用。以 MobaXterm 为例：

1. 开发板 JPO1 DBG 接口依次连接杜邦线、USB-TTL 串口转换板、USB 延长线、Linux PC。

    ![](mymedia/board-serial-uart.png)

2. 打开 MobaXterm 工具，依次点击 Session、Serial，Serial Port 根据设备管理器选择（如 COM4），Speed (bps) 选择 115200，最后点击 OK 连接串口。

    ![](mymedia/mobaxterm.png)

### 6.3 进入 USB 升级模式

根据 eMMC 当前状态，选择对应方式让开发板进入 USB 升级模式：

- **空片升级**：eMMC 处于出厂空白状态，或 U-Boot 等固件已被完全擦除。默认处于USB升级模式，直接插入USB线至CONU8 USB3.0即可识别升级。

- **非空片升级**：eMMC 上已有可运行的 U-Boot。

    1. 打开串口调试，使用 USB-TTL 串口转换板连接开发板 JPO1 DBG 接口（波特率 115200）。
    2. 开发板上电，进入 U-Boot，输入 `sgsusb` 进入 USB 升级模式。

            Sgs # sgsusb
            <USB>[UDC] PULL UP D+.
            <USB>[GADGET] UDC start
            SGS USB upgrade: no default storage (ctrl 0)
            Waiting for USB connection...
            <USB>[LINK] Suspend.
            <USB>[LINK] High speed device.
            <USB>[2][Enable] bulk out with maxpacket/fifo(512/1024)
            <USB>[1][Enable] bulk in with maxpacket/fifo(512/8192)

- **强制升级**：在JPF6 USB BOOT 插上跳帽（硬件连接图标记⑥），开发板即强制进入 USB 启动模式。可用于异常状态下的强制升级恢复。升级完成后需要拔掉跳帽才可正常使用。

### 6.4 整包固件升级

打开 "UsbDevelopToolUI.exe" --> "固件升级"，选中 `SourceCode/project/image/output/images/UsbUpgradePackage` 下生成的 `SgsUsbUpgrade.bin`，点击 "开始升级"。

![固件升级](mymedia/full.png)

### 6.5 单分区升级

1. 打开 “UsbDevelopToolUI.exe” --> “高级”，解包原固件。

    ![](mymedia/advanced.png)

2. 替换 UsbDevToolImage 目录中的分区文件。
3. 切换到工具的 “单分区” 界面，选择设备，浏览解包目录下的 package.ini，勾选要升级的分区，再点击 “开始升级”。

    ![](mymedia/single.png)

### 6.6 验证

**Debian SDK：** 升级完成后，显示器将显示 Ubuntu 桌面登录界面。

| 用户名 | 密码 |
|--------|------|
| ubuntu | ubuntu |
| root   | 123456 |

**Linux SDK：** 升级完成后，通过串口终端（波特率 115200）连接开发板，能正常进入终端即可。

> 至此，你已经成功跑通了 Comake Pi D3 的完整开发流程。

---

## 7. Git Web 平台使用指南

### 7.1 登录 Git Web

1. 打开浏览器，访问 [Git Web](https://git.sigmastar.com.cn:9090/user/login)

2. 输入登录凭据

	![输入登录凭据](mymedia/gitweb-login.png)

    - **用户名**：Comake 社区注册邮箱
    - **密码**：Comake 社区账户密码

3. 点击「登录」按钮

> 如登录失败，请确认 Comake 社区账号已激活，且用户名和密码输入正确。

### 7.2 浏览仓库

登录后，点击顶部导航栏「探索」即可查看所有对外公开的代码仓库。你也可以通过搜索栏直接搜索仓库名称。

在仓库页面可以查看：

- 文件目录与内容
- 提交历史
- 版本标签（Tags）与发布（Releases）
- 分支列表

### 7.3 克隆仓库

在仓库页面，点击「复制网址」按钮，复制 HTTPS 地址：

```bash
git clone https://git.sigmastar.com.cn:9090/<namespace>/<repo-name>.git
```

执行后输入登录凭据：

- **用户名**：Comake 社区注册邮箱
- **密码**：Comake 社区账户密码

### 7.4 下载压缩包

如果不想使用 Git 命令行，可直接下载代码压缩包：进入仓库页面，点击「...」→ 选择 下载ZIP 或 下载TAR.GZ。

![下载压缩包](mymedia/gitweb-download.png)

### 7.5 更新本地代码

当平台上的仓库有更新时，在本地仓库目录执行：

```bash
git pull
```

### 7.6 提交反馈（议题）

议题是你向 Sigmastar 技术团队反馈问题的渠道。你可以通过议题提交：

- **Bug 报告**：代码或文档中的错误
- **功能建议**：希望新增或改进的功能
- **技术咨询**：使用过程中遇到的技术问题

#### 7.6.1 创建议题

1. 登录后进入目标仓库
2. 点击顶部「议题」选项卡
3. 点击「创建议题」

    ![创建议题](mymedia/gitweb-issue-1.png)

4. 填写议题

    - **标题**：简要概述问题（如 "XXX 示例在 Linux 环境编译失败"）
    - **描述**：详细说明问题（参考下方模板）

5. 点击「创建议题」确认按钮

    ![创建议题](mymedia/gitweb-issue-2.png)

#### 7.6.2 议题描述模板

建议按照以下模板填写，以便技术团队快速定位和处理：

```markdown
### 问题类型
<!-- 请选择：Bug 报告 / 功能建议 / 技术咨询 -->

### 环境信息
- 操作系统：
- 代码版本 / Tag：
- 工具链版本（如适用）：

### 问题描述
<!-- 请详细描述遇到的问题 -->

### 复现步骤（Bug 类必填）
1.
2.
3.

### 期望行为
<!-- 描述你期望的正确行为 -->

### 实际行为
<!-- 描述实际观察到的行为 -->

### 附加信息
<!-- 可附上日志、截图、命令行输出等 -->
```

#### 7.6.3 关注议题进度

提交议题后，你可以：

- 在议题页面与 Sigmastar 技术人员留言沟通
- 当议题被标记为「已关闭」时，表示问题已处理完成