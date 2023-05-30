# upgradeMgr使用手册
## 一、upgradeMgr功能（以下简称主控程序）
1.主控程序内部实现了一个http server用于和J3进行文件传输并接收差分供应商SDA组件的指令。

2.主控程序除了http相关实现外，还实现了zmq的resp端用以和DM通信，实现了2*req端用以和J3及mcu升级控制程序通信。

3.主控程序以进程存在，并运行在TDA4内部。

---

## 二、主控程序编译
holobuilder build qh01_soc_app/upgradeMgr -f

holobuilder的安装请参考相关手册。

## 2.1 holobuilder配置编译环境
下面的指令中workspace是个人的工作空间

mkdir workspace

cd workspace

holobuilder create

holobuilder configure --build_platform aarch64-linux-tda4-tisdk820-QH01 --build_product HoloARK/holoark1.0/qh01_ota --build_type release

holobuilder download --crosstool

holobuilder build holo_ota_app/updateMgr -r

---

## 三、主控程序源码目录说明
CMakeLists.txt: 编译配置文件

config: 进程配置文件，配置J3的IP，线程池线程数量等

include: 头文件，里面使用到了开源的Json解析代码nolhmann

README.md: 关于主控程序的一些说明也就是本文档

lib: UA的静态库和tda4 bsp提供的动态库

src: src下面就是源代码

test: 里面写了一些测试代码用于部分接口的前期测试，并实现了所有测试文件的编译

---

## 四、注意
主控程序目前完全是按照QHO1奇瑞需求而开发的，详细代码逻辑请参考：[[OTA HLD](https://holomatic.feishu.cn/docx/JofwdGKqMoxYPnxa5nbcdztBn0f)]

---

