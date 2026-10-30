# Yu-RobotHover
小型两轮机器人，可语音对话，运动，识别物体等。<br>
本项目基于LuwuDynamics的[RIG-Omni](https://github.com/LuwuDynamics/rig_omni/tree/main)项目二次开发。

# 硬件
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
### 编译
#### 克隆仓库
git clone https://github.com/LuwuDynamics/rig_omni.git RIG-Omni<br>
cd RIG-Omni

#### 激活ESP-IDF 环境
source ~/esp/esp-idf/export.sh<br>

#### 编译 & 烧录
idf.py build<br>
idf.py -p /dev/ttyUSB0 flash monitor<br>
将 /dev/ttyUSB0 替换为实际串口，macOS 下通常为 /dev/cu.usbmodem…。<br>
