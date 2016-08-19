# Gazebo仿真
---
官网英文原文地址：http://dev.px4.io/simulation-gazebo.html

# Gazebo 仿真

[Gazebo](http://gazebosim.org) 是一个自动机械手3D 模拟环境 . 它能够使用ROS 就像使用完整或独立的机器人仿真套件一样, 本指南包括简单的设置独立的操作。

{% youtube %}https://www.youtube.com/watch?v=qfFF9-0k4KA&vq=hd720{% endyoutube %}

{% mermaid %}
graph LR;
  Gazebo-->Plugin;
  Plugin-->MAVLink;
  MAVLink-->SITL;
{% endmermaid %}


## 安装

安装请求安装 Gazebo 和仿真插件.

<aside class="tip">
Gazebo 版本 6 可以使用. Linux 使用者: 如果你已经安装一个比Jade更早的ROS版本 , 务必卸载捆绑 Gazebo (sudo apt-get remove ros-indigo-gazebo) 太旧的版本 .
</aside>

### Mac OS

Mac OS 请求安装 Gazebo 6.

<div class="host-code"></div>

```sh
brew install gazebo6
```

### Linux安装

 PX4 SITL使用 the Gazebo 仿真, 但不依靠 ROS仿真也能够 像普通的飞行代码的同样方式[联接到ROS](../4_Simulation/interfacingto_ros.md) .

#### ROS 使用者

如果计划使用带 ROS的PX4 , 一定要遵循  [Gazebo 版本6指南](http://gazebosim.org/tutorials?tut=ros_wrapper_versions#Gazebo6.xseries) 使用 ROS.

#### 普通安装

遵循 [Linux 安装指令](http://gazebosim.org/tutorials?tut=install_ubuntu&ver=6.0&cat=install) 安装 Gazebo 6.

## 运行仿真

PX4固件是能在一个飞行器 PX4 SITL模拟器 (支持四轴, 固定翼 和 垂直飞降, 包括光流)的源目录上运行:

### 四旋翼

<div class="host-code"></div>

```sh
cd ~/src/Firmware
make posix_sitl_default gazebo
```

### 带光流四旋翼

<div class="host-code"></div>

```sh
cd ~/src/Firmware
make posix gazebo_iris_opt_flow
```

### 标准垂直起降

<div class="host-code"></div>

```sh
cd ~/src/Firmware
make posix_sitl_default gazebo_standard_vtol
```

### Tailsitter垂直起降 

<div class="host-code"></div>

```sh
cd ~/src/Firmware
make posix_sitl_default gazebo_tailsitter
```

<aside class="tip">
如果你遇到任何错误或者缺少的依赖项，一定要遵循 [安装文件和代码](http://dev.px4.io/starting-installing-mac.html) 指南适配于你的操作系统。
<aside>

这提到 PX4 shell:

```sh
[init] shell id: 140735313310464
[init] task name: mainapp

______  __   __    ___
| ___ \ \ \ / /   /   |
| |_/ /  \ V /   / /| |
|  __/   /   \  / /_| |
| |     / /^\ \ \___  |
\_|     \/   \/     |_/

准备飞行.


pxh>
```

<aside class="note">
正确检查四轴模式是否允许从内容菜单中启用“跟随模式”, 这是方便保持它在视图 .
</aside>

## 飞在空中

 ![gazebo](../pictures/sim\gazebo.png)

一旦它完成了初始化后，系统将显现原点。  (`telem> home: 55.7533950, 37.6254270, -0.00`). 你能靠输入命令验证:

```sh
pxh> commander takeoff
```

<aside class="tip">
 可以通过地面站(QGC)用手动输入支持操纵杆或拇指操纵杆 , 把系统打到手动飞行模式 (e.g. POSCTL, 位置控制).从地面站参数菜单中启动拇指操纵杆。
</aside>

## 扩展和自定义

扩展或者自定义仿真接口, 编辑文档在 `Tools/sitl_gazebo` 文件夹. 代码数据能够通过 [sitl_gazebo repository](https://github.com/px4/sitl_gazebo) 在 Github网站上取得.

<aside class="note">
建立系统实施被检验正确的子模块的所有依赖项, 包括模拟器. 它不会覆盖目录中的文件的更改, 然而, 当这些改变是继承了需要在固件中重新获得新的HASH协议注册的子模块.  这样做, `git add Tools/sitl_gazebo` 和继承修改. 这将更新模拟器的 GIT hash.
</aside>

## 联接到ROS

仿真能够 [联接到 ROS](../4_Simulation/interfacingto_ros.md) 同样方式像在使用一辆真车一样.
