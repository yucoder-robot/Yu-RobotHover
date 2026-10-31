# Yu-RobotHover
小型两轮机器人，可语音对话，运动，识别物体等。<br>
本项目基于LuwuDynamics的[RIG-Omni](https://github.com/LuwuDynamics/rig_omni/tree/main)项目二次开发。<br>
感谢LuwuDynamics对开源的贡献！

# 结构外壳
3D打印件模型下载地址：https://makerworld.com.cn/zh/models/3180489-robothover#profileId-3750085

# 电子硬件
| 组件 | 接口 | 说明 |
| ---- | ---- | ---- |
| GC9A01 圆屏 | SPI | 屏幕显示表情等 |
| IMU（QMI8658C） | I2C | 6 轴姿态 + 平衡控制 |
| 串行舵机 | UART | EM3舵机 |
| KP4012 轮毂电机（Hover: 2 轮） | UART | 平衡、差速驱动和云台控制 |
| I2S 音频（直连） | I2S | 单工/双工 麦克风 + 扬声器（无硬件编解码芯片） |
| 摄像头（GC0308） | DVP | MCP 工具快照 |
| Boot 按键 + 外置触摸模块 | GPIO | 顶部触摸按钮 |

# 快速开始
## 在线开发
访问yucoder.com，无需配置任何环境，即可通过自然语言在线开发代码，编译，打包，下载等。<br>
0基础，新手建议使用此方式开发。

## 本地开发
### 环境要求
对应板型的 ESP32-S3 硬件，配备 16 MB Flash、PSRAM 和匹配的显示屏<br>
ESP-IDF 5.5.x；<br>
工具脚本使用 Python 3.10+；固件构建使用 ESP-IDF 安装的 Python 环境<br>
如需生成或重采样语音资源，安装 FFmpeg<br>

### 安装ESP-IDF
参考官方安装步骤：https://docs.espressif.com/projects/esp-idf/zh_CN/stable/esp32/get-started/index.html#get-started-set-up-tools<br>

Linux快速安装步骤，解决gihub访问过慢问题：
```bash
git clone -b v5.5 https://gitee.com/EspressifSystems/esp-idf.git
cd esp-idf
设置git子模块的仓库为github
./tools/set-submodules-to-github.sh

设置 Git 全局代理替换：
git config --global url."https://git.espressif.com.cn/".insteadOf "https://github.com/"
后续如果还要拉去github的仓库，记得unset这个配置：
git config --global --unset url."https://git.espressif.com.cn/".insteadOf "https://github.com/"

拉取所有子模块
git submodule update --init --recursive

设置国内下载加速环境变量 + 执行安装脚本
export IDF_GITHUB_ASSETS="dl.espressif.cn/github_assets"
export PIP_INDEX_URL="https://pypi.tuna.tsinghua.edu.cn/simple"
./install.sh

**加载环境变量，激活 idf 环境（每次新开终端都需要执行）
./export.sh
```

### 编译
#### 克隆仓库
git clone https://github.com/yucoder-robot/Yu-RobotHover <br>
cd Yu-RobotHover

#### 激活ESP-IDF 环境
Linux环境：
source esp-idf安装目录/export.sh<br>
示例：source ~/esp-idf/export.sh<br>
其他环境参考上面的ESP-IDF官方命令

#### 编译 & 烧录
idf.py build<br>
idf.py -p /dev/ttyUSB0 flash monitor<br>
将 /dev/ttyUSB0 替换为实际串口，macOS 下通常为 /dev/cu.usbmodem…。<br>
