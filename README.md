开发环境：Linux 16.04
硬	   件：ESP8266MOD开发板，ESP8266EX芯片

环境配置：
安装python（2.7）和aos-cube
aos-cube是 AliOS Things 基于Python开发的项目管理工具包，依赖 Python 2.7 版本（64bits，2.7.14已验证）。主要分为两部分：python和pip安装、基于pip安装aos-cube及相关的依赖包。

# 安装python和pip
sudo apt-get install -y python
sudo apt-get install -y python-pip
# 完成python和pip安装后，再安装依赖库和aos-cube，步骤如下：
python -m pip install setuptools
python -m pip install wheel
python -m pip install aos-cube
# 如果在安装aos-cube遇到网络问题，可使用国内镜像源，步骤如下：
### 安装/升级 pip
python -m pip install --trusted-host=mirrors.aliyun.com -i 				https://mirrors.aliyun.com/pypi/simple/ --upgrade pip

### 基于pip依次安装第三方包和aos-cube
pip install --trusted-host=mirrors.aliyun.com -i 		https://mirrors.aliyun.com/pypi/simple/   setuptools
pip install --trusted-host=mirrors.aliyun.com -i https://mirrors.aliyun.com/pypi/simple/   wheel
pip install --trusted-host=mirrors.aliyun.com -i https://mirrors.aliyun.com/pypi/simple/   aos-cube

### 如需要使用doubanio作备用源，如需指定版本，可改成如aos-		cube==0.2.50
pip install  --trusted-host pypi.doubanio.com -i  http://pypi.doubanio.com/simple/  aos-cube
下载AliOS-Things源：
git clone https://gitee.com/alios-things/AliOS-Things.git

编译bin文件：
cd AliOS-Things
注意：
此时默认为主版本
通过git branch -a查看分支
需要切换到1.3.3版本（或更高的版本）
切换之后编译才会有xxxxx-0x1000.bin文件，若在住版本上编译不会有可用bin文件
git checkout -b rel_1.3.3 origin/rel_1.3.3
aos make clean
aos make linkkitapp@esp8266

烧写bin文件：
将AliOS-Things/out/linkkitapp@esp8266/binary/linkkitapp@esp8266-0x1000.bin
AliOS-Things/platform/mcu/esp8266/bsp/下的boot_v1.7_921600.bin、blank.bin、esp_init_data_default.bin
移动到Windows下，使用ESP官方的flash烧写文件按照下图配置烧写：

串口调试助手
波特率为：921600
