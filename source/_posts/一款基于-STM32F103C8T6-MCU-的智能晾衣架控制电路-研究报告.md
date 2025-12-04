---
title: 一款基于 STM32F103C8T6 MCU 的智能晾衣架控制电路 研究报告
date: 2025-12-04 21:57:49
tags: 
	- 嵌入式开发
	- 单片机
	- STM32
	- ESP8266
	- 结题报告
	- 研究性学习
	- 计算机
	- 华师一附中回忆录
cover: https://gh.404cafe.fun/https://raw.githubusercontent.com/LuccaWang404/luccawang404.github.io/refs/heads/img/IMG/2025-12-04/11c031507658bac9ca87156a7fc6cc75.jpg
---
# 一款基于 STM32F103C8T6 MCU 的智能晾衣架控制电路</br>
<center><b>——小组研究报告篇</b></center>
</br>

<div align="center">
	<img src="https://gh.404cafe.fun/https://raw.githubusercontent.com/LuccaWang404/luccawang404.github.io/refs/heads/img/IMG/2025-12-04/Tools.svg"></img>
	<img src="https://gh.404cafe.fun/https://raw.githubusercontent.com/LuccaWang404/luccawang404.github.io/refs/heads/img/IMG/2025-12-04/ESP8266EX-000000.svg"></img>
	<img src="https://gh.404cafe.fun/https://raw.githubusercontent.com/LuccaWang404/luccawang404.github.io/refs/heads/img/IMG/2025-12-04/STM32F103C8T6-000000.svg"></img>
	<img src="https://gh.404cafe.fun/https://raw.githubusercontent.com/LuccaWang404/luccawang404.github.io/refs/heads/img/IMG/2025-12-04/C & C++ Language-00599C.svg"></img>
	<img src="https://gh.404cafe.fun/https://raw.githubusercontent.com/LuccaWang404/luccawang404.github.io/refs/heads/img/IMG/2025-12-04/OpenSource-GPLv3-00599C.svg"></img>
</div>



***Product proudly developed by 王俊皓 (In code: LuccaWang404) with ❤ & ✨.***

***All support thankfully from 谭锦程、方鹏杰、张熙正、杜文彬、陈恩卓、宋子洋 .***

***Report proudly written by 王俊皓.***



## I.前言

### 1. 鸣谢

*本项目的诞生离不开谭锦程同学、方鹏杰同学、张熙正同学、杜文彬同学、陈恩卓同学、宋子洋同学（排名不分先后）不遗余力的支持。*

***在此对他们致以最诚挚的感谢。***

### 2. 关于代码、技术细节

- 本项目开发时间紧迫，本组没来得及找到合适的指导老师，所有代码、硬件开发均由王俊皓同学独立完成。

- 本项目代码共**迭代7次**，总代码量超***2000行***，详情请见下文**IV.5.*困难&解决方案***部分。

- 与本项目有关的技术细节请参考下文***技术分析/解读***部分。

- 本项目已根据GPLv3协议在校园内网CG社代码托管服务站上 [**开放源代码**](http://git.cg.mcfx.xyz/LuccaWang404/goddamn_clothes_hanger_stm32_v1_rev1)。

>  //注：校外公网暂时无法访问

### 3. 背景&立项

夏天到了，天气说变就变。有时候，一场毫无征兆的大雨就可能让我们正在晾晒的衣物湿透，白费了我们洗衣服的辛苦付出。看到劳动成果泡汤除了让我们抓狂，也让我们对晾衣服的方式产生了思考。

为着手解决雨天不能及时收衣服的问题，在组长谭锦程和开发负责人王俊皓的统筹下，我们小组提出了”智能晾衣架控制电路“这一研究课题。

## II. 关于本组

### 1. 本组信息

- 班级：23级17班（ 高一 (17) 班 ）
- 组长：谭锦程
- 副组长：王俊皓
- 开发负责：王俊皓
- 问卷设计：谭锦程、方鹏杰
- 问卷分析：张熙正、杜文彬、陈恩卓、宋子洋
- 摄影：方鹏杰
- 总结PPT制作：王俊皓
- 指导老师：不知道
- 调查时间：2024.05.26~2024.06.01
- 调查途径：问卷
- 调查对象：网友、同学
- 研究方法：调查问卷法、查阅资料法、现场采访法、试错迭代法
- 研究目的：推出一款智能晾衣架控制电路，解决雨天忘收衣服的问题
- 产品开发途径：嵌入式开发技术文档、已掌握的编程知识

### 2. 我们的研究规划

- 开展线上问卷调查
- 分析问卷调查结果
- 根据结果确定研究目标
- 完成既定目标，迭代开发出最终产品

## III. 问卷Q&A分析、我们的目标

> 在谭锦程同学的主持下，我们于2024年5月26日至6月1日使用问卷星开展了为期一周的线上公开问卷调查。
>
> 以下是张熙正、杜文彬、陈恩卓、宋子洋同学对收到的有效问卷的结果分析。

### Q1. 您和您的家人在日常生活中是否受到过“下雨时人不在家，衣服在阳台上没人收”的困扰？

![Q1](https://gh.404cafe.fun/https://raw.githubusercontent.com/LuccaWang404/luccawang404.github.io/refs/heads/img/IMG/2025-12-04/chart_01_rain_without_react.png)

>  选择了”是“的受访者占比超75%。

可见大多数受访者有过雨天忘收衣服的经历，这说明我们组有开发本款智能晾衣架控制电路的必要性。

### Q2. 您有使用智能晾衣架（具有自动控制、远程互联、环境感知等功能的晾衣架）的需求吗？

![Q2](https://gh.404cafe.fun/https://raw.githubusercontent.com/LuccaWang404/luccawang404.github.io/refs/heads/img/IMG/2025-12-04/chart_02_demands.png)

>  选择了”是“的受访者接近60%。

过半数的受访者有晾衣架自动控制功能的需求，这表明本组有必要在产品开发中实现此类功能。

### Q3. 室外智能晾衣架可根据天气变化调整晾晒策略，如在即将下雨时自动回收衣物

![Q3](https://gh.404cafe.fun/https://raw.githubusercontent.com/LuccaWang404/luccawang404.github.io/refs/heads/img/IMG/2025-12-04/chart_03_weather.png)

> 超过60%的受访者表示有该功能时”很喜欢“；然而没有该功能时受访者们的反应参差不齐，绝大多数受访者对此类功能的需求并不迫切。

由此可见，绝大多数人对这类功能的需求并不迫切，没有实现的必要；另外，添加”自动调整晾晒策略“还会向本产品引入物联网模块，使产品拥有成本陡增，不能满足人们对产品性价比的要求。所以我们退而求其次，开发了一种更经济的快速反应型补救措施，在更低的价格上实现了相似的功能，具体细节请参考后文***IV.4.技术分析/解读***部分。

### Q4. 室外智能晾衣架可以接入智能家居生态来联动其他智能家具

![Q4](https://gh.404cafe.fun/https://raw.githubusercontent.com/LuccaWang404/luccawang404.github.io/refs/heads/img/IMG/2025-12-04/chart_04_IOT.png)

> 本题中大多数受访者对没有对此类功能的反应为”无所谓“，没有此方面的迫切需求。

与Q3的结论类似，从成本上、需求上考虑，没有开发该功能的必要。

**但是，若研究进展顺利，可以考虑添加WIFI模块以实现更复杂的拓展功能。**

### Q5. 室外智能晾衣架可手机或遥控进行智能远程控制

![Q5](https://gh.404cafe.fun/https://raw.githubusercontent.com/LuccaWang404/luccawang404.github.io/refs/heads/img/IMG/2025-12-04/chart_05_remote_control.png)

> 本题中大多数受访者能够接受没有这类功能，但我们注意到有超过1/4的受访者很不喜欢没有这类功能

经过组内讨论，我们一致认为晾衣架实现自动控制已经能满足绝大多数的需求，没有必要添加远程控制的功能。有关自动控制的内容，请参考后文***IV.4.技术分析/解读***部分。

### Q6*. 室外智能晾衣架的材料耐久度高，结构稳固

![Q6](https://gh.404cafe.fun/https://raw.githubusercontent.com/LuccaWang404/luccawang404.github.io/refs/heads/img/IMG/2025-12-04/chart_06_durability.png)

> 大多数受访者认为晾衣架必须坚固耐用

**本题不在本组的研究范畴内，但是也让我们了解到了对晾衣架材料的要求，这可以作为我们日后的努力方向。*

### Q7*. 室外智能晾衣架有更稳定的衣夹子或不易让三角衣架脱落的挂孔，以避免衣物掉落

![Q7](https://gh.404cafe.fun/https://raw.githubusercontent.com/LuccaWang404/luccawang404.github.io/refs/heads/img/IMG/2025-12-04/chart_07_clips.png)

> 本题数据与Q6完全一致。大多数受访者认为晾衣架必须要有防止衣物脱落的的功能

虽然本题同Q6一样，不在我们的研究范畴内，但我们在控制程序中添加了防止衣物脱落的细节，请参考后文***IV.4.技术分析/解读***部分。

### ~~Q8*. 您认为智能晾衣架还应该具备哪些功能？~~

![WTF](https://gh.404cafe.fun/https://raw.githubusercontent.com/LuccaWang404/luccawang404.github.io/refs/heads/img/IMG/2025-12-04/WTF.png)

![WTF2](https://gh.404cafe.fun/https://raw.githubusercontent.com/LuccaWang404/luccawang404.github.io/refs/heads/img/IMG/2025-12-04/WTF2.png)

~~这都是些啥玩意儿啊？？？~~

> ~~开放问题，但收到的答案要么是”无“，要么就过于离谱，不在此赘述。~~

### G. 我们的目标

分析问卷结果后，我们拟定的研究目标如下：

- [ ] 制定出符合用户需求的控制方案
- [ ] 根据控制方案拟出硬件方案
- [ ] 了解各类硬件原理
- [ ] 根据硬件方案采购合适的硬件
- [ ] 学习使用STM32开发板
- [ ] 测试开发板、传感器功能
- [ ] 分别实现各传感模块的功能
- [ ] 并行测试各传感器功能
- [ ] 编写环境感应、条件判定部分代码
- [ ] 测试环境感应、条件判定部分代码
- [ ] 编写晾衣架控制模块代码
- [ ] 测试晾衣架控制部分代码
- [ ] 迭代、优化代码结构
- [ ] 测试全部代码
- [ ] 编译程序最终版本
- [ ] 烧录程序，运行全部模块

- [ ] *[附加任务]完成多平台程序移植
- [ ] *[附加任务]加入远程控制、联网模块代码
- [ ] *[附加任务]编写远程控制、物联网模块代码
- [ ] *[附加任务]编写获取天气信息代码
- [ ] *[附加任务]整合物联网模块
- [ ] *[附加任务]完成多语言交叉编译
- [ ] *[附加任务]将源代码发布到开源平台
- [ ] *[附加任务]尽可能地控制成本少于100元
- [ ] 整合所有模块
- [ ] 发布产品

## IV. 研究实现

### 0*. 关键名词解释

#### 1). MCU

微控制单元(Microcontroller Unit；MCU) ，又称单片微型计算机(Single Chip Microcomputer )或者单片机，是把中央处理器(Central Process Unit；CPU)的频率与规格做适当缩减，并将内存(memory)、计数器(Timer)、USB、A/D转换、UART、PLC、DMA等周边接口，甚至LCD驱动电路都整合在单一芯片上，形成芯片级的计算机，为不同的应用场合做不同组合控制。诸如手机、PC外围、遥控器，至汽车电子、工业上的步进马达、机器手臂的控制等，都可见到MCU的身影。

***<u>下文中STM32、ESP8266、ESP32都是MCU。</u>***

附STM32芯片示意图（来自CubeMX）：

![chip](https://gh.404cafe.fun/https://raw.githubusercontent.com/LuccaWang404/luccawang404.github.io/refs/heads/img/IMG/2025-12-04/stm32_chip.png)

#### 2). C / C++

计算机高级程序设计语言，C++由C语言扩展升级而产生。

#### 3). DHT11

DHT11是一款有已校准数字信号输出的温湿度传感器。 其精度湿度±5%RH， 温度±2℃，量程湿度5~95%RH， 温度-20~+60℃。

![DHT11](https://gh.404cafe.fun/https://raw.githubusercontent.com/LuccaWang404/luccawang404.github.io/refs/heads/img/IMG/2025-12-04/DHT11.png)

上图：DHT11传感器实物图

![](https://gh.404cafe.fun/https://raw.githubusercontent.com/LuccaWang404/luccawang404.github.io/refs/heads/img/IMG/2025-12-04/dht11.jpg)

上图：DHT11原理图

#### 4). GY-302 (BH-1750)

GY-302(A.K.A. BH1750FVI)， 是一种用于两线式串行总线接口的数字型光强度传感器集成电路。这种集成电路可以根据收集的光线强度数据来调整液晶或者键盘背景灯的亮度。利用它的高分辨率可以探测较大范围的光强度变化。

该集成电路内部由光敏二极管、运算放大器、ADC采集、晶振等组成。PD二极管通过光生伏特效应将输入光信号转换成电信号，经运算放大电路放大后，由ADC采集电压，然后通过逻辑电路转换成16位二进制数存储在内部的寄存器中（光照越强，光电流越大，电压就越大）。

![GY-302-1](https://gh.404cafe.fun/https://raw.githubusercontent.com/LuccaWang404/luccawang404.github.io/refs/heads/img/IMG/2025-12-04/gy-302.png)

上图：GY-302传感器实物图

![GY-302-2](https://gh.404cafe.fun/https://raw.githubusercontent.com/LuccaWang404/luccawang404.github.io/refs/heads/img/IMG/2025-12-04/gy-302-02.png)

上图：GY-302传感器原理图

#### 5). DO

即Digital Output，数字输出。信号输出为高/低电平，对应开关量。

#### 6). IIC总线

即Inter-Integrated Circuit，集成电路总线，又写作I2C，一种串行通信总线。

#### 7). 引脚

引脚，又叫管脚，英文叫Pin。就是从集成电路*（芯片）*内部电路引出与外围电路的接线，所有的引脚就构成了这块芯片的接口。

### 1. 硬件选择

查阅CSDN我们得知，目前嵌入式微控制器有如下两种主流方案：

- STM32，成本低，开发难度较高
- ESP8266 / ESP32，成本较高，但上手难度较低

**经过讨论，我们决定从成本出发，选择了STM32。**

*根据我们分析得出的硬件方案，我们采购了以下硬件：*

- STM32开发板*1

  → STM32F103C8T6最小系统板。

  *** *这种开发板串口输出不可用，故在代码部分注释掉了所有串口输出语句***

- 雨水传感器*1

  → 型号未知，带驱动板

- 光电传感器*1

  → GY-302 (BH-1750)

- 温湿度传感器*1

  → DHT11

- 5kg大扭矩舵机*1

  → SG-5010

- 5V 电源*1 (Micro-USB接口)

- 面包板*1

### 2. 线路连接

查阅资料，我们得到了STM32F103 MCU的引脚图：

![STM32_MCU](https://gh.404cafe.fun/https://raw.githubusercontent.com/LuccaWang404/luccawang404.github.io/refs/heads/img/IMG/2025-12-04/MCU_PINS.png)

以及各引脚功能对照表：

![PIN_01](https://gh.404cafe.fun/https://raw.githubusercontent.com/LuccaWang404/luccawang404.github.io/refs/heads/img/IMG/2025-12-04/PIN_01.png)

![PIN_02](https://gh.404cafe.fun/https://raw.githubusercontent.com/LuccaWang404/luccawang404.github.io/refs/heads/img/IMG/2025-12-04/PIN_02.png)

![PIN_03](https://gh.404cafe.fun/https://raw.githubusercontent.com/LuccaWang404/luccawang404.github.io/refs/heads/img/IMG/2025-12-04/PIN_03.png)

查阅分析后，我们讨论出了这样的线路连接方案：

#### 1). 供电

- 3.3V、GND引脚连接导电槽，为硬件系统提供整体供电

#### 2). 传感器、数据引脚连接

- DHT11数据引脚连接STM32的PA1引脚
- 雨水传感器的DO引脚连接STM32的PB5引脚
- GY-302光敏传感器的SCL、SDA引脚分别连接STM32的PB6、PB7引脚，ADDR引脚连接导电槽负极通过GND引脚接地
- 舵机数据引脚连接PA2

这样的连接方案会让各线路相对集中，便于我们检查连接和排除故障。另外，我们在测试完硬件后将所有可更换的面包线换成了面包板跳线，进一步增强了本控制系统的可靠性。

### 3. 程序设计（控制方案）

经过考虑，王俊皓同学选择了程序结构简洁、编程暗病较少的Arduino IDE。

构建工程前，我们在开发环境中安装了STM32开发板支持库和GY-302(BH-1750)、DHT11传感器驱动。

> *后文中，`//Serial.print("...");`为弃用的串口输出部分，相关语句来自本产品的ESP8266版本。

程序逻辑判定如下：

#### 1). 回收衣物条件判定

##### i. 温湿度因素

使用DHT11传感器探测环境温度，当环境温度小于0℃、大于45℃时或湿度超过90%时收回衣物。
```C++
//DHT11温湿度传感器驱动
#include "DHT11.h"
DHT11 dht11(A1);
```
> 上：DHT11驱动、引脚初始化部分 
```c++
bool is_wet() {
	//Serial.print(dht11.readHumidity());
	//Serial.println(" %\t");
	if (dht11.readHumidity() >= 90) {
  		//Serial.println("EXTREME HUMIDITY DETECTED!");
  		return true;
	}
	else return false;
}

bool is_heat_extreme() {
	//Serial.print(dht11.readTemperature());
	//Serial.println(" Celsius\t");
	if (dht11.readTemperature() >= 45 || dht11.readTemperature() <= 0) {
  		//Serial.println("EXTREME HEAT DETECTED!");
  		return true;
	}
	else return false;
}
```
> 上：DHT11环境条件判断函数

##### ii. 光照因素

使用GY-302探测环境光线，若环境光线低于设定阈值（光照强度低于15 lux），衣物收回。

*GY-302传感器使用IIC通信协议，需要在代码中添加IIC驱动
```c++
//启用IIC总线协议
#include "Wire.h"
//BH-1750(GY-302)光敏传感器驱动
#include "BH1750.h"

BH1750 ENV_LIGHT;
```
> 上：GY-302(BH-1750)驱动、IIC通信协议初始化

```c++
bool is_night() {
  //Serial.print(ENV_LIGHT.readLightLevel());
  //Serial.println(" [lux]\t");
  if (ENV_LIGHT.readLightLevel() < 15) {
    //Serial.println("LOW LIGHT DETECTED!");
    return true;
  }
  else return false;
}
> 上：GY-302环境判断函数

##### iii. 降水因素

雨滴落在雨水传感器表面会接通探测线路，传感器模块DO引脚会输出低电平，即`false`值，以此作为判定条件则有：
```c++
bool is_raining() {
  if (!digitalRead(PB5)) {
    //Serial.println("RAINDROPS DETECTED!");
    return true;
  }
  else return false;
}
```
#### 2). 晾出衣物条件判定（基本上可以参考第一项）

- 温度正常（0~45℃）
- 湿度正常（<90%）
- 光照大于阈值
- 不下雨

#### 3). 舵机操作函数

为避免舵机反复操作，王俊皓同学于程序中加入了一个bool类的flag——`is_servo_out`，具体代码如下：
```c++
bool is_servo_out = true;

void hanger_init() {
  for (int pos = 0; pos <= 75; pos ++) {
    digitalWrite(PC13, LOW);
    delay(25);
    digitalWrite(PC13, HIGH);
    delay(25);
    Servo_01.write(pos);					
  }
  is_servo_out = true;
}

void servo_out() {
  if ( is_servo_out == true ) Serial.println("HANGER IS OUT!");
  else{
    for (int pos = 0; pos <= 75; pos ++) {
      digitalWrite(PC13, LOW);
      delay(25);
      digitalWrite(PC13, HIGH);
      delay(25);
      Servo_01.write(pos);					
    }
  }
}

void servo_back() {
  if ( is_servo_out == false ) Serial.println("HANGER IS BACK!");
  else{
    for (int pos = 75; pos >= 0; pos --) {
      digitalWrite(PC13, LOW);
      delay(25);
      digitalWrite(PC13, HIGH);
      delay(25);
      Servo_01.write(pos);					
    }
  }
}
```
根据程序设计，在舵机操作时，STM32开发板上的蓝灯会快速闪烁指示操作状态。

#### 4). 晾衣架逻辑判断、操作函数

该函数会评估条件，循环执行。

在`is_raining()`、`is_night()`、`is_wet()`、`is_heat_extreme()`四个函数中只要有一个返回值为`true`，同时`is_servo_out`的flag值为`true`，则晾衣架收回。

简而言之，如果符合晾晒衣物的条件，则晾衣架伸出；反之，晾衣架收回。
```c++
void hanger_operation() {
  if ( is_raining() || is_night() || is_wet() || is_heat_extreme() && is_servo_out ) {
    //Serial.println("ABNORMAL ENVIRONMENT! COLLECTING BACK CLOTHES...");
    servo_back();
    is_servo_out = false;
  }
  else {
    //Serial.println("NORMAL ENVIRONMENT!");
    servo_out();
    is_servo_out = true;
  }
}
```
#### 5). 完整代码

以上为本晾衣架控制电路程序设计部分。下面展示本程序完整代码。

如果需要项目源文件，可前往本项目的开原页面。详见***I.2.关于代码、技术细节***。
```c++
/*------------------------------------------头文件------------------------------------------*/

//BH-1750(GY-302)光敏传感器驱动
#include "BH1750.h"

//DHT11温湿度传感器驱动
#include "DHT11.h"

//舵机驱动
#include "Servo.h"

//启用IIC总线协议
#include "Wire.h"


/*------------------------------------------头文件------------------------------------------*/

/*------------------------------------------硬件初始化------------------------------------------*/

//各模块驱动类声明，定义本程序中传感器名称
BH1750 ENV_LIGHT;
DHT11 dht11(PA1);
Servo Servo_01;
bool is_servo_out = true;

void hanger_init() {
  for (int pos = 0; pos <= 75; pos ++) {
    digitalWrite(PC13, LOW);
    delay(25);
    digitalWrite(PC13, HIGH);
    delay(25);
    Servo_01.write(pos);					
  }
  is_servo_out = true;
}

void setup() {
  
  Wire.begin();
  ENV_LIGHT.begin();
  Servo_01.attach(PA4, 500, 2500);
  //Serial.begin(115200);
  pinMode(PB5, INPUT);
  pinMode(PC13, OUTPUT); //晾衣指示灯：开发板载LED，对应PC13引脚
  hanger_init();

}

/*------------------------------------------硬件初始化------------------------------------------*/


/*---------------------环境监测判断函数---------------------*/

bool is_raining() {
  if (!digitalRead(PB5)) {
    //Serial.println("RAINDROPS DETECTED!");
    return true;
  }
  else return false;
}

bool is_night() {
  //Serial.print(ENV_LIGHT.readLightLevel());
  //Serial.println(" [lux]\t");
  if (ENV_LIGHT.readLightLevel() < 15) {
    //Serial.println("LOW LIGHT DETECTED!");
    return true;
  }
  else return false;
}

bool is_wet() {
  //Serial.print(dht11.readHumidity());
  //Serial.println(" %\t");
  if (dht11.readHumidity() >= 90) {
    //Serial.println("EXTREME HUMIDITY DETECTED!");
    return true;
  }
  else return false;
}

bool is_heat_extreme() {
  //Serial.print(dht11.readTemperature());
  //Serial.println(" Celsius\t");
  if (dht11.readTemperature() >= 45 || dht11.readTemperature() <= 0) {
    //Serial.println("EXTREME HEAT DETECTED!");
    return true;
  }
  else return false;
}

/*---------------------环境监测判断函数---------------------*/

void normal_env() {
  digitalWrite(PC13, LOW); //环境正常，晾衣指示灯亮
}

void abnormal_env() {
  digitalWrite(PC13, HIGH); //环境不正常，晾衣指示灯灭
}

void servo_out() {
  if ( is_servo_out == true ) normal_env(); //Serial.println("HANGER IS OUT!");
  else{
    for (int pos = 0; pos <= 75; pos ++) {
      digitalWrite(PC13, LOW);
      delay(25);
      digitalWrite(PC13, HIGH);
      delay(25);
      Servo_01.write(pos);					
    }
    normal_env();
  }
}

void servo_back() {
  if ( is_servo_out == false ) abnormal_env(); //Serial.println("HANGER IS BACK!");
  else{
    for (int pos = 75; pos >= 0; pos --) {
      digitalWrite(PC13, LOW);
      delay(25);
      digitalWrite(PC13, HIGH);
      delay(25);
      Servo_01.write(pos);					
    }
    abnormal_env();
  }
}

void hanger_operation() {
  if ( is_raining() || is_night() || is_wet() || is_heat_extreme() && is_servo_out ) {
    //Serial.println("ABNORMAL ENVIRONMENT! COLLECTING BACK CLOTHES...");
    servo_back();
    is_servo_out = false;
  }
  else {
    //Serial.println("NORMAL ENVIRONMENT!");
    servo_out();
    is_servo_out = true;
  }
}



void loop() {
  hanger_operation();
}
```
### 4. 技术分析/解读 Q&A

#### Q1. 怎么查看晾衣架控制电路的工作状态？

> A：可以看核心板上的指示灯。红灯亮，电源接通正常；蓝灯亮，晾衣架已伸出，处于正常晾晒状态；蓝灯灭，晾衣架已收回，天气不满足晾晒条件；蓝灯闪烁，晾衣架正在伸出或收回。

#### Q2. 为什么把晾晒温度设置为0~45℃？

> A: 防止衣物结冰、防止太阳晒坏衣服

#### Q3. 为什么要把晾晒湿度设置为低于90%？

> A: 防止衣物久晾不干产生异味

#### Q4. 为什么将晾晒光照阈值设置为15 lux?

> A: 请参考以下亮度对照表。查阅可知白天光照阈值约为15 lux。
>
> ![Lux](https://gh.404cafe.fun/https://raw.githubusercontent.com/LuccaWang404/luccawang404.github.io/refs/heads/img/IMG/2025-12-04/light.png)

#### Q5. 下雪了怎么办？

> A: 雪能融化，则能接通雨水传感器；雪不能融化，则温度会低于温湿度传感器设定阈值。

#### Q6. 防止衣物掉落的措施是什么？快速反应型补救措施是什么？

> A: 只要符合晾出/回收条件，开发板会将启动信号传给大扭矩舵机，使之**缓慢转动**（25ms/°），控制晾衣架在10s内完成伸缩的同时确保衣物不会掉落。

### 5. 研究开发遇到的困难&解决方案（开发负责人の自述）

得益于组内同学的全力相助，我们顺利地完成了产品开发的所有如统计、分析、设计的研究任务。

**然而**，轮到我来开发最终产品时，噩梦开始了......

#### 1). 初识STM32？

~~我在挑选硬件时光考虑价格去了，完全没有想到后续开发难度是地狱级的......~~

~~结果收到东西后去查了下开发文档，直接被各种专业性极高的技术文档搞懵了，完全不知道从什么地方下手......~~

查了下嵌入式开发初学者入门教程，我决定先从点亮一只LED灯开始做起。

也不知犯了神马迷糊，盲目地跟着网上的逆天教程选了难度爆表、对初学者极其不友好的的Keil μVision 5，写出了我的第一个点灯程序。看到面包板上一闪一闪的LED，我竟觉得这玩意很简单，开发工期不会太长。结果倒好，在尝试接入各种传感器后，我破防了：引入外部驱动就报错，各类头文件丢失，花式编译失败，HAL库配置不正确......种种问题让我在不断地迭代中耗尽了耐心，最后果断放弃了Keil。

弃坑了Keil，总是得找到第二款开发软件。查了查主流的IDE，另一款开发工具吸引了我的注意：RT-Thread Studio（以下简称RTTS）。RTTS对芯片引脚的快速声明、初始化是我选择它的主要原因。在这款软件的帮助下，我完成了雨水传感器模块、舵机模块、指示灯模块的开发工作。但是涉及到外部驱动的引入时，RTTS的缺陷也暴露了出来：生态不完善、官方底层驱动不适配导致GY-302、DHT11的开发陷入了困境。眼看预留的开发时间不足两天，经过艰难的心理斗争后，我弃用了这一条技术路线，选择了ESP8266和Arduino IDE。

周末在家，我最终还是选择了与我开发初衷相背离的路线——ESP路线。在我以往开发经验的加持下，我在8小时内完成了ESP8266驱动的控制电路的开发进程。开发成功时，已是凌晨五点半。看着成功在正常条件、异常条件下起转的舵机，我的心中除了成功的喜悦和成就感，也多了几分没能有效控制整体成本的遗憾。休息前，我告诉自己，如果这就是最后的办法了，明天就把结题报告写了吧......

然而，事情很快出现了转机。第二天，我猛然惊醒：为什么不能用Arduino IDE来开发STM32呢？想到这里，我马上查阅相关文档。根据文档说明，我安装了STM32的Arduino IDE适配开发插件，将原有的ESP8266程序进行移植性修改后，编译，运行成功！

迭代七次，写了超两千行代码后，我终于完成了我们的开发目标！

~~但不得不说，那个适配插件真是坑爹，内置编译器的最新版本有BUG，换了好几个版本才能成功，离大谱了属于是~~

#### 2). 传感器元器件没焊针脚？

到祸发现，GY-302的针脚没焊上。

为了测试硬件，我化身飞线仙人，用面包线把传感器钉在了面包板上，于是便有了经常接触不良的光敏传感模块......

后来总觉得这样绝对会出大问题，咬咬牙买了个电烙铁给它焊上了，测试引脚，均能正常使用。

~~从来没发现我这么会用电烙铁哈哈哈哈~~

#### 3). 传感器读数异常？

最开始那个DHT11在测试时，无论温度湿度总是返回253，很让人抓狂。后来看了店家的描述，发现是我接错了正负极，给它玩烧了......

后来换了一个，就能正常读数了。

~~真羞耻啊啊啊啊啊~~



## VI. 研究任务、目标完成情况

截止至研究结束，我们的研究任务、目标完成情况如下：

### 前置任务：

- [x] 确立研究项目选题
- [x] 立项
- [x] 确定研究方法
- [x] 分配研究任务
- [x] 开展问卷调查
- [x] 分析调查问卷
- [x] 制定出符合用户需求的控制方案

### 主线任务

- [x] 根据控制方案拟出硬件方案
- [x] 了解各类硬件原理
- [x] 根据硬件方案采购合适的硬件
- [x] 学习使用STM32开发板
- [x] 测试开发板、传感器功能
- [x] 分别实现各传感模块的功能
- [x] 并行测试各传感器功能
- [x] 编写环境感应、条件判定部分代码
- [x] 测试环境感应、条件判定部分代码
- [x] 编写晾衣架控制模块代码
- [x] 测试晾衣架控制部分代码
- [x] 迭代、优化代码结构
- [x] 测试全部代码
- [x] 编译程序最终版本
- [x] 烧录程序，运行全部模块

### 附加挑战：

- [x] *[附加任务]完成跨平台程序移植
- [ ] *[附加任务]加入远程控制、联网模块代码
- [ ] *[附加任务]编写远程控制、物联网模块代码
- [ ] *[附加任务]编写获取天气信息代码
- [ ] *[附加任务]整合物联网模块
- [x] *[附加任务]完成多语言交叉编译
- [x] *[附加任务]将源代码发布到开源平台
- [x] *[附加任务]尽可能地控制成本少于100元

### 最终任务：

- [x] 整合所有模块
- [x] 发布产品

## VII. 结论&建议

本次研究，我们历经千辛万苦，成功按计划开发出了我们设想中的产品。我们不仅出色地完成了开发主线任务，还完成了部分附加挑战，可谓收获满满。

回看市面上的同类产品，其价格至少是我们DIY出的最终产品的5倍，可见我们产品的极致性价比。讨论后，我们得出的建议如下：1、尽可能缩减控制器的成本；2、尽可能优化代码，提升代码执行效率；3、考虑用户需求，削减不必要功能；4、多次实验，尽可能获取相对可靠的控制参数。

## VIII. 遗憾&反思

然而，我们的产品开发进程看似完美结束，但最终产品仍有许多遗憾和缺陷。

远程控制、物联网模块、自动晾晒策略调整等诸多项目初期设想我们均未能在工期内实现，接触不良、控制电路体积过大、传感器不灵敏、线路复杂等诸多结症也值得我们反思。在以后的研究实践中，我们计划系统学习电路板设计、物联网等相关知识，进一步优化控制系统排线、布局等细节，进一步尝试讲我们的产品融入物联网家具生态链中。

另外，我们本次的研究比较偏原理方向。为了进一步验证产品可行性，我们也会在暑假尝试将控制电路实装到真正的晾衣架上，以进一步测试相关功能。

## IX. 感悟&总结

从项目落地到得出成果，我们前前后后花费了一个月的时间，一步一个脚印地走向了研究的最终成功。虽然没有100%完成我们最初的设想，但对自动化控制、嵌入式开发等领域的初步探索让我们收获颇丰。

在研究的过程中，我们进一步培养了合作精神和团队意识；此外，我们也在实践探究中增进了彼此间的友谊，感受到了默契协作的可贵。

最后，我们想用一句话来总结本次的研究性学习任务：

***有志者，事竟成。***

***Nothing is impossible to a willing heart.***

## X. 参考文档（部分不记得来源了）

[DHT11_百度百科 (baidu.com)](https://baike.baidu.com/item/DHT11/1206271)

[DHT11详细介绍（内含51和STM32代码）-CSDN博客](https://blog.csdn.net/m0_55849362/article/details/126426768)

[手把手教你玩转DHT11（原理+驱动） - 良许Linux - 博客园 (cnblogs.com)](https://www.cnblogs.com/yychuyu/articles/17892426.html)

[STM32--光照强度传感器（BH1750(GY-302)）_高精度光照度传感器 特定参数-CSDN博客](https://blog.csdn.net/weixin_45771489/article/details/123507030)

[电子模块|光照强度传感器模块 GY-302及其驱动（arduino、STC51、STM32）_gy302-CSDN博客](https://blog.csdn.net/qq_32761549/article/details/128549038)

[BH1750( GY-302 )光照传感器-CSDN博客](https://blog.csdn.net/Dustinthewine/article/details/127540711)

[STM32新手入门教程_stm32教程-CSDN博客 #这就是那个逆天入门教程](https://blog.csdn.net/xiaoshihd/article/details/110039281)

[stm32_百度百科 (baidu.com)](https://baike.baidu.com/item/STM32/9133302)

[RT-Thread Studio联合STM32CubeMX进行开发_rtthread与stm32cubemx联合开发-CSDN博客](https://blog.csdn.net/qq_45396672/article/details/118076336)

[RT-Thread | BH1750软件包的使用_rt如何添加bh1750-CSDN博客](https://blog.csdn.net/zhengnianli/article/details/106536624)

[【智能家居项目】RT-Thread版本——DHT11获取温湿度 | MQTT上传到服务器 | 服务器控制外设_rt-thread dth11获取温湿度-CSDN博客](https://blog.csdn.net/weixin_63726869/article/details/137120568)

[STM32-雨滴传感器_雨滴传感器stm32-CSDN博客](https://blog.csdn.net/qq_51458770/article/details/127861030)

[基于STM32F103入门1——点亮LED灯_multisim模拟一个stm32开关控制8个led的颜色-CSDN博客](https://blog.csdn.net/weixin_47457689/article/details/119395069)

[STM32使用RT-thread完成点灯，pwm，按键中断，定时器中断，ADC_rt thread pwm输出-CSDN博客](https://blog.csdn.net/hhcgn/article/details/134017326)

[STM32 —— USB 转 TTL（CH340）-CSDN博客](https://blog.csdn.net/m0_59161987/article/details/128480063)

[stm32最小系统USB转TTL接线_usb-ttl: 5v<->5v gnd<->gnd rxd<->pa9 txd<->pa10-CSDN博客](https://blog.csdn.net/qq_36784975/article/details/87860098)

[STM32简介（系统结构、引脚定义……）_stm32引脚功能介绍-CSDN博客](https://blog.csdn.net/Neu_leizi/article/details/124871639)

[【硬件基础】STM32F103C8T6芯片引脚定义及功能介绍_stm32f103c8t6引脚图及功能-CSDN博客](https://blog.csdn.net/weixin_60324241/article/details/136492164)

[通常环境光照度参照表_光照强度1000lux相当于什么-CSDN博客](https://blog.csdn.net/banrieen/article/details/51190688)

[Arduino借助STM32Duino开发STM32教程-(2023年8月)-CSDN博客](https://blog.csdn.net/m0_46236949/article/details/132381810)

[使用ArduinoIDE进行STM32开发（STM32duino）环境配置方法_stm32 arduinoide开发-CSDN博客](https://blog.csdn.net/shineber/article/details/136891901)

[ST-Link驱动的下载、安装、配置，以及ST-Link固件的升级_stlink驱动-CSDN博客](https://blog.csdn.net/qq_52102933/article/details/126830904)

[Arduino控制舵机详解（含代码）_arduino舵机控制程序-CSDN博客](https://blog.csdn.net/m0_58857684/article/details/125740665)

[用 Arduino 控制舵机 – Arduino 实验室 (nxez.com)](https://arduino.nxez.com/2016/12/20/use-arduino-to-control-the-steering-gear.html)

**——王俊皓、谭锦程、方鹏杰、张熙正、杜文彬、陈恩卓、宋子洋**

## XI. 后记

本文创作于2024年5月至6月，我的高一下学期。那时，我正因研究性学习任务忙得焦头烂额，一人承担了组内除问卷调查外的所有工作（是的，你看到的上文中所有任务分配其实都是应付学校评委老师的产物）……不过，我夜以继日的付出最终斩获了喜人的成就——我已一己之力带领全组斩获了华师一附中研究性学习一等奖（也有可能是选题和报告太过硬核）。

故我认为，我的一切工作都是值得的。这次任务让我踏入了嵌入式开发的大门，也锻炼了我C++代码编写的能力，进一步丰富了我对底层硬件的认知。完成这次开发后，我在嵌入式开发、物联网开发的领域也有了新的见解，新的项目诸如电解槽自动温控装置也陆续落成。因此可以说，这次开发探究的旅程带给我的并不仅仅是那张一等奖证书，更是打开创造力、想象力和工程能力等众妙之门的宝贵钥匙！

我仿佛可以看见，那通往技术未来的璀璨画卷，已在我脚下徐徐铺开！
